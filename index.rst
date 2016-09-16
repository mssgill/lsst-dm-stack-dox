.. LSST DM Stack  documentation master file, created by
   sphinx-quickstart on Tue May 12 10:44:33 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

LSST DM Stack documentation
====================

We want to try to understand how the current DM Stack processes images, showing the steps in an interactive format.


.. From here on in the below we will use the color coding:
 - Green = code or executable to be run 
 - Blue and Cyan = data files to run over
 - Red = Flags
 - Magenta = lines of code


We will take the worked out ci_hsc pkg as an example, and we assume the user has this installed already, along with the entire DM Stack for the cmds to work.  For quick pointers on where to go to know how to do the install, see the first link below.

Contents:

.. toctree::
   :maxdepth: 2

   install
   ingest
   processccd
   