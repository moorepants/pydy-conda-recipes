This repository contains all of the recipes used to build the packages at
http://anaconda.org/pydy.

PyDy Build Example
==================

For each release of PyDy we upload binaries for the conda package manager to
anaconda.org for easy installation using conda. For every conda package there
should be a directory containing at least three files: ``meta.yaml``,
``bld.bat``, and ``build.sh``. The directory should be named as such
``pydy-X.X.X`` where ``X.X.X`` is the PEP 440 compliant version number. For
instructions on building a conda package see the conda documentation:
http://conda.pydata.org.

The basic process for creating and uploading a new package is as follows:

Install the needed packages::

   $ conda update conda
   $ conda install conda-build anaconda-client

Create a new directory for the PyDy version and copy the files from the
previous version (or use ``conda skeleton pypi pydy``)::

   $ mkdir pydy-X.X.X
   $ cp pydy-Y.Y.Y/* pydy-X.X.X/

Edit the files to reflect any new changes in to the package (especially
dependency changes) and run conda build for each version of Python to build
against::

   $ conda build --python X.X pydy-X.X.X

This will build the default package for your computer architecture. Since PyDy
is a pure Python package we can generate the packages for other architectures
with a single command::

   $ conda convert --platform all /home/<username>/<miniconda|anaconda>/conda-bld/linux-64/pydy-X.X.X-py27_0.tar.bz -o pydy-X.X.X/build

Finally, each of these packages can be uploaded to anaconda with::

   $ anconda upload --user pydy pydy-X.X.X/build/<arch>/pydy-X.X.X-py27_0.tar.bz
