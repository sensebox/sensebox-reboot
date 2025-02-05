---
layout: project_page
date: 2025-02-05
author: Paula & Eduardo
title: "Füllstand Mülleimer"
abstract: "Nutze den ToF-Distanzsensor und das LoRa-Modul, um den Füllstand eines Mülleimers aus der Ferne anzeigen zu lassen."
thumbnail: /images/projects/Titelbild_Fuellstand-Muelleimer.png
image0: /images/projects/Fuellstand-Muelleimer/aufbau.png
image1: /images/projects/Fuellstand-Muelleimer/var_fuell-max.jpg
image2: /images/projects/Fuellstand-Muelleimer/berechnung-fuellstand.png
image3: /images/projects/Fuellstand-Muelleimer/led-initialisieren.png
image4: /images/projects/Fuellstand-Muelleimer/led-anzeige.png
image5: /images/projects/Fuellstand-Muelleimer/gesamter-code.png
image6: /images/projects/Fuellstand-Muelleimer/muelleimer.jpg

material:
  - 1-2x senseBox MCU S2
  - 1x LoRa-Bee
  - 1x QWIIC-Kabel
  - 1x ToF-Sensor
ide: blockly
version: ["edu-S2"]
lang: de
tags: ["Informatik","IoT","LoRa"]
difficult: mittel
---

