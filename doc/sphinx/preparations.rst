.. -*- coding: utf-8 -*-

.. _chapter-preparations:

==============
 Preparations
==============

.. _ipython-interpreter:

Python interpreter: ``ipython``
===============================

In the following we are using `ipython`_ as our interactive Python
interpreter [#ipython_install]_. It has a number of very useful features:

* use the interactive help (:samp:`{command}?` or
  :samp:`{command}??`)

* :kbd:`TAB` completion, e.g. :code:`MDAnalysis.U<TAB>` will
  autocomplete to :code:`MDAnalysis.Universe`. 

  :code:`MDAnalysis.Universe.<TAB>` will show all methods and
  attributes.

* quick plotting with :mod:`matplotlib` (and array manipulations with
  :mod:`numpy`)

Start :program:`ipython`::

  ipython  --matplotlib

Inside :program:`ipython`, load :mod:`numpy` ::

  import numpy as np

as we will constantly make use of its capabilities.

.. _ipython: http://ipython.org/



Loading MDAnalysis
==================

MDAnalysis is primarily a library that provides means to work with
particle-based simulation trajectories (including single frames such
as PDB files). As such, it is mainly used 

#. in scripts
#. for interactive use

In both cases, we always import the module :mod:`MDAnalysis` at the top level::
  
  import MDAnalysis

(Not all sub-modules are imported automatically; for instance,
analysis modules such as :mod:`MDAnalysis.analysis.rms` have to be
imported explicitly.)

MDAnalysis comes with a bunch of test files and trajectories. One is a
trajectory of the enzyme adenylate kinase that samples a transition
from a closed to an open conformation [Beckstein2009]_, which we will
use as an example throughout the tutorial. The topology file (CHARMM
PSF format) and trajectory (CHARMM DCD format) can be loaded into the
variables :code:`PSF` and :code:`DCD`::

  from MDAnalysis.tests.datafiles import PSF, DCD


.. rubric:: Footnotes

.. [#ipython_install] If you do not have ipython_ installed then you
   can install it. If you are using the :ref:`conda-installation`):

   .. code-block:: bash

	conda install -n mdaenv ipython

   and if you are using the :ref:`pip-installation`:

   .. code-block:: bash

	pip install --user ipython

