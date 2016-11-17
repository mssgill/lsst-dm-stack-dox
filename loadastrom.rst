
LoadAstrometryNetObjects
=========================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1meas_1_1astrom_1_1load_astrometry_net_objects_1_1_load_astrometry_net_objects_task.html

Load reference objects from astrometry.net index files. 


How to call with options/flags
++++++++++++++++++++++++++++++

Debugging
+++++++++ 

Specific functions of class
+++++++++++++++++++++++++++

loadSkyCircle
--------------
Load reference objects that overlap a circular sky region. 

Returns	an lsst.pipe.base.Struct containing:

- refCat -- a catalog of reference objects with the standard schema as documented in LoadReferenceObjects, including photometric, resolved and variable; hasCentroid is False for all objects.

 - fluxField -- name of flux field for specified filterName


readIndexFiles
--------------

Read all astrometry.net index files, if not already read. 
 

getMIndexesWithinRange
----------------------
Get list of muti-index objects within range. More...
 
getSolver
---------

Examples
++++++++

LoadAstrometryNetObjectsTask is a subtask of AstrometryTask, which is called by PhotoCalTask. See meas_photocal_photocal_Example.



What it returns
+++++++++++++++

