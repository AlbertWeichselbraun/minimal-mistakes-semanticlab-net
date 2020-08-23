---
title: Geo Tagger Evaluation Framework
alias: index.php/Geo_Tagger_Evaluation_Framework/
layout: single
categories: nlp
---

The *Geo Tagger Evaluation Framework* (geoTEF) provides an open
framework for evaluating Geo-Taggers. The following graph shows the
conceptual evaluation framework:

![](/assets/posts/Geo_evaluation_framework.png "Geo evaluation framework")

Currently only a proof-of-concept scoring based on
*HierarchyLocationReference* and *SetLocationReference* are implemented;
More complex implementations of the *ILocationReference* interface
supporting OntologyBasedScoring are under development.

Software
========

This framework is used to evalute geo-taggers using utility scoring. Please refer to the corresponding [paper](#weichselbraun2009) for a
detailed description of the underlying concepts and ideas.

Download
--------

A tar file containing the geoTEF framework, the extensible Web Retrieval
Toolkit, data files, and cache files required to run the experiments.

 [geoTEF-0.1.tar.bz2](https://weichselbraun.net/data/geoTEF-0.1.tar.bz2){: .btn}

Code Repository
---------------

The most recent code is available at github.

`git clone https://github.com/AlbertWeichselbraun/geoTEF.git`

Installation Instructions
-------------------------

Dependencies:

-   [Python2.4](http://www.python.org) or higher
-   [Gnuplot](http://www.gnuplot.info/)
-   The [extensible Web Retrieval Toolkit (eWRT)](https://github.com/weblyzard/ewrt) is required
    to run this program (only necessary if you use the most current
    version from subversion).

**Installation:**

-   download & unpack the software
-   adjust env.sh to reflect your installation settings and set the
    environment variables using

`   source env.sh`

-   copy `geoTEFconfig.py-sample.py` to `geoTEFconfig.py`. If you plan
    to evaluate your own geo-tagger's you will have to set up the
    gazatteer database and adjust the database settings in the
    configuration file accordingly.
-   ./evaluation.py starts the evaluation.

**Database set up**

-   Download the gazetteer database dump from [here](https://weichselbraun.net/data/geoTEF_gazetteer_20090207.sql.bz2).
-   Dump it into your database using

` bzcat geoTEF_gazetteer_20090207.sql.bz2 |psql dbname`


Evaluation Data Sets
====================

We currently use the [Reuters corpus](#reuters) to perform
the evaluations. For legal reasons we cannot publish this dataset on the
project page, but have instead included comma separated text files with
the tagging results (which are used for the evaluation) in the
frameworks `/data` directory.

The **gazetteer** used by the evaluation framework uses the following
database schema:

![](/assets/posts/GeoLyzard_db_schema.png "GeoLyzard DB schema.png")

A compressed postgres data dump of the gazetteer is available
[here](https://weichselbraun.net/data/geoTEF_gazetteer_20090207.sql.bz2).

Remarks
=======

The Framework implements caching using the [extensible Web Retrieval
Toolkit](https://github.com/weblyzard/ewrt).

Bibliography
============

- Reuters. <a name="reuters">Reuters Corpus,</a> Volume 1, English language, 1996-08-20 to 1997-08-19
- Weichselbraun, Albert. (2009). <a name="weichselbraun2009">[A Utility Centered Approach for Evaluating and Optimizing Geo-Tagging](http://eprints.weblyzard.com/13/1/geo.pdf)</a>. First International Conference on Knowledge Discovery and Information Retrieval (KDIR 2009), 134-139, Madeira, Portugal

