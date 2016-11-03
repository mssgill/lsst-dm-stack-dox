measure faint sources, fit an improved WCS and get the photometric zero-point


Calibrating an Image
=====================

Overall:


    Given an exposure with a good PSF model and aperture correction map
    (e.g. as provided by CharacterizeImageTask), perform the following operations:
    - Run detectAndMeasure subtask to peform deep detection and measurement
    - Run astrometry subtask to fit an improved WCS
    - Run photoCal subtask to fit the exposure's photometric zero-point

      

Debugging
+++++++++


Specific functions of CalibImg
+++++++++++++++++++++++++++++++

Calibrate (*calibrate*)
------------------------

The detectAndMeasure routing is run again, yielding another version of the source catalog, and the background.

Next astrometry is done against a known catalog, and all matches are returned in a different catalog.

Then photometric calibration is done by matching to known sources, determining a photometric zero-point and returning the result.


Persisting the outputs (*writeOutputs*)
-----------------------------------------

*getSchemaCatalogs*
-------------------

*setMetadata*
--------------

*copyIcSourceFields*
--------------------


