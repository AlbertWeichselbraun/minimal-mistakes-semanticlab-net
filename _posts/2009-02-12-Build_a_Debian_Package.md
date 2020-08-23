---
title: Build a Debian Package
layout: single
categories: Sysadmin
---

In this tutorial we will create a Debian package for `lesslog`. If this
program is installed, it will copy two binaries and a readme-file in
`/usr/local/pgsql/bin/`. This will be done with this package.

1.  Create a directory for the package, e.g. `pglesslog` = package
    root-directory
2.  Create every folder in this directory, e.g. `usr/local/pgsql/bin`
3.  Move the binaryfiles where they ought to be stored,
    `usr/local/pgsql/bin`
4.  Create a folder called `DEBIAN` in the package root-directory
5.  Create a file named `control` in the folder `DEBIAN`
6.  This file stores the information for the package. One example how
    this file look like (For further details, see
    [1](http://www.debian.org/doc/manuals/maint-guide/ch-dreq.en.html#s-control)):

```
Package: pglesslog  
Source: pglesslog  
Version: 1.1  
Section: misc  
Priority: optional  
Architecture: amd64  
Depends: postgresql-8.3  
Maintainer: Heinz Lang <email@wu.ac.at>  
Description: lesslog - PostgreSQL logfile compressor  
 see /usr/local/pgsql/bin/README.lesslog
```

1.  Create the package. Run the following command one level above the
    package root-directory

    `dpkg -b pglesslog pglesslog_amd64.deb`
