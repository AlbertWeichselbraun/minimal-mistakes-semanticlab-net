---
title: Full Text Search in Databases
permalink: thesis/Full_Text_Search_in_Databases/
layout: single
---

Introduction
------------

The Media Watch on Climate Change aggregates, annotates, and visualizes
environmental articles from 150 Anglo-American news media sites. From
300,000 news media articles gathered in weekly intervals, the system
selects, annotates and indexes about 10,000 articles focusing on
environmental issues, before storing them in a central knowledge
repository, which can be navigated along multiple dimensions like time,
topics, keywords, and geographic proximity.

Despite innovative browsing aids like ontologies, semantic and
geographic maps most users still rely on full text search for navigating
through this vast document collection. Efficient full text search and
ranking algorithms therefore play a crucial role in providing a
user-friendly interface for document repositories.

Currently the Media Watch on Climate Change facilitates Tsearch2, a
search framework tightly integrated with its Postgresql database.
Comparing this framework with other open source solutions like
[Lucene](#Lucene "wikilink"), the [Full Text Search
Engine](#FTS "wikilink") and popular search algorithms like Google Page
Rank, HITS, and TrustRank shall pave the way for improving the user's
search experience in terms of speed and accuracy and providing more
advanced search options with a minimum on overheads.

Todo
----

The goals of this thesis are

1.  a literature and web research evaluating:
    1.  approaches towards full text search and ranking
        (algorithms, ...)
    2.  open source solutions and the techniques employed by them
    3.  evaluation techniques for full text searches (results,
        ranking, ...)

2.  the design of testcases for evaluating search results
3.  the implementation and evaluation of 1-3 full text search algorithms
    within PostgreSQL

Source
------

The sources and the completed theses can be downloaded from the svn
repository: <https://svn.semanticlab.net/svn/oss/thesis/fts/trunk>

Literature
----------

-   [Postgresql homepage](http://www.postgresql.org)
-   [Tsearch
    homepage](http://www.sai.msu.su/~megera/postgres/gist/tsearch/)
-   <cite id="Lucene">[Lucene](http://lucene.apache.org/) - A search
    framework developed by the apache foundation</cite>
-   <cite id="FTS">[Open Full Text
    Search](http://openfts.sourceforge.net/)</cite>
-   <cite id="PageRank">[Google Page
    Rank](http://en.wikipedia.org/thesis/PageRank)</cite>
-   <cite id="segaran2007">Segaran, Toby (2007). *Collective
    Intelligence - Building Smart Web 2.0 Applications*, pages 54-85,
    O'Reilly</cite>

