.. LSST DM Stack  documentation master file, created by
   sphinx-quickstart on Tue May 12 10:44:33 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

LSST DM Stack documentation
============================

We want to try to understand how the current DM Stack processes images, showing the steps in an interactive format.


.. From here on in the below we will use the color coding:
 - Green = code or executable to be run 
 - Blue and Cyan = data files to run over
 - Red = Flags
 - Magenta = lines of code


We will take the worked out ci_hsc pkg as an example, and we assume
the user has this installed already, along with the entire DM Stack
for the cmds to work.  For quick pointers on where to go to know how
to do the install, see the first link in the 'Contents' below.

Current Status
--------------

   astrometry    - need to find location of this exx code
   assembleccd   - covered at a decent level, needs cleanup
   calibimg      - needs running
   charimg
   coaddsrcxform
   diacat
   decorrALkernel
   deblendimg
   detectcoaddsrcs
   dipolemeas
   examplecmdline
   examplesigmaclippedstats
   examplesimplestats
   fittansip
   
   forcedmeas
   forcedsrcxform
   imagepsfmatch
   ingest
   install
   installgaussianpsf
   isrtask
   loadastrom
   loadrefobjects
   measureapcorr
   measuremergedcoaddsrcs
   mergedets
   mergemeasts
   modelpsfmatch
   objectsizestarsel
   processccd
   propvisitflags
   psfmatch
   readfitscat
   readtextcat
   safeclipassemble
   secondmomentstarsel
   singleframemeas
   sourcedet
   srcxform
   subtractbkgd
   snapcombine
   snappsfmatch
   xform
   template

Brief description of image processing
--------------------------------------

Image processing is one of the first steps that are undertaken in
analyzing data from a telescope for any purpose, be it astronomical,
astrophysical, or cosmological.  It generally consists of a few
separable steps:

 - Remove image defects in each CCD through ISR
 - Assemble the CCD's together into a large single image
 - Do characterization of the image

We'll now describe each of these steps in more detail.

-----------

Contents:

.. toctree::
   :maxdepth: 2

   astrometry   
   assembleccd
   calibimg
   charimg
   coaddsrcxform
   diacat
   decorrALkernel
   deblendimg
   detectcoaddsrcs
   dipolemeas
   examplecmdline
   examplesigmaclippedstats
   examplesimplestats
   fittansip
   forcedmeas
   forcedsrcxform
   imagepsfmatch
   ingest
   install
   installgaussianpsf
   isrtask
   loadastrom
   loadrefobjects
   measureapcorr
   measuremergedcoaddsrcs
   mergedets
   mergemeasts
   modelpsfmatch
   objectsizestarsel
   processccd
   propvisitflags
   psfmatch
   readfitscat
   readtextcat
   safeclipassemble
   secondmomentstarsel
   singleframemeas
   sourcedet
   srcxform
   subtractbkgd
   snapcombine
   snappsfmatch
   xform
   template
