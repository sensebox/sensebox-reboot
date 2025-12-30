---
layout: post
title: "Die Entstehung der senseBox:bike – von der Idee zum Produkt"
date: 2023-12-06
author: Gina
abstract: "Wie können Verkehrs- und Umweltdaten gemessen werden? Dazu wurde die senseBox:bike als Erweiterung der senseBox:familie entwickelt, um mobile Messwerte beim Radfahren zu erheben. Mehr zum Entstehungsprozess der senseBox:bike erfahrt ihr hier."
thumbnail: /images/blog/Bike-Box-6.png
image1: /images/blog/Bike-Box-1.jpg
image2: /images/blog/Bike-Box-2.jpg
image3: /images/blog/Bike-Box-3.jpg
image4: /images/blog/Bike-Box-4.jpg
image5: /images/blog/Bike-Box-5.jpg
image6: /images/blog/Bike-Box-6.png
image7: /images/blog/Bike-Box-7.png
image8: /images/blog/Bike-Box-8.png
image9: /images/blog/Bike-Box-9.png
image10: /images/blog/bike-app.png
lang: de
tag: News
---

Radfahren ist vielerorts ein riskantes Unterfangen: Radwege sind nicht vorhanden, sehr schmal oder uneben und die Anzahl an Verkehrsunfällen zwischen Fahrrad- und Autofahrenden ist erschreckend hoch. Wir haben uns daher die Frage gestellt, wie wir eine senseBox zur mobilen Umwelt- und Verkehrsdatenerhebung mit dem Fahrrad für Bürgerinnen und Bürger konzipieren können. Dabei wird die Fahrt per GPS getrackt und verkehrsrelevante Messwerte zu Erschütterungen, Seitenabständen, der Feinstaubbelastung, Brems- und Beschleunigungsvorgänge sowie Temperatur und Luftfeuchte erhoben und an die openSenseMap gesendet. Auf der Internetplattform können die Daten visualisiert, analysiert und mit anderen geteilt werden. Die so erfassten offenen Daten sollen dazu beitragen Schwachstellen und Verbesserungspotenziale im Stadtverkehr aufzudecken.

# Wie alles begann – ein Makeathon zum Prototyping

