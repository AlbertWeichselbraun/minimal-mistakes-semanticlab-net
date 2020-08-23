---
title: Optimizing Data Retention in Postgresql
permalink: thesis/Optimizing_Data_Retention_in_Postgresql/
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

The IDIOM Media Watch builds upon [webLyzard](http://www.weblyzard.com)
a large-scale Web assessment and monitoring framework mirroring
thousands of pages in daily, weekly and monthly intervals. webLyzard's
database comprises millions of documents, annotations and pictures
stored in a [PostgreSQL](http://www.postgresql.org) database.

Handling this amount of data required intelligent data handling and
retention strategies distributing data among different kinds of storage
depending on its importance and usage levels. This thesis shall address
some of those challenges by implementing a postgresql module for
intelligent data retention and distribution.

Todo
----

The goals of this thesis are

1.  a literature and web research evaluating:
    1.  database data handling technologies (tablespaces, table
        partitioning, ...)
    2.  open source solutions and the techniques employing these
        techniques
    3.  methods for acquiring PostgreSQL database/table/row usage
        statistics

2.  design of a testcase for evaluating data retention
3.  implementation of 1-3 data retention strategies for postgresql

Literature
----------

-   [Postgresql homepage](http://www.postgresql.org) | [Table
    Partitioning](http://www.postgresql.org/docs/8.3/interactive/ddl-partitioning.html)
    | [Server
    Programming](http://www.postgresql.org/docs/8.3/static/server-programming.html)
-   [Create a Partitioned Table In
    PostgreSQL](http://postgresqldbnews.blogspot.com/2007/08/create-partitioned-table-in-postgresql.html)
-   <cite id="noyer2007">Noyer, Ulf and Ruschinzik, Martin and Rataj,
    Jürgen (2007). *Teile und herrsche - Tabellenpartitionierung in
    PostgreSQL*, iX - Magazin für Professionelle Informationstechnik,
    April 2007, pages 141--143</cite>
-   <cite id="kulev2007">Milen Kulev and Peter Welker (2007). *Data
    Warehouses & Open-Source-Datenbanken*, Datenbank-Spektrum,
    dpunkt.verlag, pages 25--36, 7(22)</cite>
-   [PLProxy](http://pgfoundry.org/projects/plproxy/) - a database
    partitioning system implemented as PL language
-   [PyReplica](http://pgfoundry.org/projects/pyreplica/) - a PostgreSQL
    Python-based Master/Slave replication system

