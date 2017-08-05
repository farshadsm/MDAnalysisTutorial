.. -*- coding: utf-8 -*-

.. _chapter-basics:

========
 Basics
========

We discuss the fundamental objects in MDAnalysis, the
:ref:`universe-and-atomgroup`, and the facilities for
:ref:`selections` of atoms. These selections themselves are again an
:class:`~MDAnalysis.core.groups.AtomGroup`.


.. _universe-and-atomgroup:

Universe and AtomGroup
======================

MDAnalysis is **object oriented**. Molecular systems consist of
:class:`~MDAnalysis.core.groups.Atom` objects (instances of the
class :class:`MDAnalysis.core.groups.Atom`), which are grouped in
:class:`~MDAnalysis.core.groups.AtomGroup` instances. You build the
:class:`~MDAnalysis.core.groups.AtomGroup` of your system by
loading a **topology** (list of atoms and possibly their connectivity)
together with a **trajectory** (coordinate information) into the
central data structure, the
:class:`~MDAnalysis.core.universe.Universe` object::

  >>> u = MDAnalysis.Universe(PSF, DCD)
  >>> print(u)
  <Universe with 3341 atoms>

The atoms are stored in the attribute
:attr:`~MDAnalysis.core.universe.Universe.atoms` of the
:class:`MDAnalysis.core.universe.Universe`::

  >>> print(u.atoms)
  <AtomGroup with 3341 atoms>
  >>> list(u.atoms[:5])
  [< Atom 1: name 'N' of type '56' of resname 'MET', resid 1 and segid '4AKE'>,
   < Atom 2: name 'HT1' of type '2' of resname 'MET', resid 1 and segid '4AKE'>,
   < Atom 3: name 'HT2' of type '2' of resname 'MET', resid 1 and segid '4AKE'>,
   < Atom 4: name 'HT3' of type '2' of resname 'MET', resid 1 and segid '4AKE'>,
   < Atom 5: name 'CA' of type '22' of resname 'MET', resid 1 and segid '4AKE'>]

Any :class:`~MDAnalysis.core.groups.AtomGroup` knows the residues
that the atoms belong to via the attribute
:attr:`~MDAnalysis.core.groups.AtomGroup.residues`, which produces a
:class:`~MDAnalysis.core.groups.ResidueGroup`. A
:class:`~MDAnalysis.core.groups.ResidueGroup` acts like a list of
:class:`~MDAnalysis.core.groups.Residue` objects::

  >>> u.atoms[100:130].residues
  <ResidueGroup with 3 residues>
  >>> list(u.atoms[100:130].residues)
  [<Residue LEU, 6>, <Residue GLY, 7>, <Residue ALA, 8>]

Larger organizational units are
:class:`~MDAnalysis.core.groups.Segment` instances, for example one
protein or all the solvent molecules or simply the whole
system. :class:`~MDAnalysis.core.groups.Atom`,
:class:`~MDAnalysis.core.groups.AtomGroup`,
:class:`~MDAnalysis.core.groups.Residue`, and
:class:`~MDAnalysis.core.groups.ResidueGroup` have an
attribute :attr:`~MDAnalysis.core.groups.AtomGroup.segments` that
will list the segment IDs ("segids") as a
:class:`~MDAnalysis.core.groups.SegmentGroup`::

  >>> u.atoms.segments
  <SegmentGroup with 1 segment>
  >>> list(u.atoms.segments)
  [<Segment 4AKE>]  

The converse is also true: each "higher" level in the hierarchy also
know about the :class:`~MDAnalysis.core.groups.Residue` and
:class:`~MDAnalysis.core.groups.Atom` instances it contains. For
example, to list the atoms of the
:class:`~MDAnalysis.core.groups.ResidueGroup` we had before::

  >>> r = u.atoms[100:130].residues
  >>> r.atoms
  <AtomGroup with 36 atoms>


Exercise 1
----------

1. What residue ("resname") does the last atom belong to in the above
   example? ::

    >>> r = u.atoms[100:130].residues
    >>> r.atoms[-1]
    <Atom 136: O of type 70 of resname ALA, resid 8 and segid 4AKE>

2. Why does the expression ::

     len(u.atoms[100:130]) == len(u.atoms[100:130].residues.atoms)
   
   return ``False``?

   Because the complete residues contain more atoms than the arbitrary
   slice of atoms.

3. How many residues are in the
   :class:`~MDAnalysis.core.groups.AtomGroup.Universe` ``u``? ::

     >>> len(u.atoms.residues)
     >>> u.atoms.n_residues
     214

   How do you get a list of the residue names (such as ``["Ala",
   "Gly", "Gly", "Asp", ...]``) and residue numbers ("resid") for
   atoms 1000 to 1300? And as a list of tuples ``(resname, resid)``
   (Hint: :func:`zip`)?::

     >>> resnames = u.atoms[999:1300].residues.resnames
     >>> resids = u.atoms[999:1300].residues.resids
     >>> list(zip(resnames, resids))

   How do you obtain the resid and the resname for the 100th residue?
   (Hint: investigate the :class:`~MDAnalysis.core.groups.Residue`
   object interactively with :kbd:`TAB` completion) ::

     >>> r100 = u.atoms.residues[99]
     >>> print(r100.resid, r100.resname)
     100 GLY


4. How many segments are there?  ::

     >>> len(u.segments)
     >>> len(u.atoms.segments)
     >>> u.atoms.n_segments
     1

   What is the segment identifier of the first
   :class:`~MDAnalysis.core.groups.Segment`? ::

     >>> s1 = u.segments[0]
     >>> s1.id
     '4AKE'
   

