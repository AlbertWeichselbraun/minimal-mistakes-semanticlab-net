---
title: Pgperformer
permalink: thesis/Pgperformer/
layout: single
---

Introduction
============

Pgperformer is a postgreSQL Performance Measurement Tool specifically
designed to perform predefined testcases. It allows you to perform
generic and custom benchmarks. Apart from that one can define
custom-made test cases which adapt to an external database application
of your need. Pgperformer also offers simple export functions for later
analysis.

Features
========

**Generic benchmarks:**

-   SELECT test case
-   INSERT test case
-   UPDATE test case
-   VIEW test case
-   prepared statements test cases
-   stored procedures test cases

**Custom benchmarks:**

-   tsearch unranked test case
-   tsearch ranked test case
-   tsearch comparison (unranked vs. ranked)

**Export function:**

-   Export as EPS, CSV or JPG

Note that the JPG export feature only takes a snapshot of the current
graph visible over the GUI. If you want all data you will need to stick
with EPS or CSV.

Installation
============

In order to run pgperformer correctly you'll need to perform some
preliminary setup tasks.

Setting up your database environment
------------------------------------

Pgperformer uses four different databases, which are pointed to via the
connection.properties file.

1.  dbname - the main database for performing generic benchmarks
2.  statdbname - this is the database where statistical information is
    stored
3.  tsearchdbname - the database containing tsearch tables
4.  viewdbname - the database designed for the VIEW test cases

It is recommended to add PL/pgSQL as a language to each database in
order to prevent errors. To do so, issue the following command as
privileged postgres user via command prompt:

`createlang plpgsql $your_db$`

You only need to create the stated databases, except for the tsearch
database. In this case a filled tsearch database of the following format
is needed:

![](tsearch.png "tsearch.png")

Pgperformer takes care of preparing all other databases for use via the
menu called "Database". Use "Reset DB" in order to handle all needed
actions in one go. Once you're familiar with what to delete or create
you can use the provided menu entries.

Preparing your property files
-----------------------------

There are two main property files available:

-   connection.properties
-   simple.properties

"Connection.properties" is pretty self-explanatory whereas the file
"simple.properties" needs some specific attention for certain
properties:

1.  inserts - specifies the number of tuples per table
2.  insert - defines the iterations for all INSERT test cases
3.  select - defines the iterations for all SELECT test cases
4.  update - defines the iterations for all UPDATE test cases

Usage
=====

The following steps explain how to use pgperformer with a generic
benchmark:

1.  Start pgperformer
2.  Choose Database &gt; Reset DB (otherwise you'll get useless data
    mixed up with previous data)
3.  Choose a test case from the "Testcase" menu
4.  Click Setup and let pgperformer generate some workload data which
    will be stored in a corresponding file
5.  Click Connect and wait until all threads are connected and ready to
    run
6.  Finally click Run and start the benchmark
7.  When the benchmark is finished you can export the graph as EPS, CSV
    or as a JPG via the Chart menu

This is the standard procedure for a benchmark. If you choose a custom
benchmark you will not need to setup workload data but provide a search
term word list for the tsearch test case, or an SQL file for the
custom-made test case.  
  
Note that after completion of a test case all significant data is
written to a file called testcase.log located in your working directory
defined via the simple.properties file.

Screenshots
===========

Tsearch Testcase
----------------

![tsearch test case|600
px](Tsearch_screenshot.png "tsearch test case|600 px")

INSERT Testcase
---------------

![INSERT test case|600
px](INSERT_screenshot.png "INSERT test case|600 px")

Downloads
=========

You can checkout Pgperformer from subversion or download a compiled
version here.

Download
--------

The following starter shell script includes all required jar files in
order to take a quick look at pgperformer:

` `[`pgperformer.tar.bz2`](http://www.bascha.com/msf/pgperformer.tar.bz2)

Sources
-------

You can checkout the complete source for pgperformer from subversion:

`svn checkout `[`https://svn.semanticlab.net/svn/oss/thesis/pgperformer/trunk/`](https://svn.semanticlab.net/svn/oss/thesis/pgperformer/trunk/)
