

Characterizing an Image
========================

Given an exposure with defects repaired (masked and interpolated over, e.g. as output by IsrTask), this task does the kinds of things normally associated with e.g. SExtractor and PSFex.

Some of its primary functions are to:

  - Detect and measure bright sources

  - Repair cosmic rays

  - Measure and subtract background

  - Measure the PSF



Debugging
+++++++++

The command line task interface for charImg supports a flag '--debug'
to import debug.py from your $PYTHONPATH; see `Using lsstDebug to
control debugging output`_ for more about debug.py.

.. _Using lsstDebug to control debugging output: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/base_debug.html

CharacterizeImageTask has a debug dictionary with the following keys:

- frame
int: if specified, the frame of first debug image displayed (defaults to 1)

- repair_iter
bool; if True display image after each repair in the measure PSF loop

- background_iter
bool; if True display image after each background subtraction in the measure PSF loop

- measure_iter
bool; if True display image and sources at the end of each iteration of the measure PSF loop See lsst.meas.astrom.displayAstrometry for the meaning of the various symbols.

- psf
bool; if True display image and sources after PSF is measured; this will be identical to the final image displayed by measure_iter if measure_iter is true

-repair
bool; if True display image and sources after final repair

-measure
bool; if True display image and sources after final measurement


Specific functions of CharImg via example
+++++++++++++++++++++++++++++++++++++++++

Overall: Once the exposures are processed initially minimally by IsrTask, it is passed here CharImg.

   - Characterize the image: measure bright sources, fit a background and PSF, and repair cosmic rays
     
    - Calibrate the exposure: measure faint sources, fit an improved WCS and get the photometric zero-point

Characterize
------------

This detect and measures sources and estimates the PSF.

Interpolates over cosmic rays.

Perform final measurement.

Estimates a background for the exposure, and then subtracts this from the image itself.


Cosmic Ray Repair
-----------------

 CharImg first detects CR's using the function RepairTask, whose
 purpose is to initially detect the CR streaks, and then to
 interpolate smoothly over them so that they are entirely masked out.

 
 
Detect, Measure, and Estimate Psf 
----------------------------------

This installs a simple PSF model (replacing the existing one, if need be).

Returns a source catalog, background, PSF model.

..
  467         - interpolate over cosmic rays with keepCRs=True
  468         - estimate background and subtract it from the exposure
  469         - detect, deblend and measure sources, and subtract a refined background model;
  470         - if config.doMeasurePsf:
