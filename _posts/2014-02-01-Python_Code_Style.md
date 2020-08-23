---
title: Python Code Style
alias: index.php/Python_Code_Style/
layout: single
categories: python
excerpt: Guidelines for writing efficient Python code.
---
{% include toc %}
Guidelines for writing efficient Python code.

Slow vs. Fast
=============

This section shall help in writing quicker and more elegant python code.
It therefore contrasts currently *recommended* practices with code
snippets from our projects and thesis.

Sorting dictionaries
--------------------

Using methods from the operator module often pays of.

``` python
items = [ (v,k) for k,v in token_dict.iteritems() ]
items.sort()
```

versus

``` python
from operator import itemgetter
items = sorted(token_dict.iteritems(), key=itemgetter(1), reverse=True)
```

Extracting Indices from Lists
-----------------------------

``` python
v = [ x for nr, x in enumerate(mylist) if nr in indices ]
```

versus

``` python
from operator import itemgetter
v = itemgetter(*indices)(mylist)
```

*Info:* itemgetter returns a scalar if only one index is requested,
otherwise a tuple of the requested values.


Detecting digits and alphanumerical data in strings
---------------------------------------------------

String functions are much quicker (but less powerful) than regular
expression matching.

``` python
import re
digit_pattern = re.compile('.*\d+.*')
alnum_pattern = re.compile('.*[a-zA-Z0-9_-].*')
#
if digit_pattern.match(s): return "digit"
if alpha_pattern.match(s): return "alnum"
```

versus

``` python
if s.isdigit(): return "digit"
if s.isalnum(): return "alnum"
```

Patterns
========

Programming patterns

Conditions and List Comprehensions
----------------------------------

``` python
  [ {cond} and {true} or {false} for x in lst ]
```

Example: replace all values, which are bigger than *v\_max* with
*v\_max*.

``` python
  [ x>v_max and v_max or x for x in lst ]
```

Decorators
----------

Example:

``` python
from eWRT import MemoryCached

@MemoryCached
def mySlowFunction(a):
  ...
```

-   [Python Decorators I - An
    Introduction](http://www.artima.com/weblogs/viewpost.jsp?thread=240808)
-   [Python Decorators II - Decorator
    Arguments](http://www.artima.com/weblogs/viewpost.jsp?thread=240845)

Python Hacks
============

-   IPython - An enhanced interactive Python shell & architecture for
    interactive parallel computing\] - eases the work in the python
    shell ([Homepage](http://ipython.scipy.org/moin/) | [ONLamp
    Article](http://www.onlamp.com/pub/a/python/2005/01/27/ipython.html)).

Python Unit Testing
===================

-   [Nose](http://somethingaboutorange.com/mrl/projects/nose/) extends
    python's default testing framework.
-   An excellent article on python testing frameworks: [Part
    1](http://www.ibm.com/developerworks/aix/library/au-pythontesting1/),
    [Part
    2](http://www.ibm.com/developerworks/aix/library/au-pythontesting2/),
    [Part
    3](http://www.ibm.com/developerworks/aix/library/au-pythontesting3/)

Default arguments
=================

-   Default arguments are a handy way to define default values, but keep
    in mind, that Python sets the value, when the function is definied.
    So setting the actual value directly could lead to
    unexpected sideeffects. For example if the first example is called
    several times without a value for delimiters, the append 'hello
    world" to the previous list and not to an empty one.

``` python
def function(delimiters=[]) 
    delimiters.append('hello world')
```

-   Correct way of using default arguments:

``` python
def function(delimiters=None) 
    if delimiters == None:
        delimiters = []
    delimiters.append('hello world')
```

Python Profiling
================

-   One of the best ways to profile your python code can be found
    [here](http://code.google.com/appengine/kb/commontasks.html#profiling).Please
    note that you need to install the `python-profiler` package to use
    the `pstats` module in Debian.

Example Code
============

The example code below demonstrates some techniques you should consider,
when programming in python.

``` python
#!/usr/bin/env python
# -----------------------------------------------------------------------
# http://www.python.org/dev/peps/pep-0290/


# dictionary creation using dict and a list of tuples(!)
myDict = dict(  [ (key,value) for key,value in values ] )

# multiple assignments
a=b=c=0
a,b = 2,3

# use str instead of the depreciated string class
import string
lowerCase = map(string.lower, upperCase)
lowerCase = map(str.lower, upperCase)



class MyExample

        # do not use setter/getter functions for instance variables
        # use the "property" function instead (if required)
        def __init__(self, vorname, nachname, extension):
                self.v   = vorname
                self.n   = nachname
                self.ext = extension


        def setValidExtension(self, extension):
                if not isinstance(extension, int):
                        raise "Extensions must be numeric!"
                else:
                        self.__extension=extension


        # use static methods, where they make sense(!)
        @staticmethod
        def aStaticMethod():
                pass
```

Recommended Resources
=====================

**Videos**

-   [Raymond Hettinger: "Transforming Code into Beautiful, Idiomatic
    Python"](http://www.youtube.com/watch?v=OSGv2VnC0go)

**Tutorials and Intros**

-   [Python Style Guide](http://www.python.org/dev/peps/pep-0008/)
-   [Python Performance
    Tips](http://wiki.python.org/moin/PythonSpeed/PerformanceTips)
-   [Python Coding
    Guidelines](http://jaynes.colorado.edu/PythonGuidelines.html)
-   [Python Idioms and
    Efficiency](http://jaynes.colorado.edu/PythonIdioms.html)
-   [Python Tips, Tricks, and Hacks](http://www.siafoo.net/article/52)
    at Siafoo (17 Aug 2010)

