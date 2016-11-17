
SecondMomentStarSelectorTask
============================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1meas_1_1algorithms_1_1second_moment_star_selector_1_1_second_moment_star_selector_task.html#SecondMomentStarSelectorTask_

A star selector based on second moments.


(Warning: 
This is a naive algorithm; use with caution.)

How to call with options/flags
++++++++++++++++++++++++++++++

Like all star selectors, the main method is run.


Debugging
+++++++++ 

SecondMomentStarSelectorTask has a debug dictionary with the following keys:

- display -- bool; if True display debug information

display = lsstDebug.Info(name).display displayExposure = lsstDebug.Info(name).displayExposure pauseAtEnd = lsstDebug.Info(name).pauseAtEnd


Specific functions of class
+++++++++++++++++++++++++++

selectStars
------------
Return a list of PSF candidates that represent likely stars.

A list of PSF candidates may be used by a PSF fitter to construct a PSF.

Parameters:

- [in]	exposure --	the exposure containing the sources
- [in]	sourceCat --	catalog of sources that may be stars (an lsst.afw.table.SourceCatalog)
- [in]	matches --	astrometric matches; ignored by this star selector

Returns a lsst.pipe.base.Struct containing:

- starCat -- catalog of selected stars (a subset of sourceCat)


Examples
++++++++

None given..
 
What it returns
+++++++++++++++

