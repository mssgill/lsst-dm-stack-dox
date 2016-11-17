
LoadReferenceObjectsTask 
=========================

- `Doxygen link`_
.. _Doxygen link: https://lsst-web.ncsa.illinois.edu/doxygen/x_masterDoxyDoc/classlsst_1_1meas_1_1algorithms_1_1load_reference_objects_1_1_load_reference_objects_task.html#LoadReferenceObjectsTask_

Abstract base class for tasks that load objects from a reference catalog in a particular region of the sky.

Implementations must subclass this class, override the loadSkyCircle method, and will typically override the value of ConfigClass with a task-specific config class.

How to call with options/flags
++++++++++++++++++++++++++++++

Debugging
+++++++++ 

Specific functions of class
+++++++++++++++++++++++++++

__init__
---------

Construct a LoadReferenceObjectsTask.

Parameters:

- [in]	butler --	A daf.persistence.Butler object. This allows subclasses to use the butler to access reference catalog files using the stack I/O abstraction scheme.

loadPixelBox 
-------------

Load reference objects that overlap a pixel-based rectangular region.

The search algorithm works by searching in a region in sky coordinates whose center is the center of the bbox and radius is large enough to just include all 4 corners of the bbox. Stars that lie outside the bbox are then trimmed from the list.

Parameters:

- [in]	bbox	bounding box for pixels (an lsst.afw.geom.Box2I or Box2D)
- [in]	wcs	WCS (an lsst.afw.image.Wcs)
- [in]	filterName	name of camera filter, or None or blank for the default filter
- [in]	calib	calibration, or None if unknown

Returns a lsst.pipe.base.Struct containing:

- refCat --  a catalog of reference objects with the standard schema as documented in LoadReferenceObjects, including photometric, resolved and variable; hasCentroid is False for all objects.
- fluxField -- name of flux field for specified filterName


 

loadSkyCircle
-------------

Load reference objects that overlap a circular sky region.

Parameters:

- [in]	ctrCoord	center of search region (an lsst.afw.geom.Coord)
- [in]	radius	radius of search region (an lsst.afw.geom.Angle)
- [in]	filterName	name of filter, or None for the default filter; used for flux values in case we have flux limits (which are not yet implemented)

Returns an lsst.pipe.base.Struct containing:

- refCat a catalog of reference objects with the standard schema as documented in LoadReferenceObjects, including photometric, resolved and variable; hasCentroid is False for all objects.

- fluxField = name of flux field for specified filterName


makeMinimalSchema
-----------------

Make the standard schema for reference object catalogs.

Parameters:

- [in]	filterNameList --	list of filter names; used to create filterName_flux fields
- [in]	addFluxSigma --	if True then include flux sigma fields
- [in]	addIsPhotometric --	if True add field "photometric"
- [in]	addIsResolved --	if True add field "resolved"
- [in]	addIsVariable --	if True add field "variable"


joinMatchListWithCatalog
------------------------

Relink an unpersisted match list to sources and reference objects.

A match list is persisted and unpersisted as a catalog of IDs produced
by afw.table.packMatches(), with match metadata (as returned by the
astrometry tasks) in the catalog's metadata attribute. This method
converts such a match catalog into a match list (an
lsst.afw.table.ReferenceMatchVector) with links to source records and
reference object records.

Parameters:

- [in]	matchCat --	Unperisted packed match list (an lsst.afw.table.BaseCatalog). matchCat.table.getMetadata() must contain match metadata, as returned by the astrometry tasks.

- [in,out]	sourceCat --	Source catalog (an lsst.afw.table.SourceCatalog). As a side effect, the catalog will be sorted by ID.

Returns the match list (an lsst.afw.table.ReferenceMatchVector)



_addFluxAliases
---------------

Add aliases for camera filter fluxes to the schema

If self.config.defaultFilter then adds these aliases:

- camFlux:      <defaultFilter>_flux
- camFluxSigma: <defaultFilter>_fluxSigma, if the latter exists

For each camFilter: refFilter in self.config.filterMap adds these aliases:

- <camFilter>_camFlux:      <refFilter>_flux
- <camFilter>_camFluxSigma: <refFilter>_fluxSigma, if the latter exists

@throw RuntimeError if any reference flux field is missing from the schema


_trimToBBox
------------

Remove objects outside a given pixel-based bbox and set centroid and hasCentroid fields.

Parameters:
- [in]	refCat	a catalog of objects (an lsst.afw.table.SimpleCatalog, or other table type that supports getCoord() on records)
- [in]	bbox	pixel region (an afwImage.Box2D)
- [in]	wcs	WCS used to convert sky position to pixel position (an lsst.afw.math.WCS)

Returns a catalog of reference objects in bbox, with centroid and hasCentroid fields set

	

Examples
++++++++

None given.
 
What it returns
+++++++++++++++

