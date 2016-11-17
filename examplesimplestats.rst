
ExampleSimpleStatsTask 
=======================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1pipe_1_1tasks_1_1example_stats_tasks_1_1_example_simple_stats_task.html

Example task to compute mean and standard deviation of an image.

This was designed to be run as a subtask by ExampleCmdLineTask. It is about as simple as a task can be; it has no configuration parameters and requires no special initialization. See also ExampleSigmaClippedStatsTask as a variant that is slightly more complicated.

The main method is run.


How to call with options/flags
++++++++++++++++++++++++++++++

Debugging
+++++++++ 

This task has no debug variables.

Specific functions of class
+++++++++++++++++++++++++++

run
---

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

