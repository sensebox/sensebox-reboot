---
layout: post
title: "Offene Analyse von Umweltdaten"
date: 2018-01-12
author: "Daniel Nüst"
abstract: "Die offenen Daten der openSenseMap werden inzwischen in vielen weiteren Projekten genutzt"
thumbnail: /images/blog/2018-01-12-Offene-Forschung/2018-01_sensebox-binder-rstudio-screenshot.png
image1: /images/blog/2018-01-12-Offene-Forschung/2018-01_sensebox-binder-rstudio-screenshot.png
image2: https://media.giphy.com/media/l49JRjO65S0WQ1Kyk/giphy.gif
lang: de
---

_Dieser Artikel ist auf Englisch auf der [o2r website](http://o2r.info/2018/01/12/sensebox-binder/) veröffentlicht._

Der Beginn des neuen Jahres ist die Zeit der guten Vorsätze.
Für den Wissenschaftler [Daniel Nüst](http://nordholmen.net/) vom Forschungsprojekt "Offene Reproduzierbare Forschung" ([o2r](http://o2r.info)) bedeutete dies sich endlich mit seiner brandneuen _senseBox:home_ zu beschäftigen und eine kleine [reproduzierbare](https://de.wikipedia.org/wiki/Reproduzierbarkeit#Wissenschaft) Datenanalyse zu erstellen.
Dank der offenen Hardware von _senseBox_, den offenen Daten von der _openSenseMap_, und Freier Open Source Software ([FOSS](https://de.wikipedia.org/wiki/Free/Libre_Open_Source_Software)) konnte er eine transparente und nachvollziehbare Untersuchung über Feinstaubwerte zum Jahreswechsel in Münster erstellen.

Auf Basis von _[BinderHub](https://binderhub.readthedocs.io)_ kann jeder mit nur wenigen Klicks das gleiche virtuelle Labor in seinem Browser öffnen, welches für die ursprüngliche Untersuchung genutzt wurde.
Und alles ohne irgendwelche Software zu installieren.

Probiere es aus: [![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/nuest/sensebox-binder/master)

{% include image.html image=page.image2 %}

Natürlich kann der gesamte Quellcode auch auf dem eigenen Computer ausgeführt und inspiziert werden.
Er ist gemeinsam mit den Daten auf GitHub veröffentlicht: **[https://github.com/nuest/sensebox-binder/](https://github.com/nuest/sensebox-binder/)**

Die Analyse umfasst das Herunterladen der Messdaten mit [opensensmapR](), die Berechnung von statistischen Kennwerten, und verschiedene graphische Darstellungen auf Basis der Software _[R](https://de.wikipedia.org/wiki/R_(Programmiersprache))_.
Der folgende Screenshots zeigt die das Analyseskript und das erzeugte Dokument im Editor [RStudio](https://www.rstudio.com/products/rstudio/).

{% include image.html image=page.image1 %}

Wenn Du es nicht erwarten kannst, dann schau Dir unter [diesem Link](https://nuest.github.io/sensebox-binder/sensebox-analysis.html) die lesbare (aber nicht editierbare) fertige Version der Analyse an.

Und Daniel ist nicht alleine mit seinem Interesse an Feinstaubmessungen in der Neujahrsnacht.
[Johannes Friedrich](https://github.com/JohannesFriedrich/), Wissenschaftler an der [Universität Bayreuth](https://www.uni-bayreuth.de/de/index.html), hat mit seiner Software [senseBox](https://johannesfriedrich.github.io/senseBox/) die Daten von _über 400 senseBoxen_ heruntergeladen, visualisiert und bei Twitter für die Jahre [2018](https://twitter.com/johnsenfr/status/951568789526732800?s=21), [2019](https://twitter.com/johnsenfr/status/1080228102695985159?s=21) und [2020](https://twitter.com/johnsenfr/status/1345097543152242689?s=21) veröffentlicht.
