---
title: LaTeX Hacks
layout: single
alias: /index.php/LaTeX_Hacks
categories: latex
excerpt: A list of useful hacks for working with LaTeX.

---
{% include toc %}

A list of useful hacks for working with LaTeX.

LaTeX
=====

LaTeX snippets which might be useful;)

Subequations
------------

The *amsmath* packages provides support for subequations - the equations
in the example above will therefore get the numbers *1a* and *1b*.

``` LaTeX
  \begin{subequations}
    \begin{eqnarray}
      \label{eq:pyt}
        a^2 &=& b^2 + c^2 \\
      \label{eq:c}
        a &=& c\cdot cos(\phi)
     \end{eqnarray}
   \end{subequations}
```

Tables
------

-   Huge Tables: use the [supertabular
    environment](http://www.ifi.uio.no/it/latex-links/supertabular.pdf)
    or its successor the [xtable
    environment](http://www.ctan.org/tex-archive/macros/latex/contrib/xtab/xtab.pdf).
-   The [longtable
    environment](ftp://ftp.tex.ac.uk/tex-archive/macros/latex/required/tools/longtable)
    allows multi-page tables as well, but offers a much better control
    over line breaks.
-   colorize cells/rows/columns: use the [colortbl
    package](http://www.ctan.org/tex-archive/macros/latex/contrib/colortbl/colortbl.pdf).

``` latex
\begin{tabular}{lcc}
Service  & Utility                      & Comment \\\hline
MyLab    & \cellcolor[gray]{0.5} 4000.1 & example1 \\
TestLab  & 43928.50                     & \cellcolor[gray]{0.8} example2 \\
\end{tabular}
```

-   Handling [Multirow and multicolumn
    spanning](http://andrewjpage.com/index.php?/archives/43-Multirow-and-multicolumn-spanning-with-latex-tables.html)
    with latex tables.

Add Comments to PDFs
--------------------

Install (and use ;)
[PDFComment](http://pdfcomment.josef-kleber.de/en_index.htm). Add the
following snippet to the beginning of your paper:

``` LaTeX
  % start_pdfcomments
  \usepackage{marginnote}
  \usepackage[svgnames]{xcolor}
  \usepackage[colorlinks=true,linkcolor=black,citecolor=black,urlcolor=blue,plainpages=false,linktocpage]{hyperref}
  \usepackage{ifpdf}
  \usepackage{xkeyval}
  \usepackage{hycolor}
  \usepackage[color=Yellow,author={Albert Weichselbraun},final]{pdfcomment}
  % end_pdfcomments
```

Depending on your LaTeX installation you might be required to copy
updated hycolor.sty, pdfcomment.sty, xcolor-patch.sty into your working
directory.

BibTeX
======

This section contains various hacks related to BibTeX.

Bibliography styles
-------------------

-   Please take a look at Surajit Ray's page on [bibliography and
    citation styles](http://www.stat.psu.edu/~surajit/present/bib.htm).

Multiple Bibliographies
-----------------------

-   Use the
    [multibib](http://www.ctan.org/tex-archive/macros/latex/contrib/multibib/) package.

Finalizing Papers
=================

The following snippets remove pdf-comments and change the link
highlighting:

``` LaTeX
  \usepackage[colorlinks=true,linkcolor=black,citecolor=black,urlcolor=blue,plainpages=false,linktocpage]{hyperref}
  \usepackage[color=Yellow,author={Albert Weichselbraun},final]{pdfcomment}
```

Manipulating LaTeX, Postscript, PNG and PDF
===========================================

Hacks for manipulating various LaTeX output formats like .pdf and
postscript.

Extracting Formulas, Tables or other Parts from LaTeX documents
---------------------------------------------------------------

-   Use the [preview
    package](http://www.ctan.org/tex-archive/macros/latex/contrib/preview/)
    to extract specific parts of the LaTeX document
-   `latex` `fname;` `dvipng` `fname` will extract the table as an
    PNG-Image from the document below (provided that it has been saved
    as `fname.tex`)

``` LaTeX
\documentclass[a4paper,10pt]{article}
\usepackage[active,floats]{preview}


\begin{document}

\pagestyle{empty}

\begin{table*}
\begin{tabular}{cc}
 $a, b, c$ & $f(a, b, c)$ \\\hline
  1, 1, 1  & 0.10 \\
  1, 1, 2  & 0.03 \\
  1, 2, 2  & 0.10 \\
  1, 2, 3  & 0.10 \\
  2, 2, 1  & 0.50 \\
  2, 2, 2  & 0.15 \\
  2, 3, 2  & 0.05 \\
  2, 3, 3  & 0.05 \\
  \ldots   &  \ldots \\
\end{tabular}
\end{table*}
\end{document}
```

Embedding fonts in a PDF
------------------------

pdflatex/pdftex do not embed all fonts in their default configuration.
Some publishers (for instance IEEE when using IEEE PDF eXpress) require
submitting papers with embedded fonts. The following command line
creates a PDF conforming to these requirements:

```bash
 pdf2ps article.pdf - |ps2pdf -dPDFSETTINGS=/prepress - article_embedded.pdf
```

Reducing the size of a PDF file
-------------------------------

```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
```

Other settings for `-dPDFSETTINGS` are `/ebook` and `/printer`, `/prepress`,
`/default`.

Converting Postscript to png
----------------------------

```bash
 pstoimg -density 300 -antialias -aaliastext -multipage file.ps
```

Converting SVG to EPS
---------------------

```bash
 inkscape tagcloud-mass-media.svg -E tagcloud-mass-media.eps --export-ignore-filters --export-ps-level=3
```

pdftk Tools
-----------

These tools support all kinds of manipulations of .pdf-documents like
merging, splitting, rotating, filling of forms, applying of watermarks,
repairing corrupted pdf-files (where possible), etc.

Example: join pdf-files:

` pdftk 1.pdf 2.pdf cat output combined.pdf`

PDFjam for handouts and more
----------------------------

PDFjam is used to manipulate PDF files and provides the following
functions:

- `pdfnup`, put multiple PDF pages on one page,
- `pdfjoin`, combine PDF files,
- `pdf90`, rotate PDF files.

A full overview over PDFjam's functionality is available
[here](http://www2.warwick.ac.uk/fac/sci/statistics/staff/academic/firth/software/pdfjam/).

```bash
  pdfnup --nup 2x2 --frame false --noautoscale false --orient landscape --delta "0.2cm 0.3cm" --scale 0.95 slides.pdf
```

Converting transparent PNGs for use with LaTeX
----------------------------------------------

Sometimes LaTeX does not handle the transparency of PNGs correctly. Use
ImageMagick to convert the transparency of such images into a proper
color (white) for printing:

``` bash
  convert -background white -layers merge input.png output.png
```

Source:
[Lenni.Info](http://lenni.info/blog/2009/08/converting-transparent-pngs-for-use-with-latex/)

Create thumbnails from PDF files
--------------------------------

The following command creates thumbnails of 72dpi (default) and a width
of 100 pixels from the pages of a PDF document:

``` bash
    convert file.pdf -resize 100 thumb.jpg
```

You end up with as many jpegs as the PDF document had pages.

Literature
==========

- [Ghostscript documentation](http://pages.cs.wisc.edu/~ghost/doc/)
- [ps2pdf documentation](http://pages.cs.wisc.edu/~ghost/doc/svn/Ps2pdf.htm)

