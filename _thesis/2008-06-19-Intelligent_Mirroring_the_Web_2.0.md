---
title: Intelligent Mirroring the Web 2.0
permalink: thesis/Intelligent_Mirroring_the_Web_2.0/
layout: single
---

Motivation
==========

The http-protocol provides mechanisms to determine whether a Web page
has changed since the last request. Leveraging this technology, web
spiders and proxy servers only download modified resources, leading to a
considerably better performance of Web spider architectures. Mirroring
and analysis of sites leveraging Web 2.0 technologies like AJAX and
dynamic HTML pose another serious challenge for current web spider
architectures. Due to dynamic elements modified by JavaScript and
similar technologies, simple HTML-to-text conversion techniques like
lynx and html2text do not deliver usable text representations of Web
documents. New approaches based on more advanced rendering architectures
are required to tackle this problem.

Tasks
=====

-   extend httrack to make use of etags and Last-Modified-Headers
-   implement, test and compare crawling and archiving strategies for
    httrack
-   literature review: conversion of Web 2.0 sites to text.

Literature to start
===================

-   RFC2616 (http://www.ietf.org/rfc/rfc2616.txt)
-   httrack (http://www.httrack.com)
-   Jansen, B.J., Mullen, T., Spink, A. and Pedersen, J. (2006).
    “Automated Gathering of Web Information: An In-depth Examination of
    Agents Interacting with Search Engines”, ACM Transactions on
    Internet Technology, 6(4): 442-464.
-   Wolf, J.L., Squillante, M.S., et al. (2002). "Optimal Crawling
    Strategies for Web Search Engines", 11th International Conference on
    World Wide Web. Honolulu, USA. 136-147.
-   Broder, A.Z., Najork, M. and Wiener, J.L. (2003). "Efficient URL
    Caching for World Wide Web Crawling", 12th International World Wide
    Web Conference. Budapest, Hungary. 679-689.

