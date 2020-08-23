---
title: Java - Python Interoperability
layout: single
categories: ["Python", "Java"]
---

Compressing/Decompressing data streams to be compatible with `java.util.zip.GZIPOutputStream`, `java.util.zip.GZIPInputStream` compressed data.

The following code snippets compress/decompress data compatible with the Java compression libraries:

```python
from StringIO import StringIO
from gzip import GzipFile

def _compress(data):
    outData = StringIO()
    d = GzipFile( mode="w", fileobj = outData )
    d.write(data)
    d.close()
    return outData.getvalue()

def _decompress(data):
    """ handles data returned from the tagger """
    d = GzipFile( fileobj = StringIO( data) ) 
    return d.read()
```
