Les outils
==========

Cette partie présente les principaux outils utilisés pour générer la
documentation d'un projet à partir des docstrings dans un format plus agréable
à lire et plus facile à partager pour les utilisateurs (HTML, PDF, ...).
  
.. _`docutils`:

Docutils
--------

Les *docutils* sont des outils distribués avec Python pour convertir les
fichiers reStructuredText en HTML, LaTeX, etc.

Ce sont les outils de référence pour convertir les documents reStructuredText
mais il en existe d'autres développés par des tiers : Pandoc, rst2pdf, etc.

.. _`pandoc`:

Pandoc
------

Pandoc est un logiciel capable de traduire un grand nombre de formats de
documents.

Il permet entre autre de convertir des fichiers Markdown, HTML, Latex ou DocBook
en documents reStructuredText et inversement.

Pandoc peut être utilisé comme alternative aux docutils_.

Pour plus d'information, voir http://pandoc.org/.


.. Include options:
.. http://docutils.sourceforge.net/docs/ref/rst/directives.html#include

.. include:: pydoc.rst

.. include:: epydoc.rst

.. include:: sphinx.rst

