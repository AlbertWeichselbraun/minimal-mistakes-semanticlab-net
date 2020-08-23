---
title: Automatically Learning Text Patterns to Extract Relations from Domain Documents
permalink: thesis/Automatically_Learning_Text_Patterns_to_Extract_Relations_from_Domain_Documents/
layout: single
---

Background
----------

[Ruiz-Casado et al.](#ruiz2007 "wikilink") extend
[WordNet](#fellbaum2008 "wikilink") by extracting hyponym, hyperonym,
holonym and meronym relations from the simple english version of
WikiPedia. The authors automize

-   the extraction of relations and
-   the process of learning textual patterns modeling these
    relations (e.g. X is one of the PLURAL-NOUN in Y)

The described approach applies the following steps:

-   word sense disambiguation
-   pattern extraction based on existing relations in WordNet
-   pattern generalization of the patterns retrieved in the step above
-   identification of new relations

The authors show that the precision of the generated patterns is similar
to patterns written by hand.

Tasks
-----

-   implement a simple vector-space-based component for word sense
    disambiguation
-   extract lexical patterns from a corpus based on known relations
-   implement an algorithm for generalizing these patterns
-   test these pattern on the corpus for identifying new relations.

Literature
----------

1.  <cite id="ruiz2007"> Ruiz-Casado, Maria, Alfonseca, Enrique and
    Castells, Pablo (2007). *Automatising the learning of lexical
    patterns: An application to the enrichment of WordNet by extracting
    semantic relationships from Wikipedia*, Data \\& Knowledge
    Engineering, pages 484 - 499, 61(3)</cite>
2.  <cite id="hearst_automatic_1992">Hearst, Marti A. (1992). *Automatic
    Acquisition of Hyponyms from Large Text Corpora*, Proceedings of the
    Fourteenth International Conference on Computational Linguistics
    (COLING'92), pages 539--545</cite>
3.  <cite id="fellbaum1998">Fellbaum, C. (1998). *WordNet - An
    Electronic Lexical Database*, Computational Linguistics, pages
    292--296, 25(2)</cite>

