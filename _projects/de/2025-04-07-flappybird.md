---
layout: project_page
date: 2025-04-07
author: Ben
title: "Flappy Bird"
abstract: "Nutze die Sensebox als Spiele konsole."
thumbnail: /images/projects/Screenshot 2025-04-11 102045.png
image0: /images/projects/AufbauBild.jpeg
image1: /images/projects/FlappyBird/Bild2.svg
image2: /images/projects/FlappyBird/Bild3.svg
image3: /images/projects/FlappyBird/Bild4.svg
image3: /images/projects/FlappyBird/Bild5.svg

material:
  - senseBox MCU-S2
  - LED-Matrix
  - 1x qwiic Kabel

ide: blockly
version: ["edu", "mini v1"]
lang: de
tags: ["Informatik",  "Spiel"]
difficult: mittel
---

# Flappy Bird {#head}

In diesem Projekt programmieren wir das klassische Spiel **Flappy Bird**.

{% include image.html image=page.thumbnail %}

## Aufbau

Wichtig ist zunächst zu verstehen, dass du eine **LED-Matrix** benötigst, um das Spiel am Ende spielen zu können.  
{% include image.html image=page.image0 %}

## Programmierung

### Schritt 1: `setup()`

Um die LED-Matrix verwenden zu können, musst du sie zunächst in der Funktion `setup()` initialisieren.  
Außerdem solltest du hier schon die Variable für den **Vogel** anlegen. Damit dieser in der Mitte des Spielfelds startet, gibst du ihm den Wert **4**, da die LED-Matrix nur 8 Pixel hoch ist.

{% include image.html image=page.image0 %}

### Schritt 2: Bewegung des Vogels

Zuerst solltest du ein Intervall erstellen, damit das Spiel nicht zu schnell abläuft.  
Dann fügst du das Löschen der LED-Matrix ein.  
Wechsle nun zur Kategorie „Logik“ und nimm dir ein **„wenn, dann“**-Element.  
Füge einen Button-Sensor ein und prüfe, ob der Button gedrückt ist. Wenn ja, bewegt sich der Vogel nach **oben** – wenn nicht, nach **unten**.

{% include image.html image=page.image1 %}

### Schritt 3: Hindernisse

Erstelle zwei weitere Variablen: `XAchse` und `Gegenstände`.  
Setze `XAchse` auf einen beliebigen Wert zwischen **3 und 6**, und `Gegenstände` auf **12**, damit die Hindernisse nicht direkt vor dem Spieler erscheinen.  
Verwende wieder ein **„wenn, dann“**, um die Variable `Gegenstände` zurückzusetzen und eine neue Zufallszahl zu generieren. So entstehen die Hindernisse in unterschiedlichen Abständen.  
Setze `XAchse` dann wieder auf 12.  
Pack das Ganze in eine „wenn, dann“-Abfrage, die überprüft, ob `XAchse == 0` ist.

{% include image.html image=page.image2 %}

### Schritt 4: Hindernisse visualisieren

Verringere den Wert von `XAchse` regelmäßig um 1, sodass sich die Hindernisse auf den Spieler zu bewegen.  
Jetzt wird der Code aus Schritt 3 nützlich:  
Du kannst mit der Zufallszahl die oberen und unteren Wände berechnen – zum Beispiel durch `+2 bis +6` und `-2 bis -6`. In diesen Bereichen füllst du dann die entsprechenden Pixel.

{% include image.html image=page.image33 %}

### Schritt 5: Kollisionen

Erstelle eine weitere **„wenn, dann“**-Abfrage.  
Darin prüfst du, ob sich `XAchse` der Hindernisse an der gleichen Position wie der Vogel befindet **und** ob der Vogel mit einer Wand kollidiert oder die Y-Achse des Vogels außerhalb des Spielfelds liegt.  
Wenn das passiert, soll ein trauriges Motiv auf der LED-Matrix angezeigt werden.

{% include image.html image=page.image4 %}

## Gesamter Code

Den vollständigen Blockly-Sketch findest du [hier]().

Damit du Flappy Bird auch unterwegs spielen kannst, empfiehlt es sich, die **senseBox** mit einer Powerbank zu betreiben.  Herzlichen Glückwunsch – du hast das Projekt erfolgreich abgeschlossen und kannst jetzt **Flappy Bird** spielen, ganz ohne Smartphone!