Welche Daten soll die senseBox für das Fahrrad erheben, um Aussagen zur Fahrradinfrastruktur treffen zu können und wie muss das Gehäuse gestaltet sein, damit es an verschiedenen Fahrradtypen befestigt werden kann und auch auf ruckeligen Straßen hält? Schnell war klar, dass wir diese Fragen nicht allein beantworten können. Also haben wir gemeinsam mit dem [Futurium Berlin](https://futurium.de/), der [Akademie der Bildenden Künste (ABK) Stuttgart](https://www.abk-stuttgart.de/index.html) und dem [c.lab der Hochschule München](https://creative-lab-hm.de/) bei einem Makeathon im Februar 2021 überlegt, wie die senseBox:bike aussehen soll und funktionieren könnte.

Hier die Ergebnisse der ersten Prototypen:

{% include image_gallery.html id="gallery1" image1=page.image1 image2=page.image2 image3=page.image3 %}

# Weiterentwicklung des Prototypen und Workshop mit Bürger:innen

Der Makeathon machte erste Herausforderungen deutlich, etwa die Stromversorgung oder die Unterbringung aller Komponenten auf möglichst minimalen Raum. Doch anhand der ersten Prototypen konnten wir das Gehäuse weiterentwickeln. Im Oktober 2021 war es dann so weit: Im Rahmen eines Workshops im Futurium Berlin bauten wir die senseBox:bike mit 30 Teilnehmenden zusammen und an die Fahrräder montiert. Anschließend radelten die Bürgerinnen und Bürger durch Berlin und erhoben während der Fahrt erste mobile Umweltdaten. Diese wurden an die openSenseMap übertragen und wurden im Futurium als Visualisierung in der Ausstellung präsentiert. Ein Video dazu findet ihr [hier](https://www.youtube.com/watch?v=mgcFX256XSk&t=163s). Nach einem Jahr wurden die Testmessungen bei einem [Open Lab Abend](https://futurium.de/de/open-lab-abend/open-lab-abend-6/open-lab-abend-2) im Futurium mit den Teilnehmenden sowie weiteren interessierten Bürger:innen evaluiert und diskutiert. Auf Basis des Feedbacks konnten finale Anpassungen des Gehäuses vorgenommen werden. Es wurde z.B. ein kleiner Ventilator für eine optimale Belüftung integriert und die senseBox MCU durch die [senseBox MCU mini](https://docs.sensebox.de/hardware/allgemein-sensebox-mcu-mini/) ersetzt, um deutlich Platz zu sparen.

{% include image_gallery.html id="gallery2" image1=page.image4 image2=page.image5 image3=page.image6 %}

# Outtakes: Die space:Box

Ursprünglich war die Idee, alles im 3D-Druck herzustellen. Die senseBox:bike im Rahmen der Bürger:innen-Werkstatt im Futurium war noch gewichtmäßig sehr schwer, weil unter anderem alle Sensorik und die MCU auf einer Eisenplatte befestigt waren. Deswegen war eins der größten Takeaways, dass die Box leichter sein muss und ausschließlich aus 3D-Druck-Teilen bestehen sollte. Wir haben also einen Entwurf für ein 3D-Druck-Gehäuse gemacht und 1:1 die Teile aus der Bike-Box des Futuriums integriert. Das neue Gehäuse sah allerdings eher wie ein kleines Raumschiff aus, sodass wir sie eher eine Space-Box als eine Bike-Box war. Daraufhin haben wir uns daran gemacht die MCU durch die MCU mini sowie die große Powerbank mit einem kleinen Laderegler + 2 LiPo Batterien und den SDS011 Feinstaubsensor mit dem wesentlich kleineren SPS30 zu ersetzen. Die finale senseBox:bike ist somit etwa 1,5 x kleiner und eutlich leichter als die Box, die für die Futurium-Workshops verwendet wurde. Außerdem hatten wir noch schnell gemerkt, dass das Gehäuse unbedingt eine Lüftung braucht, um für adäquate Temperatur- und Feinstaubwerte zu sorgen.

{% include image_gallery.html id="gallery3" image1=page.image7 image2=page.image8 image3=page.image9 %}

# Weiteres Feature: Die senseBox:bike App

Eine mobile Datenerhebung erfordert auch eine mobile Datenvisualisierung. Mit der senseBox:bike App können die Daten der senseBox:bike aufgezeichnet und an die openSenseMap übertragen werden. Darüber hinaus werden Live-Werte der senseBox:bike und die zurückgelegte Route angezeigt. Die App ist für [Android](https://play.google.com/store/apps/details?id=de.reedu.senseboxbike&gl=DE) und demnächst auch bei iOS verfügbar.

{% include image.html image=page.image10 %}

# Einsatz der senseBox:bike in der Schule

Mit dem Projekt „[Essen auf Rädern](https://essen.aufraedern.org/)“ soll die Verkehrswende hin zu mehr Radverkehr auch im Schulkontext beleuchtet werden. Dazu werden Jugendliche von fünf Essener Schulen mit unterschiedlichen sozialräumlichen Umfeld mit der senseBox:bike die Radverkehrsinfrastruktur in ihrem jeweiligen Schulviertel untersuchen und mit politischen Akteuren ihre auf Grundlage der selbst erhobenen Daten erstellten Konzepte und Vorschläge diskutieren.
Alle weiteren Informationen zur senseBox:bike findet ihr [hier](https://sensebox.de/de/products-bike).

Die senseBox:bike ist auch ab sofort bei uns im [Shop](https://sensebox.kaufen/pages/sensebox-bike) erhältlich!
