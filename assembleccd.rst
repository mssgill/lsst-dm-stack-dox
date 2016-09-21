
Assembling Subimages into a Single Image
=========================================

    This task assembles sections of an image into a larger mosaic.  The sub-sections
    are typically amplifier sections and are to be assembled into a detector size pixel grid.
    The assembly is driven by the entries in the raw amp information.  The task can be configured
    to return a detector image with non-data (e.g. overscan) pixels included.  The task can also 
    renormalize the pixel values to a nominal gain of 1.  The task also removes exposure metadata that 
    has context in raw amps, but not in trimmed detectors (e.g. 'BIASSEC').
