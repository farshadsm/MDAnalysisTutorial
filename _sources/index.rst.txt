.. -*- mode: reST; coding: utf-8 -*-
.. MDAnalysis Tutorial documentation master file, created by
   sphinx-quickstart on Thu Oct 30 00:40:26 2014.

MDAnalysis Tutorial
===================

:MDAnalysis version: ≥ |MDAnalysis_version|
:Tutorial release: |release|
:Last updated: |today|


MDAnalysis_ is an open source Python library that helps you to quickly
write your own analysis algorithm for studying trajectories produced
by the most popular simulation packages [Gowers2016]_
[Michaud-Agrawal2011]_.

This tutorial serves as an **introduction to MDAnalysis**. It starts
out with *installing the library* and then introduces the key components
of the library. It will show you 

* how to load a structure or a MD trajectory; 
* how to select parts of your system;
* how to work with atoms, residues and molecules through the object-oriented
  interface of MDAnalysis;
* how to analyze MD trajectories;
* how to write out modified trajectories;
* how to use algorithms in the  `MDAnalysis.analysis`_ module
  (intermediate level of difficulty)

The tutorial contains many links to the `online documentation`_ ,
which you can use to learn more about the functions, classes, an
methods that are discussed. The online help together with the
interactive Python documentation (``help(...)`` or ``...?`` in
:program:`ipython`) should help you while you are using the library.

If you have **questions or suggestions** please post them in the
`MDAnalysis User Discussion Group`_.

.. _MDAnalysis: http://www.mdanalysis.org
.. _online documentation: http://docs.mdanalysis.org/
.. _MDAnalysis.analysis: http://docs.mdanalysis.org/documentation_pages/analysis_modules.html
.. _MDAnalysis User Discussion Group: http://groups.google.com/group/mdnalysis-discussion

Begin the tutorial with :doc:`howto` and use the *sidebar* for navigation.

.. Contents
.. --------
..
.. Alabaster includes the TOC as a collapsible sidebar. Hide it here.

.. toctree::
   :maxdepth: 2
   :numbered:	      
   :hidden:	      

   howto
   installation
   preparations
   basics
   atomgroups   
   trajectories
   writing
   analysismodule	
   references

