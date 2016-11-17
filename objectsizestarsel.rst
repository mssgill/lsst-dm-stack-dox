
ObjectSizeStarSelectorTask 
===========================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1meas_1_1algorithms_1_1object_size_star_selector_1_1_object_size_star_selector_task.html#ObjectSizeStarSelectorTask_

A star selector that looks for a cluster of small objects in a size-magnitude plot.


How to call with options/flags
++++++++++++++++++++++++++++++

Debugging
+++++++++ 

ObjectSizeStarSelectorTask has a debug dictionary with the following keys:

- display -- bool; if True display debug information

- displayExposure -- bool; if True display the exposure and spatial cells

- plotMagSize -- bool: if True display the magnitude-size relation using pyplot

- dumpData -- bool; if True dump data to a pickle file

Specific functions of class
+++++++++++++++++++++++++++

selectStars
------------

Return a list of PSF candidates that represent likely stars.

A list of PSF candidates may be used by a PSF fitter to construct a PSF.

Parameters:

- [in]	exposure --	the exposure containing the sources
- [in]	sourceCat --	catalog of sources that may be stars (an lsst.afw.table.SourceCatalog)
- [in]	matches	-- astrometric matches; ignored by this star selector

Returns a lsst.pipe.base.Struct containing:

- starCat -- catalog of selected stars (a subset of sourceCat)


Examples
++++++++

None given.
 
What it returns
+++++++++++++++

