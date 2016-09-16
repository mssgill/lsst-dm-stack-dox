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


Doing the ISR
+++++++++++++

The ISR code is at::
   
     $IP_ISR_DIR/python/lsst/ip/isr/isrTask.py.

The ISR code processes one CCD at a time.

The process for correcting imaging data is very similar from camera to camera. IsrTask provides a vanilla implementation of doing these corrections, including the ability to turn certain corrections off if they are not needed. 

The inputs to the primary method, run, are a raw exposure to be corrected and the calibration data products. The raw input is a single chip-sized mosaic of all amps including overscans and other non-science pixels. 

IsrTask performs instrument signature removal on an exposure following these overall steps:

- Detect saturation, apply overscan correction, bias subtraction, dark and flat
- Perform CCD assembly
- Mask known bad pixels
- Interpolate over defects, saturated pixels and all NaNs
- Provide a preliminary WCS


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
    
	    
Specific functions of IsrTask
+++++++++++++++++++++++++++++


Bias correction
----------------

The IsrTask biasCorrection method takes as arguments the science
exposure and the bias exposure, and first checks if they have the same
exact footprint (i.e. if the 4 corners are all at the same locations),
and if not, it raises a RuntimeError saying that they’re not the same
size.

If they are the same size, it takes the masked science exposure and
simply does a straight subtraction (pixel by pixel) of the bias
exposure, and returns this.

