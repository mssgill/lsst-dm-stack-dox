
1/4

TransformTask
=========================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1pipe_1_1tasks_1_1transform_measurement_1_1_transform_task.html#TransformTask_

Transform a SourceCatalog containing raw measurements to calibrated form. 

Given a set of measurement algorithms with their associated configuration, the table of source measurements they have produced, and information about an associated WCS and calibration, transform the raw measurement output to a calibrated form.

Transformations are defined on a per-measurement-plugin basis. In addition, a configurable set of fields may be simply copied from the input to the output catalog.

This task operates on an input SourceCatalog and returns a BaseCatalog containing the transformed results. It requires that the caller supply information on the configuration of the measurement task which produced the input data as well as the world coordinate system and calibration under which the transformation will take place. It provides no functionality for reading or writing data from a Butler: rather, per-dataset-type command line tasks are provided to obtain the appropriate information from a Butler (or elsewhere) and then delegate to this task.

How to call with options/flags
++++++++++++++++++++++++++++++

Debugging
+++++++++ 

Specific functions of class
+++++++++++++++++++++++++++


__init__
---------

Initialize TransformTask.

Parameters:

- [in]	measConfig --	Configuration for the measurement task which produced the measurments being transformed.
- [in]	inputSchema --	The schema of the input catalog.
- [in]	outputDataset --	The butler dataset type of the output catalog.
- [in]	*args --	Passed through to pipeBase.Task.__init__()
- [in]	*kwargs --	Passed through to pipeBase.Task.__init__()


getSchemaCatalogs
------------------

Return a dict containing an empty catalog representative of this task's output. 
 

run
---------

Transform raw source measurements to calibrated quantities.

Parameters:

- [in]	inputCat --	SourceCatalog of sources to transform.
- [in]	wcs --	The world coordinate system under which transformations will take place.
- [in]	calib --	The calibration under which transformations will take place.

Returns a BaseCatalog containing the transformed measurements.

Examples
++++++++

None.

What it returns
+++++++++++++++

