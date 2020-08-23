---
title: Meta Data Extraction with Jhove
layout: single
categories: nlp
---

Jhove (Jstore/Havard Object Validation Environment) is a tool that
provides functions to perform format-specific identification,
validation and characterization of digital objects

Introduction
------------

-   Format identification is the process of determining the format to
    which a digital object conforms; in other words, it answers the
    question: "I have a digital object; what format is it?"


-   Format validation is the process of determining the level of
    compliance of a digital object to the specification for its
    purported format, e.g.: "I have an object purportedly of format F;
    is it?"


-   Format validation conformance is determined at two levels:
    well-formedness and validity.
    1. A digital object is well-formed if it meets the purely syntactic requirements for its format.
    2. An object is valid if it is well-formed and it meets additional semantic-level requirements.

For example, a TIFF object is well-formed if it starts with an 8 byte
header followed by a sequence of Image File Directories (IFDs), each
composed of a 2 byte entry count and a series of 8 byte tagged entries.
The object is valid if it meets certain additional semantic-level rules,
such as that an RGB file must have at least three sample values per
pixel.

-   Format characterization is the process of determining the
    format-specific significant properties of an object of a given
    format, e.g.: "I have an object of format F; what are its salient
    properties?"

The set of characteristics reported by JHOVE about a digital object is
known as the object's representation information, a concept introduced
by the Open Archival Information System (OAIS) reference model \[ISO/IEC
14721\]. The standard representation information reported by JHOVE
includes: file pathname or URI, last modification date, byte size,
format, format version, MIME type, format profiles, and optionally,
CRC32, MD5, and SHA-1 checksums \[CRC32, MD5, SHA-1\]. Additional media
type-specific representation information is consistent with the NISO
Z39.87 Data Dictionary for digital still images and the draft AES
metadata standard for digital audio.

Identification, validation, and characterization actions are frequently
necessary during routine operation of digital repositories and for
digital preservation activities. These actions are performed by modules.
The output from JHOVE is controlled by output handlers. JHOVE uses an
extensible plug-in architecture; it can be configured at the time of its
invocation to include whatever specific format modules and output
handlers that are desired. The initial release of JHOVE includes modules
for arbitrary byte streams, ASCII and UTF-8 encoded text, GIF, JPEG2000,
and JPEG, and TIFF images, AIFF and WAVE audio, PDF, HTML, and XML; and
text and XML output handlers.

Implementation
--------------

**1. Requirements**

The tool is written in Java. Therefore a Java Runtime Environment is
required for the proper operation of Jhove. Jhove should be able to be
run on any operating systems like UNIX or Windows.

**2. Installation**

Download the tool from <https://sourceforge.net/projects/jhove/files/> or install it with `apt-get install jhove`.


**3. Invoke Jhove**

The JHOVE command-line interface is invoked by the Bourne shell script
"jhove" (under Unix) or the DOS shell script "jhove.bat" (under Windows)
in the JHOVE installation directory. This script properly sets the Java
CLASSPATH and executes the Jhove class with the Java interpreter.

In the invocation syntax below, brackets \[ and \] enclose optional
arguments. In addition to the syntax specified in subsequent sections,
any of the following standard options can also be used:

`... [-c config] [-h handler] [-e encoding] [-o output] [-x sax-class] [-t directory] [-b buffer] [-l loglevel]...`

where

`-c config`        specifies the pathname of the configuration file;  
`-h handler`       specifies the output handler (defaults to TEXT, the standard Text handler);  
`-e encoding`      specifies the character encoding used by the output handler (defaults to UTF-8);  
`-o output`        specifies the output file pathname (defaults to standard output);  
`-x sax-class`     specifies the SAX parser class name (defaults to the J2SE 1.4 default);  
`-t directory`     specifies the pathname of the directory in which temporary files are created (defaults to the current working directory); and  
`-b buffer`        specifies the buffer size used for buffered I/O (defaults to the J2SE 1.4 default).  
`-l loglevel`      specifies the logging level (defaults to SEVERE).`

Note that the temporary directory and buffer size and logging level can
also be specified in the configuration file. 4.1 Format Identification

The following syntax is used to discover, or identify, the format of a
digital object.

```bash
  jhove ... [-ks] file-or-uri1 .. file-or-uriN
```

where the first ellipsis ... is a placeholder for any of the optional
standard options defined above.

The digital object(s) can be specified as a file or directory pathname
or as a URI. If a directory is specified, JHOVE will recursively walk
through the directory. The optional -s flag specified that the
identification should be performed solely on the basis of the internal
signatures (e.g., magic numbers) associated with the formats, rather
than by a complete parsing of the object. After the object's format has
been identified, its representation information is displayed. The
optional -k flag specifies that object checksum values should be
calculated and displayed as part of the representation information.

**Result**

The **result of a pdf file** will look like the following:

```
 ReportingModule: PDF-hul, Rel. 1.8 (2009-05-22)
 LastModified: 2013-04-29 16:04:17 CEST
 Size: 14138
 Format: PDF
 Version: 1.5
 Status: Well-Formed and valid
 SignatureMatches:
  PDF-hul
 MIMEtype: application/pdf
 PDFMetadata: 
  Objects: 14
  FreeObjects: 1
  IncrementalUpdates: 0
  DocumentCatalog: 
   PageLayout: SinglePage
   PageMode: UseNone
  Info: 
   Creator: cairo 1.12.14 (http://cairographics.org
   Producer: cairo 1.12.14 (http://cairographics.org
  Filters: 
   FilterPipeline: FlateDecode
  Fonts: 
   TrueType: 
    Font: 
     BaseFont: NHOAPS+DejaVuSans
     FontSubset: true
     FirstChar: 32
     LastChar: 121
     FontDescriptor: 
      FontName: NHOAPS+DejaVuSans
      Flags: Nonsymbolic
      FontBBox: -1020, -415, 1680, 1166
      FontFile2: true
     Encoding: WinAnsiEncoding
     ToUnicode: true
  Pages: 
   Page: 
    Sequence: 1
```

References
----------

<http://hul.harvard.edu/jhove/index.html>
