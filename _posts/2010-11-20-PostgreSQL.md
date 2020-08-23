---
title: PostgreSQL
layout: single
categories: postgres
---

Large Scale Deployments
=======================

If you use big amounts of memory (&gt;4 GB) for shared buffer's you
might run into this error message:

```
 Starting PostgreSQL 8.3 database server: main  
 The PostgreSQL server failed to start. Please check the log output:  
 2008-08-01 07:23:19 BST FATAL:  could not create shared memory segment: No space left on device  
 2008-08-01 07:23:19 BST DETAIL:  Failed system call was shmget(key=5432001, size=8789024768, 03600).  
 2008-08-01 07:23:19 BST HINT:  This error does *not* mean that you have run out of disk space. It occurs either if all available shared memory IDs have    
                                been taken, in which case you need to raise the SHMMNI parameter in your kernel, or because the system's overall limit for   
                                shared memory has been reached.  If you cannot increase the shared memory limit, reduce PostgreSQL's shared memory request   
                                (currently 8789024768 bytes), by reducing its shared_buffers parameter (currently 1048576) and/or its max_connections   
                                parameter (currently 83).  
                                The PostgreSQL documentation contains more information about shared memory configuration.
```

In this case it is not sufficient to increase the maximum shared memory
size (*shmmax*), but you'll probably also have to increase the size of
the maximum number of shared memory segments system-wide (*shmmni*) and
the total number of shared memory pages available (*shmall*). The
following setting worked for our configuration (shared\_buffers=16GB).

```bash
 echo 175726755840 >/proc/sys/kernel/shmmax  
 echo 655360 >/proc/sys/kernel/shmmni  
 echo 20971520 >/proc/sys/kernel/shmall
```

Filesystem Related
==================

- [Linux IO Scheduler](http://www.wlug.org.nz/LinuxIoScheduler) -
  suggests the deadline IO scheduler for database systems and systems
  supporting TCQ.
- Optimize Read-ahead:

` blockdev --setra 4096 /dev/sda`

Performance
===========

Table Design and SQL Commands
-----------------------------

-   Use Indices
-   Cluster your data to improve the retrieval performance
    -   [CLUSTER documentation](http://www.postgresql.org/docs/8.4/interactive/sql-cluster.html)
    -   Article: [How does CLUSTER improve index performance](http://www.postgresonline.com/journal/index.php?/archives/10-How-does-CLUSTER-ON-improve-index-performance.html)
    -   [Database clustering using pg\_reorg](http://www.kennygorman.com/wordpress/?p=334)
        -   introduction to database clustering
        -   how to locate poorly clustered tables
        -   how to cluster your data only
    -   [pg\_reorg](http://pgfoundry.org/projects/reorg/) - clusters
        tables online

Tools and Settings
------------------

This is a (growing) list of techniques and tools used to debug, measure
and improve PostgreSQL's performance.

-   Increase the statistic daemon's memory
-   [pgFouine](http://pgfouine.projects.postgresql.org/) - analyse
    PostgreSQL logs
-   How to [determine *unused* and potentially *missing* database
    indexes](http://radek.cc/2009/09/05/psqlrc-tricks-indexes/).

IO Schedulers
-------------

The goal here is to see which of the IO schedulers (deadline, cfq)
performs better with pgbench. First you need to initialize the pgbench
tables with data, and do a vacuum. "-s 100" means 10,000,000 rows in the
"accounts" table.

`/usr/lib/postgresql/8.3/bin/pgbench -i weblyzard -s 100`

Afterwards a python script was used to switch between to two schedulers,
and run pgbench for a number of times alternativly for the two
schedulers. The following configuration options for pgbech were used
(scale factor 10, 10 concurrent clients,300000 transactions):

`-s10 -c10 -v -t300000`

So a call might look like:

`echo "cfg" > /sys/block/sda/queue/scheduler`  
`su postgres -c "/usr/lib/postgresql/8.3/bin/pgbench -s10 -c10 -v -t300000 dbname"`

For multiple iterations of the test case no real winner could be seen,
both schedulers perform more or less equally well.

tps results:

`tps = 2602 (min) to 2801 (max) --- for cfq`  
`tps = 2639 (min) to 2810.(max) --- for deadline`

Forcing a rewriting of a table
------------------------------

-   Starting from PostgreSQL 9.0 a function exists to invoke the
    rewriting of an existing table. This for example could be necessary
    after lots of data have been moved, deleted ... within a table. In
    older version this is done by altering the type of an existing
    column to the type it already has:

`ALTER TABLE ONLY table_name ALTER column_name SET DATA TYPE column_type; `


Upgrading
=========

-   [Migrating PostgreSQL with
    Bucardo](http://blog.endpoint.com/2009/09/migrating-postgres-with-bucardo-4.html) -
    Use asynchronous PostgreSQL replication to update between PostgreSQL
    versions
-   [Speeding up the PostgreSQL dump/restore
    process](http://www.depesz.com/index.php/2009/09/19/speeding-up-dumprestore-process/) -
    this article covers parallel dumps (manual) and parallel restores
    (build in support since PostgreSQL 8.4); Hint: use the PostgreSQL
    common format for dumps and restore (`pg_dump` `-Fc` `-a`).

Interesting PL/PgSQL Code Snippets
==================================

-   [Key
    Tree](http://people.planetpostgresql.org/dfetter/index.php?/archives/27-Key-Tree.html) -
    a recursive function which returns a list of all tables have foreign
    keys to a given table; requires PostgreSQL 8.4
-   Andrew Dunstan on the [use of windowing
    functions](http://people.planetpostgresql.org/andrew/index.php?/archives/42-More-fun-with-windowing-avoiding-expensive-function-calls.html)

Resources
=========

-   [PostgreSQL Wiki](http://www.postgresqldocs.org/wiki)
-   [Linux Filesystem
    Performance](http://jamesthornton.com/hotlist/linux-filesystems/)
-   [Researching Postgresql
    Performance](http://www.pgcon.org/2008/schedule/attachments/81_researching_postgresql.pdf) -
    tests the performance of different kernel parameters, file systems
    and postgresql settings.
-   [PostgreSQL 8.4devel
    Documentation](http://developer.postgresql.org/pgdocs/postgres/pgbench.html)

The "Good Practices" section is of particular interest here.

-   [Postgres OnLine](http://www.postgresonline.com/) - An in-depth
    Exploration of the PostgreSQL Open Source Database

