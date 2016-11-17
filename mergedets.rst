
1/4

MergeDetectionsTask
=========================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1pipe_1_1tasks_1_1multi_band_1_1_merge_detections_task.html#MergeDetectionsTask_

Merge coadd detections from multiple bands.

Command-line task that merges sources detected in coadds of exposures obtained with different filters.

To perform photometry consistently across coadds in multiple filter bands, we create a master catalog of sources from all bands by merging the sources (peaks & footprints) detected in each coadd, while keeping track of which band each source originates in.

The catalog merge is performed by getMergedSourceCatalog. Spurious peaks detected around bright objects are culled as described in CullPeaksConfig_.


How to call with options/flags
++++++++++++++++++++++++++++++

Debugging
+++++++++

The command line task interface supports a flag -d to import debug.py from your PYTHONPATH; see Using lsstDebug to control debugging output for more about debug.py files.

MergeDetectionsTask has no debug variables.



Specific functions of class
+++++++++++++++++++++++++++


__init__
----------

Initialize the merge detections task.

A FootprintMergeList will be used to merge the source catalogs.

Additional keyword arguments (forwarded to MergeSourcesTask.__init__):

Parameters:
- [in]	schema --	the schema of the detection catalogs used as input to this one
- [in]	butler	-- a butler used to read the input schema from disk, if schema is None
- [in]	**kwargs --	keyword arguments to be passed to MergeSourcesTask.__init__

The task will set its own self.schema attribute to the schema of the output merged catalog.


mergeCatalogs
--------------------

Merge multiple catalogs.

After ordering the catalogs and filters in priority order, getMergedSourceCatalog of the FootprintMergeList created by __init__ is used to perform the actual merging. Finally, cullPeaks is used to remove garbage peaks detected around bright objects.

Parameters:

- [in]	catalogs	
- [in]	patchRef	
- [out]	mergedList	



cullPeaks
----------

Attempt to remove garbage peaks (mostly on the outskirts of large blends).

Parameters:
- [in]	catalog --	Source catalog


getSchemaCatalogs
--------------------

Return a dict of empty catalogs for each catalog dataset produced by this task.

Parameters:
- [out]	dictionary 	of empty catalogs

getSkySourceFootprints
------------------------------

Return a list of Footprints of sky objects which don't overlap with anything in mergedList.

Parameters:
- mergedList --	The merged Footprints from all the input bands
- skyInfo --	A description of the patch
- growDetectedFootprints --	The number of pixels to grow the detected footprints


Examples
++++++++

The whole example is spelled out in detail on the doxygen page.

What it returns
+++++++++++++++

