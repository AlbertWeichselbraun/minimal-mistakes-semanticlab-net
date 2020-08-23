---
title: Generic Relation Extraction
permalink: thesis/Generic_Relation_Extraction/
layout: single
---

webLyzard is a platform for the automated analysis of content,
navigational system and interface design of networked information
systems. Through structural and textual metrics, webLyzard determines
success factors and uncovers weaknesses of deployed system by comparing
large samples of Web sites across region and industry. Currently, the
project mirrors and analyses more 500,000 sites per week.

Many current research projects, such as [IDIOM](http://www.idiom.at),
[RAVEN](http://www.modul.ac.at/nmt/raven), and the [Election 2008
Monitor](http://www.ecoresearch.net/election2008) depend on applying
state of the art pre-processing, statistical, and natural language
detection methods to be applied to this corpus.

Processing such amounts of documents requires appropriate techniques
which scale well even under Web-scale conditions ([Cafarella et
al.](#cafarella2008 "wikilink")). Open relation extraction approaches
such as the one introduced in [Banko and
Etzioni](#Banko:2008 "wikilink") address this issue.

The goals of this thesis are to

1.  investigate the state of the art in Web-scale relation extraction
    techniques,
2.  implement a research prototype in Java or Python:
    -   capable of extracting relations from documents in linear time.
    -   domain independent

Structure
---------

1.  introduction and problem definition
2.  theoretical considerations
3.  state of the art
4.  implementation
    1.  requirement analysis
    2.  system description
    3.  java or python prototype

5.  evaluation
6.  outlook and conclusions

Literature
----------

**Essential Literature**

-   <cite id="Banko:2008">\[Banko:2008\] Banko, Michele and Etzioni,
    Oren (2008). *The Tradeoffs Between Open and Traditional Relation
    Extraction*, Proceedings of ACL-08: HLT, Association for
    Computational Linguistics, pages 28--36</cite>
-   <cite id="cafarella2008">\[cafarella2008\] Cafarella, Michael J.,
    Madhavan, Jayant and Halevy, Alon (2008). *Web-scale extraction of
    structured data*, SIGMOD Rec., ACM, pages 55--61, 37(4)</cite>
-   <cite id="zelenko2003">\[zelenko2003\] Zelenko, Dmitry, Aone,
    Chinatsu and Richardella, Anthony (2003). *Kernel methods for
    relation extraction*, J. Mach. Learn. Res., MIT Press, pages
    1083--1106</cite>
-   <cite id="Nicolae2007">\[Nicolae2007\] Nicolae, Cristina, Nicolae,
    Gabriel and Harabagiu, Sanda (2007). *UTD-HLT-CG: Semantic
    Architecture for Metonymy Resolution and Classification of Nominal
    Relations*, Proceedings of the Fourth International Workshop on
    Semantic Evaluations (SemEval-2007), Association for Computational
    Linguistics, pages 454--459</cite>

**Related Literature**

-   <cite id="cimiano2007">\[cimiano2007\] Cimiano, Philipp and
    Wenderoth, Johanna (2007). *Automatic Acquisition of Ranked Qualia
    Structures from the Web*, ACL</cite>
-   <cite id="zhu2009">\[zhu2009\] Zhu, Jun, Nie, Zaiqing, Liu,
    Xiaojiang, Zhang, Bo and Wen, Ji-Rong (2009). *StatSnowball: a
    statistical approach to extracting entity relationships*, WWW '09:
    Proceedings of the 18th international conference on World wide web,
    ISBN: 978-1-60558-487-4, ACM, pages 101--110</cite>

