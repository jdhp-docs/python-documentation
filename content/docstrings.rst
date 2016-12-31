.. _`docstring`:

Docstrings
==========

Brève description
-----------------

.. TODO: décrire en quelques lignes ce que sont les docstrings

Équivalant de javadoc (Java) et de doxygen (C++, ...)

Philosophie des docstrings
--------------------------

.. TODO: décrire en quelques lignes l'intéret des docstrings

- Documentation au plus près du code

Bonnes pratiques
----------------

.. TODO: résumer ici les bonnes pratiques les plus pertinentes pour mes projets
..       issues des PEPs citées plus loin...

Une docstring doit être associée à chaque

- module
- function
- classe
- methode

d'un projet Python.

Pour plus d'information, voir
https://www.python.org/dev/peps/pep-0257/#what-is-a-docstring

Exemple
-------

.. TODO: un exemple de module

.. code:: python

    # -*- coding: utf-8 -*-

    """
    This module does blah blah.

    Put here the description of the module.
    """

    def main():
        """
        This function does blah blah.
        
        Put here the description of the function.
        """

        print("Hello!")


Documents de références
-----------------------

Guides de référence pour la rédaction des docstrings en Python
(*PEPs actives*):

- PEP8_ "Python's good practices"
- PEP257_ "Docstring Conventions"
- PEP287_ "reStructuredText Docstring Format"

À titre d'information, les *PEPs* suivantes traitent aussi du sujet mais ont été
rejetées ou sont dépréciées:

- PEP216_ "Docstring Format" (remplacée par la PEP287_)
- PEP224_ "Attribute Docstrings" (rejetée)
- PEP256_ "Docstring Processing System Framework" (rejetée)
- PEP258_ "Docutils Design Specification" (rejetée)

.. _`doctest`:

.. _`unittest`:

Quelques mots à propos des *doctests*
-------------------------------------

Les docstrings python peuvent contenir des *doctests*.

Ces *doctests* permettent d'intégrés des *tests unitaires* à la documentation
(i.e. dans les docstrings).

Ils peuvent être utilisés comme alternative ou comme complément au framework
*unittest*.

Pour plus d'information, consulter https://docs.python.org/3/library/doctest.html.
