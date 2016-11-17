
MergeMeasurementsTask
=========================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1pipe_1_1tasks_1_1multi_band_1_1_merge_measurements_task.html#MergeMeasurementsTask_

Merge measurements from multiple bands.

Command-line task that merges measurements from multiple bands.

Combines consistent (i.e. with the same peaks and footprints) catalogs of sources from multiple filter bands to construct a unified catalog that is suitable for driving forced photometry. Every source is required to have centroid, shape and flux measurements in each band.

How to call with options/flags
++++++++++++++++++++++++++++++

Debugging
+++++++++ 

The command line task interface supports a flag -d to import debug.py from your PYTHONPATH; see Using lsstDebug to control debugging output for more about debug.py files.

MergeMeasurementsTask has no debug variables.


Specific functions of class
+++++++++++++++++++++++++++

__init__
-----------
Initialize the task.

Additional keyword arguments (forwarded to MergeSourcesTask.__init__):

Parameters:

- [in]	schema:	the schema of the detection catalogs used as input to this one
- [in]	butler:	a butler used to read the input schema from disk, if schema is None

  The task will set its own self.schema attribute to the schema of the output merged catalog.

mergeCatalogs
--------------

Merge measurement catalogs to create a single reference catalog for forced photometry.

Parameters:

- [in]	catalogs:	the catalogs to be merged
- [in]	patchRef:	patch reference for data

For parent sources, we choose the first band in config.priorityList for which the merge_footprint flag for that band is is True.

For child sources, the logic is the same, except that we use the merge_peak flags.

Examples
++++++++


Simple example spelled out in detail on the doxygen page.  It's brief.

What it returns
+++++++++++++++

deepCoadd_ref{tract,patch}: SourceCatalog
