ProcessCcd
==========

Next, let’s look inside processCcd.py::

	python pathToExecutableVersionOf/processCcd.py pathTo/DATA --VariousFlags

Real example version for me::

 python $LSSTSW/stack/DarwinX86/pipe_tasks/2016_01.0-35-g183e2ce/bin/processCcd.py $LSSTSW/ci_hsc/DATA --rerun ci_hsc --id visit=903986 ccd=23 --doraise

General outline of what processCcd does:

1. Remove instrument signature: Call isr to unpersist raw data and assemble it into a post-ISR exposure.
   
2. Characterize image to estimate PSF and background: Call charImage subtract background, fit a PSF model, repair cosmic rays, detect and measure bright sources, and measure aperture correction.
   
3. Calibrate astrometry and photometry: Call calibrate to perform deep detection, deblending and single-frame measurement, refine the WCS and fit the photometric zero-points.


Doing the Instrumental Signature Removal
+++++++++++++++++++++++++++++++++++++++++

Instrumental Signature Removal (ISR) is a sequence of steps taken to
'clean' images of various aspects of defects that any system of optics
and detectors will imprint on an image by default.  Though the process
for correcting imaging data is very similar from camera to camera,
depending on the image, various of the defects will be present and
need to be removed, and thus the sequence of steps taken will vary
from image to image.  Generally these corrections are done one CCD at
a time (but all 16 amplifiers at once), and that is how the DM code
ingests and processes the information.

The ISR code is at::
   
     $IP_ISR_DIR/python/lsst/ip/isr/isrTask.py.


IsrTask provides a vanilla implementation of doing these corrections,
including the ability to turn certain corrections off if they are not
needed.

The inputs to the primary method, 'run', are a raw exposure to be
corrected and the calibration data products. The raw input is a single
chip-sized mosaic of all amps including overscans and other
non-science pixels.

IsrTask performs instrument signature removal on an exposure following these overall steps:

- Detects saturation, apply overscan correction, bias subtraction, dark and flat
- Performs CCD assembly
- Masks known bad pixels
- Interpolates over defects, saturated pixels and all NaNs
- Provides a preliminary WCS


Functions the code is capable of handling, though not all are used, depending on an image (alphabetical order):

- Bias 
- Brighter fatter correction:
- Dark
- Flat-fielding
- Fringing
- Gain
- Linearization
- Mask defects, and interpolate over them
- Mask NaNs 
- Overscan
- Saturation detection
- Saturation interpln
- Suspect pixel detection
- Update variance plane 

If you want to see an example of the ISR algorithm in action, run the example while in the $IP_ISR_DIR as follows::

  python  examples/runIsrTask.py  --write --ds9

The ‘write’ flag tells the code to write the post-ISR image file to disk.  In this example code, this output file is called:: 

   postISRCCD.fits

The ‘ds9’ flag tells it to bring up ds9 (if installed) and show the post-ISR FITS image.

  
.. ISR does the following:
            - assemble raw amplifier images into an exposure with image, variance and mask planes
    
	    
Specific functions of IsrTask via example
+++++++++++++++++++++++++++++++++++++++++

We will follow the simple steps in runIsrTask to trace how a specific
code would do ISR processing -- it will be different for every camera and
exposure.

The first several lines of runIsrTask (after imports) define a
function runIsr that has the following in it::

    #Create the isr task with modified config
    isrConfig = IsrTask.ConfigClass()
    isrConfig.doBias = False #We didn't make a zero frame
    isrConfig.doDark = True
    isrConfig.doFlat = True
    isrConfig.doFringe = False #There is no fringe frame for this example

The first line indicates this is a section about setting up the
configuration that the code will be run with.  The next several set up
specific flags, indicating that we will not do bias or fringing
corrections in this code, but will do the dark and flat corrections.

It then defines parameters that it will use to make the raw, flat and
dark exposures, using knowledge of our camera and exposures::
  
    DARKVAL = 2. #e-/sec
    OSCAN = 1000. #DN
    GRADIENT = .10
    EXPTIME = 15 #seconds
    DARKEXPTIME = 40. #seconds

Next, it makes the 3 exposures that we will be using in this example to create the final corrected output exposure::

  
    darkExposure = exampleUtils.makeDark(DARKVAL, DARKEXPTIME)
    flatExposure = exampleUtils.makeFlat(GRADIENT)
    rawExposure = exampleUtils.makeRaw(DARKVAL, OSCAN, GRADIENT, EXPTIME)

