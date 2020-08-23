---
title: REST/JSON Web Services
alias: index.php/REST/JSON_Web_Services/
layout: single
categories: ["Java", "REST"]
---

This page provides information on how to implement JSON/REST based Web
Services with Java.

Java
----

I recommend using [Jersey](http://jersey.java.net/) for Java REST
services.

### Tutorials

-   [REST with Java (JAX-RS) using Jersey -
    Tutorial](http://www.vogella.com/articles/REST/article.html) using
    Eclipse

### Important Notes

Please add the following snippet to the project's <code>web.xml<code> to
enable the automatic translation of more complex data types such as Map,
List or Objects.

``` xml
    <init-param>
        <param-name>com.sun.jersey.api.json.POJOMappingFeature</param-name>
        <param-value>true</param-value>
    </init-param>   
```

Python
------

Tutorials for querying JSON/REST Web Services from Python:

-   [Make Yahoo! Web Service REST calls with
    Python](http://developer.yahoo.com/python/python-rest.html)

