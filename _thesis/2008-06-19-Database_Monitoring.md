---
title: Database Monitoring
permalink: thesis/Database_Monitoring/
layout: single
---

Motivation
==========

webLyzard is a platform for the automated analysis of content,
navigational system and interface design of networked information
systems. Through structural and textual metrics, webLyzard determines
success factors and uncovers weaknesses of deployed system by comparing
large samples of Web sites across region and industry. Currently, the
project mirrors and analyses more than 7,000 sites in monthly, weekly,
or daily intervals (www.weblyzard.com).

Many current research projects, including AVALON, IDIOM, RAVEN, and the
Election 2008 Monitor depend on accurate sampling of relevant media
sides. Maintaining the sample's quality and identifying missing or false
data represents a challenging task. The goal of this thesis is to create
an SQL reporting and statistics tool, capable of visualizing and
identifying potentially invalid samples. The tool should automatically
warn the sample maintaining personnel if important sample-statistics
show significant deviations and aid them in diagnosing and repairing the
problem.

Todo
====

-   Generation of metrics based on the webLyzard mirror-data. (An
    example: There are website samples in the architecture that are
    mirrored and analysed weekly, which generates a lot of data in
    the database. On basis of this data the proposed system will
    generate (weekly) statistical data. So there will be created a
    history of weekly statistics, which are saved in the database. An
    easy example of statistics produced weekly would be "number of
    documents mirrored from website X". There will be a number of such
    \*benchmarks\* (see below))

<!-- -->

-   Visualization of the generated statistical data (benchmarks) over
    the time. The visualized data (charts) will help to get an
    immediate overview.
    -   all samples level (number of mirrors, analyser steps
        successfull/failed, number of documents mirrored, analysed)
    -   one sample level (benchmarks for the websites)
    -   one mirror level (detailed statistics for the mirror - number of
        stripped documents, average length, etc.)

<!-- -->

-   Creation of an interface aiding the webLyzard personnel in
    identifying and repairing invalid mirrors.

Required Qualifications
=======================

-   Good knowledge of SQL query syntax.

<!-- -->

-   Good analytical skills (development of metrics to identify
    mirror irregularities)

<!-- -->

-   Basic knowledge of PHP, Python, or Java.

<!-- -->

-   At least basic Unix/Linux skills

Support
=======

-   A view for the task will be created together with the student

<!-- -->

-   The database schema for the statistics table will be developed
    together with our programming team.

Starting Points
===============

-   [Postgresql
    Documentation](http://www.postgresql.org/docs/8.2/interactive/index.html)

