
Characterizing an Image
========================

Given an exposure with defects repaired (masked and interpolated over, e.g. as output by IsrTask), this task does the kinds of things normally associated with e.g. SExtractor and PSFex.

For example, it will:

  - Detect and measure bright sources

  - Repair cosmic rays

  - Measure and subtract background

  - Measure PSF



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
