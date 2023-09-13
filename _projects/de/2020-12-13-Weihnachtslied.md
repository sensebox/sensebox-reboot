---
layout: project_page
title: "Weihnachtslied"
date: 2020-12-13
author: Verena
abstract: "Nutze die senseBox als Instrument für ein Weihnachtslied"
thumbnail: /images/projects/Titelbild_Weihnachtslied.jpg
image0: /images/projects/Weihnachtslied/0.png
image1: /images/projects/Weihnachtslied/1.png
image2: /images/projects/Weihnachtslied/2.png
image3: /images/projects/Weihnachtslied/3.png
image4: /images/projects/Weihnachtslied/4.png

material:
  - senseBox MCU
  - 1x OLED-Display
  - 1x JST-JST-Kabel
  - 1x JST-Adapterkabel
  - 1x Piezo

ide: blockly
version: ["edu"]
lang: de
tags: ["Informatik", "Musik", "Weihnachten"]
difficult: leicht
---

<head><title>Weihnachtslied</title></head>

# Nutze die senseBox als Instrument für ein Weihnachtslied

Am dritten Advent betrachten wir die senseBox aus einer neuen Perspektive und nutzen ihre musikalische Seite. Dafür verwenden wir die Tonausgabe des Piezos. Du kannst dieses Projekt auch in ein Spiel umwandeln, indem du nur die ersten Takte eines Weihnachtsliedes programmierst und dein Gegebüber erraten muss, um welches Lied es sich handelt. Auf dem Display ist dann die Lösung zu sehen.

## Aufbau

Zuerst verbindest du das Display mit dem JST-JST-Kabel. Dies schließt du an einem der fünf I2C/Wire-Anschlüssen deiner senseBox MCU an. Für den Piezo verwendest du das JST-Adapterkabel und verbindest das kürzere Beinchen mit dem Minuspol (schwarzes Kabel) und das längere Beinchen mit einem digitalen Pin (grünes oder gelbes Kabel). Du kannst einen Widerstand vorschalten, dies ist aber nicht nötig und führt nur dazu, dass der Piezo leiser wird.

{% include image.html image=page.image0 %}

## Programmierung

Das Ziel der Programmierung ist es, dass die senseBox ein Weihnachtslied abspielt. Wir haben uns für das Lied 'Kling Glöckchen' entschieden, du kannst aber auch jedes andere Lied verwenden, falls dir dafür die Noten vorliegen. Da wir dem Piezo die Befehle in Hertz geben, müssen wir die uns bekannten Noten zuerst umschreiben. Die folgende Tabelle gibt dir einen Überblick über die jeweilige Frequenz des Tons.

{% include image.html image=page.image1 %}

### Schritt 1: Anzeige auf dem Display

Fall du den Namen des Weihnachtslieds auf dem Display anzeigen lassen möchtest, solltest du dies zuerst im Setup() initialisieren. In der Endlosschliefe verwendest du dann die Blöcke 'Zeige auf dem Display' und 'Schreibe Test/ Zahl'. Hier kannst du die Schriftgröße und Position der Anzeige anpassen und bei 'Wert' mithilfe eines Textbausteins einen beliebigen Text eingeben.

{% include image.html image=page.image2 %}

### Schritt 2: Töne erstellen

Im nächsten Schritt solltest du dir Noten für ein Weihnachtslied raussuchen, beispielsweise aus dem Internet. Die Noten, die du dort siehst, müssen dann in Hertz umgeformt werden, sodass du die jeweilige Frequenz in Blockly eingeben kannst. Diese Eingabe erfolgt im Block 'Spiele Ton an...' aus der Kategorie 'Audio'. Hier solltest du darauf achten, dass der richtige Pin ausgewählt ist. Diesen kannst du auf der senseBox MCU am Steckplatz des JST-Adapterkabels ablesen. Für jeden Ton benötigst du einen neuen Block. Die erste Zeile des Lieds 'Kling Glöckchen' enthält die folgende Tonabfolge: g-e-f-g-a-g-a-g-f-d-g-e. Mithilfe der obigen Tabelle kannst du die passende Frequenz ermitteln.

{% include image.html image=page.image3 %}

### Schritt 3: Melodie anpassen

Überträgtst du den bisherigen Programmcode auf deine senseBox, so wird dir auffallen, dass das Lied noch nicht zu erkennen ist. Der Grund dafür liegt in der fehlenden Melodie, welche du nun mithilfe des Notenwerts generieren musst. Dafür verwendest du die 'Warte'-Blöcke aus der Kategorie 'Zeit'. Je länger eine Note ist, desto länger muss folglich auch die Wartezeit sein, bis der nächste Ton abgespielt wird. In diesem Beispiel wurden 2000 Millisekunden für einen Takt gewählt und die Wartezeit auf die jeweilige Notenlänge angepasst. Es ergibt sich also folgendes Schema: Ganze Note - 2000 ms; Halbe Note - 1000 ms; Viertelnote - 500 ms; Achtelnote - 250 ms; usw. Möchtest du eine Zeile des Lieds wiederholen, so bietet es sich an, eine Schleife zu verwenden, mit der du die Anzahl der Wiederholungen anpasst.

{% include image.html image=page.image4 %}


## Gesamter Code

Den gesamten Blockly-Sketch findest du [hier](https://blockly.sensebox.de/gallery/63b68de4d2853f0013b1d9ad).

## Weiterführende Ideen

Du siehst hier nur einen kleinen Ausschnitss eines Weihnachtslieds, den du aber selbstverständlich erweitern und optimieren kannst. Zusätzlich könntest du dir auch die jeweilige Note oder den Text des Weihnachtslieds auf dem Display anzeigen lassen. Deiner Kreativität sind also keine Grenzen gesetzt.
In diesem Sinne wünschen wir dir einen schönen und musikalischen dritten Advent!
