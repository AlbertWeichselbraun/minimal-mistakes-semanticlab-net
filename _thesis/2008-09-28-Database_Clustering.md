---
title: Database Clustering
permalink: thesis/Database_Clustering/
layout: single
---

(with a focus on Postgresql)

Motivation
==========

The IDIOM Media Watch on Climate Change visualizes contextualized
information spaces comprising millions of documents. User navigate this
repository alongside multiple dimensions and formulate queries based on
textual, semantic, or geospatial criteria. High performance database
solutions are required to support real time browsing and searching of
this vast document collection.

Database clustering has the potential to provide the following benefits:

-   high throughput due to the distribution of requests through multiple
    nodes (load balancing)
-   high availability (transparent failover)
-   higher maintainability (defect nodes are easily replaceable)

The goal of this thesis is to evaluate database clustering approaches
and technologies considering the potential benefits outlined above with
a focus on postgresql.

Tasks
=====

1.  Literature review:
    1.  Database clustering approaches (commercial, literature)
        1.  advantages and drawbacks of these approaches
        2.  load balancing, replication, ...

    2.  Database clustering and Postgresql

2.  Requirement Analysis
3.  Design Performance Test Cases
    1.  cover different aspects of database access (insert,
        update, select)
    2.  number of clients/connections

4.  Evaluation
    1.  data definition language (DDL)
    2.  data manipulation language (DML)

5.  Outlook and conclusions

Starting Points
===============

-   [Postgresql
    Documentation](http://www.postgresql.org/docs/8.3/interactive/index.html)
-   [Postgres High Availability and Load
    Balancing](http://www.postgresql.org/docs/8.3/static/high-availability.html)
-   [Skype
    PL-Proxy](https://developer.skype.com/SkypeGarage/DbProjects/PlProxy)
-   [PGFoundry - Postgres Development Site](http://pgfoundry.org/)
-   [Recommended Postgresql Load Balancing
    Solutions](http://www.nntp.perl.org/group/perl.dbi.users/2007/01/msg30673.html)
-   [PgPool](http://pgpool.projects.postgresql.org/)
-   [Mammoth
    Replicator](http://www.commandprompt.com/products/mammothreplicator/)
-   [Slony](http://www.slony.info/)

