---
title: Thesis Templates
permalink: thesis/Thesis_Templates/
layout: single
alias: /index.php/Thesis_Templates
---

The following template has been compiled by M. Pimmer and M. Alexander.

Usage
=====

Unpack the [archive](/assets/thesis/Thesis_template.tar.gz)
in your working directory. Adjust the `Makefile`, if necessary. To build
your work call

```bash
make
```

To completely rebuild your thesis (and update bibliographic references) call
```bash 
make all
```

Files
=====

Important files:

- `bakkarbeit.tex`    ... the LaTeX main file for writing your work  
- `bakkarbeit.bib`    ... contains the bibliographic references

Auxiliary files:

- `Makefile`           ... controls how your thesis is build  
- `abstract.bst`       ... style for the formatting of bibliographic references  
- `itp_bakkarbeit.sty` ... style for the format of the thesis  
- `titlepage.sty`      ... titlepage style

Credits
=======

This template has been compiled by M. Pimmer (initial version) and M.
Alexander (extensions).
