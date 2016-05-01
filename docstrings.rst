Docstrings
==========

Philosophie des docstrings
--------------------------

- documentation au plus près du code
- équivalant de javadoc (Java) et de doxygen (C++, ...)

Références (PEPs actives):

- PEP8_ "Python's good practices"
- PEP257_ "Docstring Conventions"
- PEP287_ "reStructuredText Docstring Format"

À titre d'information, les PEPs suivantes traitent aussi du sujet mais ont été
rejetées ou sont dépréciées:

- PEP216_ "Docstring Format" (remplacée par la PEP287_)
- PEP224_ "Attribute Docstrings" (rejetée)
- PEP256_ "Docstring Processing System Framework" (rejetée)
- PEP258_ "Docutils Design Specification" (rejetée)

cf. aussi  http://stackoverflow.com/questions/2557110/what-to-put-in-a-python-module-docstring.

cf. aussi le livre de Tarek Ziadé: Python, petit guide à l'usage du développeur agile

    Write docstrings for all public modules, functions, classes, and methods.
    Docstrings are not necessary for non-public methods, but you should have a
    comment that describes what the method does. This comment should appear
    after the def line.

Quelques mots à propos des *doctests*
-------------------------------------

Une extension des docstrings pour faire des tests unitaires.

Une alternative (ou un complément) à *unittest*.

