
1/4

ExampleSigmaClippedStatsTask
============================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1pipe_1_1tasks_1_1example_stats_tasks_1_1_example_sigma_clipped_stats_task.html

Example task to compute sigma-clipped mean and standard deviation of an image.

This is a simple example task designed to be run as a subtask by ExampleCmdLineTask. See also ExampleSimpleStatsTask as a variant that is even simpler.

The main method is run.

How to call with options/flags
++++++++++++++++++++++++++++++

Debugging
+++++++++ 

Specific functions of class
+++++++++++++++++++++++++++

__init__
---------

Construct an ExampleSigmaClippedStatsTask.

The init method may compute anything that that does not require data. In this case we create a statistics control object using the config (which cannot change once the task is created).

 
run
----

Compute and return statistics for a masked image.

Parameters:
- [in]	maskedImage:	masked image (an lsst::afw::MaskedImage)


Returns a pipeBase Struct containing:

- mean: mean of image plane
- meanErr: uncertainty in mean
- stdDev: standard deviation of image plane
- stdDevErr: uncertainty in standard deviation

Examples
++++++++

The whole example is simply spelled out in detail on the doxygen page.  It's brief.

What it returns
+++++++++++++++

