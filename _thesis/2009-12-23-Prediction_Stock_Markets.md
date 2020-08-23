---
title: Prediction Stock Markets
permalink: thesis/Prediction_Stock_Markets/
layout: single
---

Motivation
----------

Im Rahmen der Vorbereitung des SFB Artifical Economic Life entstand
1994-95 der WU Political Stockmarket (WUPS). Die Handelsplattform folgt
dem Marktdesign von Forsythe et al. und sieht auf dem Primärmakrt den
Kauf vollständiger Aktienportfolios zu einem Fixpreis sowie Continuous
Double Auction Märkte für die einzelnen Titel auf dem Sekundärmarkt vor.
Die Marktteilnehmer können so vor der Wahl die Titel ihren Erwartungen
entsprechend kaufen und verkaufen. Nach der Wahl werden die Aktien zum
Kurs des tatsächlich eingetretenen Wahlergebnisses ausgezahlt.

Heute werden vergleichbare Marktexperimente zur Vorhersage
verschiedenster Ereignisse/Ergebnisse eingesetzt. Der primäre
wirschaftliche Nutzen wird in der raschen und einfachen Aggregation von
Einschätzungen zukünftiger Ereignisse wie dem möglichen Zeitpunkt einer
Produkteinführung oder Verkaufszahlen in kommenden Perioden gesehen. Die
daraus resultierenden Marktdesigns beziehen sich nicht mehr nur auf eine
diskrete Anzahl von Aktien/Parteien sondern auch auf Zeitspannen und
Wertebereiche. (Gregory Goth, Betting on Ideas, Communications of the
ACM 2009/03)

Im Rahmen der Arbeit soll auf Basis des WUPS eine Architektur für einen
Vorhersagemarkt erarbeitet werden, die es Benutzern ermöglicht, nicht
nur Aufträge für einzelne Werte sondern auch für Wertebereiche auf
einfache Art und Weise zu erstellen.

Die Marktsoftware des WUPS besteht aus einem Webfrontend (Perl-CGI), das
über einen Linda Tuplespace mit dem parallelisierten Backend (C++)
kommuniziert. Das Backend besteht aus einem oder mehreren
Tradermanagern, einem Marktportfolio Manager und Sensalen für die
einzelnen Titel. Das System wird wenig verändert an der Universität
Karlsruhe unter dem Namen
[PSM](http://psm.em.uni-karlsruhe.de/index.php?refId=em) nach wie vor
betrieben.

Die Architektur des WUPS sieht die Verteilung des Marktes auf mehrere
Prozesse, die auf verschiedenen Rechnern im Netzwerk laufen können vor:

-   1 Webserver mit CGIs
-   1 Tuplespace Server
-   1 Marktportfolio Manager
-   N Sensale
-   1-N Trader Manager

Das ermöglicht zwar die Trennung von Frontend und Backend sowie die
parallele Bearbeitung von Handelsaufträgen für die einzelnen Titel und
das Marktportfolio, erschwert aber gleichzeitig die Erstellung und
Administration eines Marktes.

Durch die Portierung auf ein aktuelles Java Applikationsframework unter
der Verwendung einer Relationalen Datenbank (SQL) und des Java Message
Service (JMS) soll die Administration eines Marktes mit vielen
Titeln/Sensalen ermöglicht werden.

Das Marktdesign für einen Wertebereich wird durch die Definition der
Titel eines Marktes als einzelne Intervalle im Wertebereich des Marktes
abgebildet. Der Marktteilnehmer erhält als Portfolio den gesamten
Wertebereich. Abhängig von seinen Erwartungen und den aktuellen
Makrtpreisen behält oder verkauft er die einzelnen Intervalle. Über ein
AJAX GUI soll der Benutzer die Möglichkeit erhalten, Intervalle
auszuwählen und zu handeln.

Inhaltsverzeichnis
------------------

1.  Einleitung
2.  Prediction Markets
    1.  Einführung
    2.  Abgrenzung
    3.  Marktdesigns

3.  Martübersicht
4.  WU Prediction Stockmarket
    1.  Marktdesign(s)/Requirement Analysis
    2.  SW-Architektur
    3.  Implementation

5.  Ausblick

TODO
----

-   Literaturrecherche
    -   ACM
    -   IEEE
    -   Elsevier
    -   Springer
-   Aktuelle Marktexperimente
    -   Intrade
    -   Xpree
    -   University of Iowa: Iowa Elecronic Markets (IEM)
    -   Hollywood Stock Exchange (HSE)
-   Auswahl Plattform:
    -   Applikationsframework
    -   RDBMS
    -   JMS-Implementation
-   Definition von drei Marktexprimenten
    -   JA/NEIN - Eintrittswahrscheinlichkeit 0-100
    -   Wahl - Verteilung 0-100
    -   Wertebereich - Verteilung 0-100
-   GUI-Design
    -   Trader: Portfolio / Konto
    -   Auftrag erstellen
    -   Orderbuch / Kursübersicht

Literatur
---------

-   Gregory Goth 2009, Betting on Ideas. In Communcations of the ACM
    2009/03, ACM Press New York, NY, 13-15
-   James Suroviecky The Wisdom of Crowds: Why the Many Are Smarter Than
    the Few and How Collective Wisdom Shapes Business, Economies,
    Societies and Nations 2004, Doubleday
-   Buckley, Patrick and McGrath, Fergal 2009, Managing
    prediction markets. In SIGMIS-CPR '09: Proceedings of the special
    interest group on management information system's 47th annual
    conference on Computer personnel research, ACM, New York, NY, USA
-   Reeves, Daniel M. and Soule, Bethany M. and Kasturi, Tejaswi,
    Yootopia! SIGecom Exch. volume 6 number 2 2007 1-26, ACM, New York,
    NY, USA
-   Chen, Kay-Yut and Fine, Leslie R. and Huberman, Bernardo A.,
    Forecasting uncertain events with small groups. In EC '01:
    Proceedings of the 3rd ACM conference on Electronic Commerce, 2001
    ACM, New York, NY, USA
-   Feigenbaum, Joan and Parkes, David C. and Pennock, David M.,
    Computational challenges in e-commerce, Commun. ACM 2009/01 70-74,
    ACM, New York, NY, USA
-   Dimitrov, Stanko and Sami, Rahul, Non-myopic strategies in
    prediction markets. In EC '08: Proceedings of the 9th ACM conference
    on Electronic commerce 2008, 200-209, ACM, New York, NY, USA
-   Chen, Yiling and Fortnow, Lance and Nikolova, Evdokia and Pennock,
    David M., Betting on permutations. In EC '07: Proceedings of the 8th
    ACM conference on Electronic commerce 2007, 326-335, ACM, New York,
    NY, USA
-   Chen, Yiling and Chu, Chao-Hsien and Mullen, Tracy and Pennock,
    David M., Information markets vs. opinion pools: an
    empirical comparison. In EC '05: Proceedings of the 6th ACM
    conference on Electronic commerce 2005, 58-67, ACM, New York, NY,
    USA
-   Fortnow, Lance and Kilian, Joe and Pennock, David M. and Wellman,
    Michael P., Betting boolean-style: a framework for trading in
    securities based on logical formulas. In EC '03: Proceedings of the
    4th ACM conference on Electronic commerce 2003, 144-155, ACM, New
    York, NY, US
-   Feigenbaum, Joan and Fortnow, Lance and Pennock, David M. and Sami,
    Rahul, Computation in a distributed information market. In EC '03:
    Proceedings of the 4th ACM conference on Electronic commerce 2003,
    156-165, ACM, New York, NY, USA

