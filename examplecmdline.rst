
ExampleCmdLineTask 
=========================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1pipe_1_1tasks_1_1example_cmd_line_task_1_1_example_cmd_line_task.html

Example command-line task that computes simple statistics on an image.

This task was written as an example for the documents How to Write a Task and How to Write a Command-Line Task. The task reads in a "calexp" (a calibrated science exposure), computes statistics on the image plane, and logs and returns the statistics. In addition, if debugging is enabled, it displays the image in ds9.

The image statistics are computed using a subtask, in order to show how to call subtasks and how to retarget (replace) them with variant subtasks.

The main method is run.

How to call with options/flags
++++++++++++++++++++++++++++++

Debugging
+++++++++ 

This task supports the following debug variables:

- display -- If True then display the exposure in ds9

To enable debugging, see Using lsstDebug to control debugging output.

Specific functions of class
+++++++++++++++++++++++++++


__init__
--------- 

Construct an ExampleCmdLineTask

Call the parent class constructor and make the "stats" subtask from the config field of the same name.

run
--------- 

Compute a few statistics on the image plane of an exposure.

Parameters:
- dataRef:	data reference for a calibrated science exposure ("calexp")

Returns a pipeBase Struct containing:

- mean: mean of image plane
- meanErr: uncertainty in mean
- stdDev: standard deviation of image plane
- stdDevErr: uncertainty in standard deviation

_getConfigName
------------------ 

Get the name prefix for the task config's dataset type, or None to prevent persisting the config.

This override returns None to avoid persisting metadata for this trivial task.

However, if the method returns a name, then the full name of the dataset type will be <name>_config. The default CmdLineTask._getConfigName returns _DefaultName, which for this task would result in a dataset name of "exampleTask_config".

Normally you can use the default CmdLineTask._getConfigName, but here are two reasons why you might want to override it:

If you do not want your task to write its config, then have the override return None. That is done for this example task, because I didn't want to clutter up the repository with config information for a trivial task.
If the default name would not be unique. An example is MakeSkyMapTask: it makes a sky map (sky pixelization for a coadd) for any of several different types of coadd, such as deep or goodSeeing. As such, the name of the persisted config must include the coadd type in order to be unique.
Normally if you override _getConfigName then you override _getMetadataName to match.


_getMetadataName
------------------

Get the name prefix for the task metadata's dataset type, or None to prevent persisting metadata.

This override returns None to avoid persisting metadata for this trivial task.

However, if the method returns a name, then the full name of the dataset type will be <name>_metadata. The default CmdLineTask._getConfigName returns _DefaultName, which for this task would result in a dataset name of "exampleTask_metadata".

See the description of _getConfigName for reasons to override this method.



Examples
++++++++

The example is simply spelled out in detail on the doxygen page.  It's brief.

What it returns
+++++++++++++++