Ziel dieses Projekts ist es, einen Füllstandssensor für Mülleimer zu bauen. Ganz im Sinne einer „Smart City“ kann so digital und von Weitem festgestellt werden, ob ein Mülleimer geleert werden muss.  
Damit das funktioniert, wird der Füllstand durch eine Messung der Distanz zum Deckel des Eimers bestimmt. Das setzen wir hier mit dem Time-of-Flight-Sensor (ToF) um, der präzise Distanzen messen kann. Eine RGB-LED soll je nach Füllstand in einer passenden Farbe (rot, gelb, grün) leuchten.
Die Messungen werden dann über den stromsparenden Funkstandard LoRa an das TheThingsNetwork (TTN) und  an die openSenseMap (OSM) gesendet, um die Füllstände übersichtlich auf einer Karte einsehen zu können. Ein Beispiel ist [dieser smarte Mülleimer in der Stadt Laer](https://opensensemap.org/explore/65f9865dad2eb20007aad333), der regelmäßig Daten an die openSenseMap sendet.

## Aufbau

Stecke das LoRa-Bee auf den XBEE-Steckplatz deiner senseBox, um eine Verbindung mit LoRa zu ermöglichen. Schließe den ToF-Sensor mit dem QWIIC-Kabel an einen der I2C/Wire-Steckplätze an. Infos zum ToF-Sensor findest du auf [Lernkarte](https://sensebox.de/de/lernkarten-s2) SB05.

{% include image.html image=page.image0 %}


## Programmierung

Wir wollen die senseBox mit dem ToF-Sensor unten am Deckel des Mülleimers anbringen. Durch die Entfernung vom Deckel zum nächsten Gegenstand (dem Müll) erfahren wir den ungefähren Füllstand.
Dafür brauchen wir verschiedene Variablen. (Du weißt noch nicht, was Variablen sind? Kein Problem! Schau Dir dazu die [Lernkarte](https://sensebox.de/de/lernkarten-s2) GI01 an.) Zuerst benötigen wir die Höhe des Mülleimers, da der Füllstand davon abhängt. So sind z.B. 30cm bei einem kleinen Mülleimer vielleicht schon voll, bei einem großen überhaupt nicht. Da sich die Höhe nicht laufend verändert, definieren wir die Variable bereits im Setup. Messe den Eimer vom Boden bis zur Unterseite des Deckels, also den gesamten Platz für Müll, in Zentimetern und schreibe den Wert in die Variable.

{% include image.html image=page.image1 %}


### Füllstand

Die zweite Variable bezeichnet die aktuelle Füllhöhe. Die definieren wir in der Endlosschleife, da sie sich ständig verändert. Wie können wir die Füllhöhe jetzt mit Hilfe der Distanz vom ToF-Sensor bestimmen? Wir ziehen von der maximalen Höhe einfach die Distanz ab. Denn wenn der Eimer zum Beispiel 90cm hoch ist und der Abstand vom Deckel zum Müll 40cm, bedeutet das, der Eimer ist ca. 50cm mit Müll gefüllt.
Allerdings sind Mülleimer oft unterschiedlich hoch und eine Angabe von 50cm Füllhöhe damit für eine schnelle Übersicht unpraktisch. Aus diesem Grund wollen wir die Füllhöhe in % angeben. So ist schnell klar: Ein Eimer ist zum Beispiel 85% voll und sollte deshalb schnell geleert werden. Eine Prozentangabe erhalten wir, indem wir den aktuellen Wert durch den maximalen Wert teilen.
Sinnvolle Werte für den Füllstand müssen zwischen 0 und der maximalen Höhe liegen. Um falsche Messungen, die zum Beispiel beim Leeren des Mülleimers entstehen könnten, zu verhindern, begrenzen wir die Werte zwischen 0 und der maximalen Füllhöhe. Um Strom zu sparen, lassen wir die senseBox mit Hilfe des Blocks „Intervall“ außerdem nur einmal pro Minute Werte messen (und senden).
Der Code bisher sieht dann also so aus:

{% include image.html image=page.image2 %}


### LED-Anzeige

Um direkt an der senseBox schon ein Signal zum Füllstand zu haben, nutzen wir die RGB-LED-Lampe. Dafür müssen wir sie zuallererst im Setup initialisieren.
{% include image.html image=page.image3 %}

Wenn der Mülleimer fast voll ist (z.B. ab 80%), soll sie rot leuchten, bei einem mittleren Füllstand (z.B. ab 50%) gelb und ansonsten grün. Dafür brauchen wir eine „wenn-dann“-Bedingung (Infos dazu findest du auf der [Lernkarte](https://sensebox.de/de/lernkarten-s2) GI02). Wie genau muss diese aussehen? Eine passende Möglichkeit sieht so aus:
{% include image.html image=page.image4 %}

Übertrage den Code auf Deine senseBox und probiere ihn aus! (Reduziere dafür am besten das Intervall, damit du nicht nur einmal pro Minute Feedback von der LED-Lampe erhälst. Denk daran, das Intervall anschließend wieder auf 60000 zu erhöhen.)


### LoRa & openSenseMap

Wir wollen die Daten stromsparend über LoRa versenden und anschließend übersichtlich auf einer Karte anzeigen lassen. Dafür nutzen wir das TheThingsNetwork (TTN), Cayenne LPP und die openSenseMap. Mit [dieser Anleitung](https://sensebox.de/projects/de/2021-02-19-ttnv3) könnt ihr euer Projekt korrekt einrichten.
*Hinweis: Nicht überall ist der LoRa-Empfang ausreichend. Überprüft  mit Hilfe der folgenden Karte, wie der Empfang in eurer Gegend ist: https://ttnmapper.org/heatmap/. Funktioniert das Projekt bei euch nicht, könnte es auch am Empfang liegen. Probiert es dann mit einer WLAN-Verbindung.*

Am Ende sollte der Code so aussehen:
{% include image.html image=page.image5 %}

Den Code findet ihr auch [hier](https://blockly.sensebox.de/gallery/67a3389236ebaf001930681d)


## Einsatz

Sobald du den Code auf die senseBox übertragen und ihn getestet hast, kann die Box an einen richtigen Mülleimer angebracht werden!
Damit keine Teile beschädigt oder verschmutzt werden, ist ein Gehäuse ratsam. Hierbei gibt es verschiedene Möglichkeiten. Zum Beispiel kannst du ein Gehäuse aus Karton oder Holz bauen, oder in einen Plastikbehälter (Tupperware oder ähnliches). Wenn du einen 3D-Drucker zur Verfügung hast, kannst du auch ein Gehäuse drucken. Dafür haben wir bereits Dateien erstellt, die du [hier](https://cloud.reedu.de/s/mbK5SPRZ2CzipFS) finden kannst.

Das kann dann zum Beispiel so aussehen:
{% include image.html image=page.image6 %}


## Ausblick

Das Projekt kann auf verschiedene Weise erweitert werden. 

Zum Beispiel können die Daten gespeichert und über einen längeren Zeitraum ausgewertet werden, um typische Verläufe festzustellen. Fragen könnten dabei unter anderem sein: An welchen Wochentagen und zu welchen Uhrzeiten wird am meisten Müll in den Eimer geworfen? Wie lange dauert es in der Regel, bis der Eimer voll wird und wann sollte er dementsprechend üblicherweise geleert werden?

Eine andere Möglichkeit ist, solche Füllstandssensoren an verschiedenen Mülleimern anzubringen, z.B. alle im Schulhof. Die Daten können dann auf der openSenseMap eingesehen und verglichen werden.

Welche Möglichkeiten fallen dir noch ein?