---
title: Optimizing Geographic Tagging
permalink: thesis/Optimizing_Geographic_Tagging/
layout: single
---

Introduction
------------

The vision of the Geospatial Web combines geographic data, Internet
technology and social change. Geospatial applications like the IDIOM
Media Watch on Climate Change facilitate geo-annotation services to
refine Web pages and media articles with geographic tags.

Identifying the document's target geographies is a rather complex task,
complicated by geo/geo ambiguities (e.g. Vienna/at versus
Vienna/Virginia/us) and geo/non-geo ambiguities like turkey/bird versus
Turkey/country. Most approaches toward tagging the target geography
therefore facilitate machine learning technologies, gazetteers, or a
combination of both to identify geo-tags. The gazetteer's size and many
internal tuning parameter determine the geo-tagger's performance and its
bias towards identifying smaller geographic-entities or higher-level
units. Designing a geo-tagger and choosing these parameters often
involve trade-offs; improvements in one particular area does not
necessarily yield better results in other areas.

The goals of this thesis are

1.  designing a testcase for evaluating geo-taggers
2.  implementing this testcase as a unittest
3.  applying the framework to different approaches towards geo-tagging.

Todo
----

-   Literature recherches
    -   geo-tagging algorithms
    -   public geo coding API's (evaluation)
-   Design geo-testcases (different gazetteer sizes, different regions)
-   Implement geo-unittests
-   Modifiy and measure the performance of different geo-algorithms

Literature
----------

-   E. Amitay, N. Har'El, R. Sivan, and A. Soer. "Web-a-where:
    geotagging web content". In SIGIR '04: Proceedings of the 27th
    annual international ACM SIGIR conference on Research and
    development in information retrieval, pages 273280, New York, NY,
    USA, 2004. ACM.
-   R. Beierheimer: "Geo Tagging of Web Resources", Bakkalaureatsarbeit
    an der Technischen Universität Graz, Sept. 2006
-   A. Weichselbraun: "A Utility-Testing Centered Approach for
    Optimizing Geo-Tagging", draft

