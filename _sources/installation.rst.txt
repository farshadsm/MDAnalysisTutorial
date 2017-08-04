.. -*- coding: utf-8 -*-
.. highlight:: bash
   
.. _chapter-installing-mdanalysis:

=======================
 Installing MDAnalysis
=======================

Before you can start the tutorial, you need a working installation of
MDAnalysis_ (with its test suite, MDAnalysisTests_) on your Linux or Mac
OS X machine. The following contains hints and links to further
documentation to facilitate installation of the package. In an ideal
setting (development tools (gcc tool chain), python development
headers, full scientific Python stack with numpy, scipy, matplotlib
already installed, working netcdf/HDF5 library), installation will be
as simple as ::

   pip install --user MDAnalysis MDAnalysisTests

In a less ideal setting, one typically has to install additional
packages through the distribution's package manager as described in
the links under :ref:`local-installation`. 

.. Note:: For this tutorial, you will need at least version
          |MDAnalysis_version| of MDAnalysis.

.. _MDAnalysis: http://www.mdanalysis.org
.. _MDAnalysisTests: http://wiki.mdanalysis.org/UnitTests


.. _local-installation:

Installation methods
====================

For this tutorial you will install the latest release of
MDAnalysis. We recommend the :ref:`conda-installation` method but the
traditional :ref:`pip-installation` is also fully supported.


.. _conda-installation:

Conda installation
------------------

For this tutorial we recommend using the conda_ distribution. If you
do not have conda installed, you can download the miniconda_ installer
and install a small conda system, which will not interfere with other
installed software. Follow the instructions for miniconda_ for your
operating system.

The latest release of MDAnalysis_ (and the full test suite) can be
installed from the `conda-forge anaconda.org channel`_ with conda_ ::

  conda config --add channels conda-forge
  conda update --yes conda  

The current 0.16.x release only fully supports Python 2.7.x (the
upcoming 0.17 fully supports Python 2.7 and Python 3.4+)  so we need a
Python 2.7 environment that we call *mdaenv*::

  conda create --yes -n mdaenv python=2.7

Install MDAnalysis and the tests including data files in the *mdaenv*
environment::

  conda install --yes -n mdaenv mdanalysis MDAnalysisTests

Activate the installation (has to be done in every shell, whenever you
want to use MDAnalysis)::

  source activate mdaenv

Check success [#prompt]_::

  (mdaenv) $ python -c 'import MDAnalysis as mda; print(mda.__version__)'
  0.16.2
 
  
.. _conda: http://conda.pydata.org/docs/get-started.html
.. _miniconda: https://conda.io/miniconda.html
.. _conda-forge anaconda.org channel: https://anaconda.org/conda-forge/mdanalysis


.. _pip-installation:

Pip installation
----------------

.. note::
   Installation with pip_ requires a working C-compiler on the system
   because some parts of MDAnalysis are compiled. If you don't have a
   compiler toolchain configured, do the :ref:`conda-installation`.

The latest release of MDAnalysis_ (and the full test suite) can be
installed from the python package index with pip_ ::

  pip install --user MDAnalysis[analysis] MDAnalysisTests

(Installation of the test suite is required for this tutorial because
we will use some of the data files that are part of the tests. The
``[analysis]`` tag installs additional packages that are used in
specific analysis modules; although not used in this tutorial, it will
make your MDAnalysis installation full-featured from the start.)

If there are problems then please have a closer look at the
`installation notes`_ and the `installation recipes`_; in particular,
`installing the netcdf library`_ can become more involved.

If you need help with installation issues, please do not hesitate to
ask on the `user discussion group`_.


.. _pip: http://www.pip-installer.org/en/latest/index.html
.. _installation notes: http://wiki.mdanalysis.org/Install
.. _installation recipes: http://wiki.mdanalysis.org/InstallRecipes
.. _installing the netcdf library: http://wiki.mdanalysis.org/netcdf
.. _user discussion group: http://groups.google.com/group/mdnalysis-discussion
.. _tutorial git repository: https://github.com/MDAnalysis/MDAnalysisTutorial



Testing the installation
========================

.. _test cases: http://wiki.mdanalysis.org/UnitTests

MDAnalysis comes with over 5000 `test cases`_ that check its
functionality. These test cases can be run with the command ::

  python -c 'from MDAnalysis.tests import test; test()'

This can take a few minutes. Ideally, you should only get passing
tests ("ok" or just a single dot ".") or "KnownFailures".


.. rubric:: Footnotes

.. [#prompt] In the following, the shell's prompt is shown as
             ``(mdaenv) $`` and should *not* be typed. It is supposed
             to remind you that you *must be in the virtual
             environment* [#venv]_. Only type what follows after the
             prompt. If the commands give any output, it is shown on
             the lines following the input.

.. [#venv] Do not forget to activate the *mdaenv* environment whenever
           you open a new terminal::
	  
            source activate mdaenv

           Otherwise, you will probably find that scripts cannot find
           MDAnalysis.

	   If you want to use ``ipython`` (see
	   :ref:`ipython-interpreter`) or ``jupyter notebook`` then
	   you *must* install ``ipython`` and ``jupyter`` *into the
	   same virtual environment as MDAnalysis* or they might not
	   properly find other installed libraries such as MDAnalysis.
	    
.. highlight:: python
