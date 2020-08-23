---
title: Optimizing Database Access and Full Text Indexing for Large Scale Database Applications
permalink: thesis/Optimizing_Database_Access_and_Full_Text_Indexing_for_Large_Scale_Database_Applications/
layout: single
---

Optimizing Database Access and Full Text Indexing for Large Scale
Database Applications. (with a focus on Postgresql)

### Motivation

webLyzard is a platform for the automated analysis of content,
navigational system and interface design of networked information
systems. Through structural and textual metrics, webLyzard determines
success factors and uncovers weaknesses of deployed system by comparing
large samples of Web sites across region and industry. Currently, the
project mirrors and analyses more than 7,000 sites in monthly, weekly,
or daily intervals (www.weblyzard.com).

Many current research projects, including AVALON, IDIOM, RAVEN, and the
Election 2008 Monitor depend on accurate sampling of relevant media
sides. Richer media data like pictures, microformats, and annotations
put a serious strain on the database's performance.

The goal of this work is to design database test cases and to evaluate
how changes to the database's design, configuration, and database access
mechanisms influence the database's performance. In conjunction with
current full text indexing methods and database clustering toolkits
these techniques shall pave the way for high performance database access
and resolve current bottlenecks in the database configuration

### Tasks

1.  Literature review:
    1.  Postgres tuning tips (configuration parameters, query
        optimization, database design)
    2.  Database performance tests and metrics (e.g. number of
        transactions pre second, ...)

2.  Design Performance Test Cases
    1.  cover different aspects of database access (insert,
        update, select)
    2.  number of clients/connections

3.  Database access methods
    1.  python frameworks a'la SQL-Alchemy
    2.  prepared statements (implementation in java and
        python; pitfalls)
    3.  stored procedures (PG/SQL, PG/Python, ...)
    4.  full text searching (tsearch ii, ...)

4.  Database clustering/distributed access
    1.  skytools
    2.  other postgres based systems

### Starting Points

-   [Postgresql
    Documentation](http://www.postgresql.org/docs/8.3/interactive/index.html)
-   [Postgres Performance Pontificated](http://www.powerpostgresql.com/)
-   [Skype
    PL-Proxy](https://developer.skype.com/SkypeGarage/DbProjects/PlProxy)
-   [PGFoundry - Postgres Development Site](http://pgfoundry.org/)

