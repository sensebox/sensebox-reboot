---
layout: project_page
date: 2025-04-07
author: Ben
title: "Flappy Bird"
abstract: "Nutze die Sensebox als Spiele konsole."
thumbnail: /images/projects/Titelbild_Klickzaehler.jpg
image0: 
image1: 
image2: 
image3: 

material:
  - senseBox MCU-S2
  - LED-Matrix
  - 1x Kabel

ide: blockly
version: ["edu", "mini v1"]
lang: de
tags: ["Informatik",  "Spiel"]
difficult: mittel
---

# Flappy Bird {#head}

In diesem Projekt wird das klassische Spiel Flappy bird programmiert

## Aufbau

Wichtig ist am anfang klarzustellen, dass mann eine LED-Matrix hat um das Spiel am ende zu spielen.
{% include image.html image=page.image0 %}

## Programmierung

### Schritt 1: "setup()"

Um die LED-Matrix zu verwenden muss mann erstmal unter "setup()" die LED-Matrix initialisieren. Dabei sollte mann auch schon mal die Variable für den Vogel auch in "setup()" aufschreiben, damit er in der mitte des spiel Feldes startet schreibt mann bei der Variable 4 auf da die LED-Matrix mur 8 pixel hat.

{% include image.html image=page.image1 %}

### Schritt 2: Bewegung vom Voge

Als erstes würde ich eine intervalle Erstellen, sodass das spiel langsamer läuft, und LED-Matrix löschen einfügen. Danach gehe auf "Logik" und nimm dir "wenn, dann", dann nimm dir den button sensor und stelle ihn auf ist gedrückt, sodass wenn der Button gedrückt is, dass er dann den Vogel nach oben bringt und wenn nicht nach unten.

{% include image.html image=page.image2 %}

### Schritt 3: Gegenstände

Erstelle 2 weitere Variablen "Xachse" und "Gegenstände". Schreibe bei der X achse irgend eine Zahlzwischen 3 und 6, bei den Gegenständen Schreibe 12 damit die Gegenstände nicht vor dem Spieler erstellt werden. nimm dann nochmal "wenn, dann", sodass die Variable wieder 0 wird und dann nochmal zufällig wird um nicht die ganze zeit den gleichen abstand zu bekommen und die X achse von den Gegenständen wieder zu 12 wird. Pack das alles in eine "wenn, dann" klammer die guckt ob die X achse = 0 ist.

{% include image.html image=page.image3 %}

### Schritt 4: Gegenstände Visualisiren

verwenigere die X achse immer um 1 sodass die immer näher zum Spieler kommt. der code von den "wenn, dann" klammern wird jetzt nützlich da mann für die wände die zufallszahl +2 bis +6 und -2 bis -6 rechnet und dort immer die pixel ausfüllt.

{% include image.html image=page.image3 %}

### Schritt 5: kollisionen

Erstelle eine weitere "wenn, dann" klammer, in dieser klammer kommt rein, dass wenn die X achse der gegenstände da ist wo auch der Vogel ist und der Vogel auch an einer der Wände ist, oder die Y achse des vogels runter geht, dann soll ein trauriges motive auf der LED-Matrix erscheinen.

{% include image.html image=page.image3 %}

## Gesamter Code

Den Blockly-Sketch findest du [hier]().

Damit FlappyBird nun auch mobil verwendet werden kann, empfiehlt es sich, die senseBox mithilfe einer Powerbank mit Strom zu versorgen.
Damit hast du das Projekt erfolgreich abgeschlossen und du kannst nun Flappy Bird Spielen ohne das du ein Handy benötigst.