---
title: LaTeX Bibliography Management
permalink: thesis/LaTeX_Bibliography_Management/
layout: single
---

Motivation
==========

BibTeX is an open source software for managing and formatting
bibliographic references using LaTeX. Many current BibTeX
implementations have a number of shortcomings including:

1.  missing utf8 support
2.  the unnecessarily complicated bibstyle format (bst) for specifying a
    bibliography's format
3.  no support for bibliography formats other than .bib-files

Various projects to re-create BibTeX try to address these problems but
have failed so far to provide a feasible alternative to BibTeX.

The goal of this thesis is to

1.  determine criteria and requirements for a bibliography management
    software
2.  compare existing software to these requirements
3.  rewrite BibTeX (in python) addressing the shortcomings mentioned
    above, including the quality criteria identified above.

Tasks
=====

-   literature review: bibliography management (approaches,
    requirements, ...)
-   recherche: bibliography management software (commercial, open
    source, BibTex frontends)
-   latex bibtex integration
-   design: bibtex-ng
    -   utf8 support
    -   extensibility
    -   support of the traditional bibtex .bst format
    -   support of custom style files (compare: mlbibtex, ...)
    -   export formats (endnote, ...)
-   evaluation:
    -   BibTex compatibility
    -   usability

UML component diagram
=====================

![](Bibtex-ng.png "Bibtex-ng.png")

Student profile
===============

-   excellent programming skills (preferable in python)

Literature to start
===================

-   [bibtex wikipedia article](http://en.wikipedia.org/thesis/Bibtex)
-   [Designing BibTeX
    Styles](http://www.uic.edu/depts/accc/software/tex/btxhak.pdf)
-   Jean-Michel Hufflen: [*mlbibtex: a New Implementation of
    bibtex*](http://www.ntg.nl/eurotex/mlbibtex-euro.pdf)
-   [mlBibTEX: a
    Survey](http://www.guit.sssup.it/guitmeeting/2005/articoli/hufflen.pdf)
-   [Bibulus](http://www.nongnu.org/bibulus/) - a bibliography
    processing system
-   [EndNote](http://www.endnote.com) - Bibliographies Made Easy

