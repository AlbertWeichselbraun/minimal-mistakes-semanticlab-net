---
title: Incremental Database Backup
permalink: thesis/Incremental_Database_Backup/
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

Currently providing up to data backups of these databases is a
challenging task. Due to their extend full database dumps are no longer
applicable and backups using LVM-snapshots and WAL logs are very
bandwidth, time and storage intensive, especially if transferred to
other hosts and storage media.

The goal of this thesis is to provide a scalable incremental backup
solution for large PostgreSQL databases, minimizing backup time, and
storage requirements.

Todo
----

The goals of this thesis are

1.  overview: use of databases in data mining, e-marketing and
    information retrieval
2.  literature and web research evaluating:
    -   database backup strategies (abstract techniques;
        platform independent)
    -   implementations of such strategies
        -   traditional approaches (database dumps, LVM-snapshots + WAL
            logs, etc.)
        -   open source solutions (mysql, postgresql, ...)
        -   techniques present in commercial solutions (e.g. oracle
            & co)

3.  requirement definition for an incremental backup
4.  design & implementation of an incremental backup tool for postgresql
5.  testing / evaluation
6.  outlook and conclusions

Literature
----------

-   [Postgresql Documentation - Backup and
    Restore](http://www.postgresql.org/docs/8.3/interactive/backup.html)
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