.. SeeAlso:: 

   Methods of :class:`~MDAnalysis.core.groups.AtomGroup`,
   :class:`~MDAnalysis.core.groups.ResidueGroup`, and
   :class:`~MDAnalysis.core.groups.SegmentGroup`
           
   * :attr:`~MDAnalysis.core.groups.AtomGroup.n_residues` and 
     :attr:`~MDAnalysis.core.groups.AtomGroup.n_atoms`
   * :attr:`~MDAnalysis.core.groups.AtomGroup.resids`
   * :attr:`~MDAnalysis.core.groups.AtomGroup.resnames`


.. _selections:

Selections
==========

.. TODO: named selections

MDAnalysis comes with a fairly complete `atom selection`_
facility. Primarily, one uses the method
:meth:`~MDAnalysis.core.universe.Universe.select_atoms` of a
:class:`~MDAnalysis.core.universe.Universe`::

  >>> CA = u.select_atoms("protein and name CA")
  >>> CA
  >>> <AtomGroup with 214 atoms>

but really any :class:`~MDAnalysis.core.groups.AtomGroup` has a
:meth:`~MDAnalysis.core.groups.AtomGroup.select_atoms` method::

  >>> acidic = CA.select_atoms("resname ASP or resname GLU")
  >>> acidic
  >>> <AtomGroup with 35 atoms>
  >>> list(acidic.residues)
  [<Residue GLU, 22>,
   <Residue ASP, 33>,
   <Residue GLU, 44>,
   ...
   <Residue GLU, 210>]
  
.. SeeAlso:: All the `selection keywords`_ are described in the documentation.

Numerical **ranges** can be written as ``first-last`` (or equivalently
``first:last`` [#ranges]_), where the range is *inclusive*. For example, get
residues with residue IDs 5 to 100::

  >>> u.select_atoms("resid 5-100")
  <AtomGroup with 1439 atoms>
  >>> u.select_atoms("resid 5-100").n_residues
  96
  
Selections can be combined with `boolean expressions`_. For example,
to select the :math:`\text{C}_\alpha` atoms of all acidic residues
[aspartic acid ("ASP"), glutamic acid ("GLU"), and histidines (named
"HIS", "HSD", or "HSE", depending on what force field is being used
and what protonation state it is in)]:

  >>> u.select_atoms("(resname ASP or resname GLU or resname HS*) and name CA")
  <AtomGroup with 38 atoms>

We group with ``or`` separate selections by residue name (keyword
``resname``). First either ASP, GLU, or any histidines are selected
(we use "stemming" ``HS*`` to match any residue name that starts with
"HS").  Then only those atoms whose name is "CA" are taken from the
first set by an ``and`` selection. For convenience, the ``or`` in the
first part of the selection can be taken implicitly with the shortcut
syntax

  >>> u.select_atoms("resname ASP GLU HS* and name CA")
  <AtomGroup with 38 atoms>

The *implicit or* syntax also works well for range selections such as
``resid 1-5 20 45-99 101-199``.

  
It is also possible to select by `geometric criteria`_, e.g. with the
:samp:`around {distance} {selection}` keyword::

  >>> u.select_atoms("((resname ASP or resname GLU) and not (backbone or name CB or name CG)) \
                   and around 4.0 ((resname LYS or resname ARG) \
                                    and not (backbone or name CB or name CG))").residues
  <ResidueGroup with 30 residues>

This selection will find atoms potentially involved in salt bridges
between acidic and basic residues.

.. _boolean expressions:
   http://www.mdanalysis.org/docs//documentation_pages/selections.html#boolean

.. _geometric criteria:
   http://www.mdanalysis.org/docs//documentation_pages/selections.html#geometric   

   

Exercises 2
-----------

1. Select the range of resids 100 to 200 ("100-200") with a
   selection. Compare the result to what you get by slicing the
   :attr:`u.atoms.residues` appropriately.

   Which approach would you prefer to use in a analysis script?

   Solution::

      >>> u.select_atoms("resid 100-200")
      <AtomGroup with 1609 atoms>

   Compare to the slicing solution (doing an element-wise comparison,
   i.e. residue by residue in each :func:`list`)::

      >>> list(u.select_atoms("resid 100-200").residues) == list(u.atoms.residues[99:200])
      True

   If one wants to get specific residues in scripts one typically uses
   selections instead of slicing because the index in the slice might
   not correspond to the actual residue ids (minus 1): If a number of
   residues (e.g. 150-160) are missing from the structure then the
   selection will simply give you residues 100-149 and 161-200 but the
   slice 99:200 would give you residues 100-149 and *161-209*.

2. Select all residues that do not contain a :math:`\mathrm{C}_\beta`
   ("CB") atom. How many are there? What residue names did you find? 

   Solution::

      >>> sel = u.select_atoms("(byres name CA) and not (byres name CB)").residues
      >>> len(sel)
      20

   These are all Glycines, as can be seen by comparing the residue
   groups element-wise::

      >>> glycines = u.select_atoms("resname GLY")
      >>> list(sel) == list(glycines.residues)
      True


.. _atom selection: 
   http://docs.mdanalysis.org/documentation_pages/selections.html

.. _selection keywords:
   http://docs.mdanalysis.org/documentation_pages/selections.html#selection-keywords

   
.. rubric:: Footnotes

.. [#ranges] For index ranges in atom selections, ``first-last`` and
             ``first:last`` are completely equivalent. In this
             tutorial we prefer the form ``first-last`` to reduce
             confusion with Python slicing ``group[first:last]``
             because in the atom selection syntax, ``last`` is
             *included* in the selection whereas in Python slicing it
             is *excluded*.
