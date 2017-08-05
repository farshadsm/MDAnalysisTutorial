.. -*- coding: utf-8 -*-

==========================
 How to use this tutorial
==========================

We will first determine :ref:`if you need to install MDAnalysis
<have-you-installed-MDAnalysis>`. 

After that, the tutorial is designed to be read and worked through by
yourself at your own pace. It contains short examples that introduce
important features and ideas. You should run all these examples and
code snippets yourself. *Exercises* (with solutions) are
included. Follow tutorial online in your browser, starting with the
chapter :ref:`chapter-basics`.

.. RESTORE WHEN THE notebook HAS BEEN UPDATED
   * use the Jupyter ipython notebook `MDAnalysisTutorial.ipynb`_ (which
     contains all the code and exercises but fewer hyperlinks and images
     and less explanatory text). `Download the notebook`_ and open it
     with :program:`ipython`::

	jupyter notebook MDAnalysisTutorial.ipynb

.. _MDAnalysis: http://mdanalysis.org
.. _MDAnalysisTutorial.ipynb:
   http://nbviewer.ipython.org/github/MDAnalysis/MDAnalysisTutorial/blob/master/notebooks/MDAnalysisTutorial.ipynb
.. _`Download the notebook`:
   https://raw.githubusercontent.com/MDAnalysis/MDAnalysisTutorial/master/notebooks/MDAnalysisTutorial.ipynb



.. _have-you-installed-MDAnalysis:

Have you installed MDAnalysis?
==============================

Test if you can successfully import MDAnalysis: on the command line
start the ``python`` program

.. code-block:: bash

   python

and type ::

  import MDAnalysis
  from MDAnalysis.tests.datafiles import PSF, DCD

  print(MDAnalysis.Universe(PSF, DCD))
  print(MDAnalysis.__version__)

Do you see ``<Universe with 3341 atoms>`` and does the last command
print |MDAnalysis_version| or higher?

- **NO, I need to install MDAnalysis**: If you have not installed
  MDAnalysis yet or if you need to upgrade, start with
  :ref:`chapter-installing-mdanalysis`.
- **YES, I have the latest version installed**: You can immediately
  read about the initial :ref:`chapter-preparations`.

