
MeasureApCorrTask
=========================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1meas_1_1algorithms_1_1measure_ap_corr_1_1_measure_ap_corr_task.html

Task to measure aperture correction.

This task measures aperture correction for the flux fields returned by lsst.meas.base.getApCorrNameSet()

The main method is run.

How to call with options/flags
++++++++++++++++++++++++++++++

Debugging
+++++++++ 

The command line task interface supports a flag --debug to import debug.py from your $PYTHONPATH; see Using lsstDebug to control debugging output for more about debug.py.

MeasureApCorrTask has a debug dictionary containing a single boolean key:

- display -- If True: will show plots as aperture corrections are fitted

Specific functions of class
+++++++++++++++++++++++++++

__init__
---------

Construct a MeasureApCorrTask.

For every name in lsst.meas.base.getApCorrNameSet():

- If the corresponding flux fields exist in the schema:
  - Add a new field apcorr_{name}_used
  - Add an entry to the self.toCorrect dict
- Otherwise silently skip the name

run
---

Measure aperture correction.

Parameters

- [in]	exposure --	Exposure aperture corrections are being measured on. Aside from the bounding box, the exposure is only used by the starSelector subtask (which may need it to construct PsfCandidates, as PsfCanidate construction can do some filtering). The output aperture correction map is not added to the exposure; this is left to the caller.

- [in]	catalog --	SourceCatalog containing measurements to be used to compute aperturecorrections.

Returns a lsst.pipe.base.Struct containing:

- apCorrMap: an aperture correction map (lsst.afw.image.ApCorrMap) that contains two entries for each flux field:
  - flux field (e.g. base_PsfFlux_flux): 2d model-
  - flux sigma field (e.g. base_PsfFlux_fluxSigma): 2d model of error

Examples
++++++++

None given.
 
What it returns
+++++++++++++++

