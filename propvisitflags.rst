
PropagateVisitFlagsTask 
=========================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1pipe_1_1tasks_1_1propagate_visit_flags_1_1_propagate_visit_flags_task.html#PropagateVisitFlagsTask_

Task to propagate flags from single-frame measurements to coadd measurements.

Propagate flags from individual visit measurements to coadd measurements

We want to be able to set a flag for sources on the coadds using flags that were determined from the individual visits. A common example is sources that were used for PSF determination, since we do not do any PSF determination on the coadd but use the individual visits. This requires matching the coadd source catalog to each of the catalogs from the inputs (see PropagateVisitFlagsConfig.matchRadius), and thresholding on the number of times a source is flagged on the input catalog.

An important consideration in this is that the flagging of sources in the individual visits can be somewhat stochastic, e.g., the same stars may not always be used for PSF determination because the field of view moves slightly between visits, or the seeing changed. We there threshold on the relative occurrence of the flag in the visits (see PropagateVisitFlagsConfig.flags). Flagging a source that is always flagged in inputs corresponds to a threshold of 1, while flagging a source that is flagged in any of the input corresponds to a threshold of 0. But neither of these extrema are really useful in practise.

Setting the threshold too high means that sources that are not consistently flagged (e.g., due to chip gaps) will not have the flag propagated. Setting that threshold too low means that random sources which are falsely flagged in the inputs will start to dominate. If in doubt, we suggest making this threshold relatively low, but not zero (e.g., 0.1 to 0.2 or so). The more confidence in the quality of the flagging, the lower the threshold can be.

The relative occurrence accounts for the edge of the field-of-view of the camera, but does not include chip gaps, bad or saturated pixels, etc.

How to call with options/flags
++++++++++++++++++++++++++++++



Debugging
+++++++++ 

Specific functions of class
+++++++++++++++++++++++++++

__init__
---------

run
---------
Propagate flags from individual visit measurements to coadd. 

This requires matching the coadd source catalog to each of the catalogs from the inputs, and thresholding on the number of times a source is flagged on the input catalog. The threshold is made on the relative occurrence of the flag in each source. Flagging a source that is always flagged in inputs corresponds to a threshold of 1, while flagging a source that is flagged in any of the input corresponds to a threshold of 0. But neither of these extrema are really useful in practise.

Setting the threshold too high means that sources that are not consistently flagged (e.g., due to chip gaps) will not have the flag propagated. Setting that threshold too low means that random sources which are falsely flagged in the inputs will start to dominate. If in doubt, we suggest making this threshold relatively low, but not zero (e.g., 0.1 to 0.2 or so). The more confidence in the quality of the flagging, the lower the threshold can be.

The relative occurrence accounts for the edge of the field-of-view of the camera, but does not include chip gaps, bad or saturated pixels, etc.

Parameters:

- [in]	butler --	Data butler, for retrieving the input source catalogs
- [in,out]	coaddSources --	Source catalog from the coadd
- [in]	ccdInputs --	Table of CCDs that contribute to the coadd
- [in]	coaddWcs --	Wcs for coadd

getCcdInputs
------------
Convenience method to retrieve the CCD inputs table from a coadd exposure. 


Examples
++++++++

Minimal example spelled out in detail on the doxygen page.

What it returns
+++++++++++++++

