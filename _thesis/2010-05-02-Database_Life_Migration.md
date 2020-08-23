---
title: Database Life Migration
permalink: thesis/Database_Life_Migration/
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

The IDIOM Media Watch builds upon webLyzard a large-scale Web assessment
and monitoring framework mirroring thousands of pages in daily, weekly
and monthly intervals. webLyzard's database comprises millions of
documents, annotations and pictures stored in a
[PostgreSQL](http://www.postgresql.org) database.

Currently database upgrades and data transfers require a considerable
effort in terms of man hours and server outage. The goal of this thesis
is providing a framework for database live migration based on the
PL/Python database language. The framework will enable the transfer of
whole databases or tables between databases and provide optional support
for the translation of data constructs between those databases.

Todo
----

The goals of this thesis are

1.  overview: use of databases in data mining, e-marketing and
    information retrieval
2.  traditional approaches and problems in database migration (postgres
    8.2 -&gt; copy/restore, ...)
3.  literature and web research evaluating:
    1.  database migration and synchronization strategies for open
        source databases with a focus on postgresql (e.g. slony, ...)
    2.  closed source solutions (e.g. oracle & co)
    3.  open source solutions and the techniques employing these
        techniques

4.  requirement definition for such a solution
5.  design & implementation of a life database migration framework
6.  testing / evaluation
7.  outlook and conclusions

Framework
---------

The following graphic outlines the general structure of this framework.
Two adapter components (DataBaseMigrationConnector and
DataBaseMigrationConnectorSlave) allow the translation of tables and the
whole database. Translation profiles facilitate the (optional)
translation of constructs between different database software and
versions.

The framework creates a barebone database (without any keys and
constraints) on the destination database, migrates all data to the
destination and finally adds the necessary database and table
constraints.

![](Db migration.png "Db migration.png")

Source
------

The sources and the completed theses can be downloaded from the svn
repository:

[`http://svn.semanticlab.net/svn/oss/thesis/migration/trunk`](http://svn.semanticlab.net/svn/oss/thesis/migration/trunk)

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

