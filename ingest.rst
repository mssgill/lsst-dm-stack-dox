Ingesting
=========

The first thing a user needs to do to process any img is ingest data files on disk.

Execute the correct EUPS setups, as so::

  cd  $LSSTSW/ci_hsc
  setup lsst_apps -t TagNumberYouInstalledWith
  setup   -r $LSSTSW/obs_subaru -t TagNumberYouInstalledWith
  setup   -k -r $LSSTSW/ci_hsc -t TagNumberYouInstalledWith

Then ingest as so::

 python $PIPE_TASKS_DIR/bin/ingestImages.py $LSSTSW/ci_hsc/DATA $LSSTSW/ci_hsc/raw/*.fits  --mode=link -c clobber=True register.ignore=True --doraise  

This will write out a registry.sqlite3 in your DATA subdir and make links to the science and calibration exposures.