(We are using functions defined in exampleUtils, also in the examples
subdir inside $IP_ISR_DIR, these are modified versions of the standard
functions inside the full Utils pkg (where is this?).

Finally, the output is produced with the line::

       output = isrTask.run(rawExposure, dark=darkExposure, flat=flatExposure)

And returned at the end of the function.

(The 'main' function of runIsrTask simply calls this runIsr function, and also brings
up ds9 to view the final output exposure if that flag is set on, and
writes the img to disk if that flag is set.)

Next, let's look at the two specific functions that the example uses.

Dark correction
---------------

The dark current is the signal introduced by thermal electrons in the
silicon of the detectors with the camera shutter closed. Dark
correction is done by subtracting a reference Dark calibration
frame that has been scaled to the exposure time of the visit image.

Flat fielding
-------------

The flat-field correction (often called "flat fielding") removes the
variations in the pixel-to-pixel response of the detectors. The
flat-field is derived for each filter in several ways, depending on
the telescope: from images of the twilight sky ("twilight flats");
from a screen within the dome ("dome flats"); or from a simulated
continuum source. In all cases the flat-field corrects approximately
for vignetting across the CCD (i.e. the variation in the amount of
light that hits the detector due to angle of incidence into the
aperture at the top of the telescope tube, and the resultant shadow
from one side) . The flat-field correction is performed by dividing
each science frame by a normalized, reference flat-field image for the
corresponding filter.


Other ISR steps
+++++++++++++++

Now we'll describe a few corrections that are not in the example, but
that IsrTask can also take correct for, leading to final corrected
images.

Bias correction
----------------

The bias correction is applied to remove the additive electronic
bias that is present in the signal chain. To first
approximation, the bias is a constant pedestal, but it has low-amplitude structure
that is related to its electronic stability during
read-out of the detector segment. The processing pipeline removes the
bias contribution in a two-step process. In the first step, the median
value of non-flagged pixels in the overscan region is subtracted from
the image. In the second step, the reference bias image is subtracted
from the science image to remove the higher-order structure.

Following the bias correction, the pixels are scaled by the gain
factor for the appropriate CCD. The brightness units are electrons (or
equivalently for unit gain, detected photons) for calibrated images.

More specifically, the IsrTask biasCorrection method takes as
arguments the science exposure and the bias exposure, and first checks
if they have the same exact footprint (i.e. if the 4 corners are all
at the same locations), and if not, it raises a RuntimeError saying
that they’re not the same size.

If they are the same size, it takes the masked science exposure and
simply does a straight subtraction (pixel by pixel) of the bias
exposure, and returns this.

Cross-Talk Correction
----------------------

Cross-talk introduces a small fraction of the signal from one CCD into
the signal chain of the CCD that shares the same electronics, resulting in “ghosts” of bright objects appearing in the paired CCD. This is an
additive effect, and is most noticeable for sources that are very bright, at or
near saturation.

(Not clear if LSST CCDs will need this correction, so the pipeline has
a placeholder for it, should it be necessary, but no cross-talk
correction is implemented at this time.)

Fringe Pattern Correction
-------------------------

A fringe pattern is many detectors in particularly the reddest
filters: the iʹ′-, zʹ′-, and y-bands. The pattern occurs because of
interference between the incident, nearly monochromatic light from
night sky emission lines (both from air glow from particular
components of the atmosphere, especially OH, and from reflected city
lights) and the layers of the CCD substrate. The details of the fringe
pattern depend mostly upon the spatial variation in thickness of the
top layer of the substrate, but also depend upon a number of other
factors including the wavelength(s) of the incident emission lines,
the composition of the substrate, the temperature of the CCD, and the
focal ratio of the incident beam. The amplitude of the fringe pattern
background varies with time and telescope pointing.


Linearity Correction
--------------------

The response of the CCD detectors to radiation is highly linear for
pixels that are not near saturation, to typically better than 0.1% for
most recent cameras.


Currently, no linearity correction is applied in the pipelines.

Were a correction necessary it would likely be implemented with a
look-up table, and executed following the dark correction but prior to
fringe correction.

____

[Reference: Doxygen comments in code, and Section 4 of LSST DATA CHALLENGE HANDBOOK (2011) ]
