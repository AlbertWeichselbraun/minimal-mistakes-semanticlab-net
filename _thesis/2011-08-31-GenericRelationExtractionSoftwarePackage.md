---
title: GenericRelationExtractionSoftwarePackage
permalink: thesis/GenericRelationExtractionSoftwarePackage/
layout: single
---

Software Package for Thesis Generic Relation Extraction
-------------------------------------------------------

This package includes the following software tools:

-   RelationExtractor
-   PatternInspector
-   PatternClassifier
-   OpenCalaisClient

### OpenCalaisClient

Is a command line tool, used to access the OpenCalais API for extracting
entities and relations from articles. The result of this task forms our
reference set. Its main class is

    weber.test.openCalais.TestOpenCalais

and does not have any parameters. Database connection is hardcoded.

### RelationExtractor

Our prototype is a command line tool for extracting entities and
relation by using StanfordNLP package. Its main class is

    wu.j0125536.extraction.RelationExtraction

and can take two parameters:

    -nXXX...the number of articles that should be processed
    -firstXXX...the first article_id, the prototype should start with

If no parameters are provided, this tool processes all articles starting
with the lowest article\_id. Tested with Java VM argument -Xmx5000m.

### PatternInspector

This is the only GUI tool in this project and is used to identify good
and bad patterns manually. It allows the user to search for patterns or
concrete examples represented by a pattern. Furthermore, inapropriate
patterns can be disabled. The main class of the inspector is

    wu.j0125536.inspector.PatternInspector

and does not use any parameters. Tested with Java VM argument -Xmx2000m.

### PatternClassifier

Finally, the pattern classifier command line tool works on manually
tagged patterns to learn how good and bad patterns look. Afterwards it
tags remaining patterns to improve the precision of our prototype. The
main class is

    wu.j0125536.classify.PatternClassifier

and does not use any parameters.
