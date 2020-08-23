---
title: Identifying User Comments in Web sites using Site Style Trees
permalink: thesis/Identifying_User_Comments_in_Web_sites_using_Site_Style_Trees/
layout: single
---

Introduction
------------

User feedback and recommendations play a crucial role in customer
purchasing decisions. Research shows that customers put much trust in
user reviews and product recommendations. Automatically identifying and
extracting such comments from Web pages is far from trivial. This thesis
focuses on an approach for automatically identifying customer feedback
and forum discussions on Internet Web sites using site style trees
(SST). The SST algorithm detects recurring sections on Web pages by
comparing the DOM tree of different pages to each other and therefore
identifies the HTML elements containing user reviews or forum
discussions.

The goals of this thesis are

-   to implement an Java or Python based software which identifies
    relevant content using site style trees,
-   to assemble of a test corpus for evaluating content extraction
    methods and
-   to carry out an evaluation based on the programmed software.

Table of Contents
-----------------

1.  Introduction
2.  Importance of User Feedback and Word of Mouth in Marketing
3.  Web Page Parsing Approaches
    -   Style Trees

4.  Implementation
    -   Detect User Comments based on Style Trees

5.  Evaluation
    -   Test Corpus (TripAdvisor, ...)
    -   Metrics (precision, recall, F1)

6.  Outlook and Conclusions

Student Profile
---------------

-   A profound knowledge of HTML.
-   Good Java or Python skills. The implementation is an integral part
    of this thesis.

Hints
-----

-   merge non structural elements (a, br, b, p, ...)
-   remove signatures (lines starting with "\_\_\_" or "--")
-   observation: a complete comment can be seen in one subtree

Literature
----------

-   <cite id="bank2009"> Bank, Mathias and Mattes, Michael (2009).
    *Automatic User Comment Detection in Flat Internet Fora*, Twentieth
    International Workshop on Database and Expert Systems Application
    (DEXA 2009); Sixth International Workshop on Text-Based Information
    Retrieval TIR 2009, pages 373--377</cite>
-   T. Gottron. *Content extraction: Identifying the main content in
    HTML documents*, PhD Thesis, Johannes-Gutenberg University Mainz,
    2008
    [download](http://ubm.opus.hbz-nrw.de/volltexte/2009/1859/pdf/diss.pdf)
-   <cite id="lan2003">Yi, Lan, Liu, Bing and Li, Xiaoli (2003).
    *Eliminating noisy information in Web pages for data mining*, KDD
    '03: Proceedings of the ninth ACM SIGKDD international conference on
    Knowledge discovery and data mining, ISBN: 1-58113-737-0, ACM, pages
    296--305</cite>

