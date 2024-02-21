---
layout: project_page
title: "Dein erster Sketch"
date: 2024-01-10
author: Verena
abstract: "Lasse mit deinem ersten Sketch die LED auf der senseBox MCU-S2 blinken"
thumbnail: /images/projects/ErsterSketch_Titel.png
image0: /images/projects/ErsterSketch_S2/0.png
image1: /images/projects/ErsterSketch_S2/1.png
image2: /images/projects/ErsterSketch_S2/2.png

material:
  - senseBox MCU-S2
ide: blockly
lang: de
version: ["edu-S2]
tags: ["Erste Schritte", "Informatik"]
difficult: leicht
---

# Erste Schritte: Dein erster Sketch

Ziel dieses Projektes ist es, Blockly kennenzulernen und mit einem ersten Sketch die RGB-LED auf der senseBox MCU-S2 blinken zu lassen.

## Programmierung

### Schritt 1: Setup und Endlosschleife

Dieser Block wird direkt beim Starten der Oberfläche geladen und sollte immer verwendet werden. Die zwei Basisfunktionen `Setup()` und `Endlosschleife()` werden immer benötigt, um ein funtkionsfähiges Programm zu schreiben.
Alle Blöcke, die innerhalb der `Setup()` Funktion stehen, werden nur zu Beginn des Programms einmal ausgeführt. In dieser Funktion wird zum Beispiel das Display initialsiert oder die WLAN Verbindung hergestellt. Alle Blöcke, die innerhalb der `Endlosschleife()` stehen, werden durchgehend ausgeführt. Der Mikrocontroller führt hierbei alle Blöcke immer wieder von oben nach unten hin aus. In der `Endlosschleife` werden zum Beispiel die Sensoren ausgelesen oder auch die Messwerte auf die SD-Karte gespeichert oder übertragen.

{% include image.html image=page.image0 %}

### Schritt 2: Die eingebaute LED einschalten

Um die eingebaute LED anzuschalten, musst du die RGB im Setup initialisieren. 
In der Endlosschleife kannst du die RGB-LED dann in einer beliebigen Farbe leuchten lassen. RGB steht nämlich für die Farben rot, grün und blau, welche die Grundlage für bestimmte Mischfarben bilden. Du kannst bei Frabe folglich einen beliebigen Farbblock aus der Kategorie 'LED' auswählen.
In der Informatik beginnt das Zählen bei null, weshalb du die angegebene Position unverändert lassen kannst.

{% include image.html image=page.image1 %}


### Schritt 3: Die eingebaute LED blinken lassen

Um die eingebaute RGB-LED blinken zu lassen, ist es nötig, sie mit einem weiteren 'Setze RGB-LED an' Block wieder auszuschalten. Zusätzlich muss nach dem An- sowie Ausschalten eine Pause eingefügt werden, damit das Blinken überhaupt sichtbar ist. Den `Warte` Block findest du in der Kategorie `Zeit`.

{% include image.html image=page.image2 %}

<div class="panel panel-info">
  <div class="panel-heading">
1000 Millisekunden sind 1 Sekunde
  </div>
  <div class="panel-body">
  </div>
</div>

## Gesamter Code

Den fertigen Blockly-Code findest du [hier](https://blockly.sensebox.de/gallery/5fd08ffb64d32d0011cab222). 