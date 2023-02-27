---
layout: project_page
date: 2019-12-18
author: Björn
title: "Die senseBox entscheidet"
abstract: "Du kannst dich nie entscheiden? Hier ist die Lösung!"
thumbnail: /images/projects/Entscheider/Entscheider_title.jpg
image0: /images/projects/Punktefang/Punktefang_Image00.png
image1: /images/projects/Entscheider/step_01.png
image2: /images/projects/Entscheider/step_02.png
image3: /images/projects/Entscheider/step_03.png
image4: /images/projects/Entscheider/step_04.png
imageSolution: /images/projects/Entscheider/final.png

material:
  - senseBox MCU
  - 1x OLED Display
  - 1x JST-JST Kabel
ide: blockly
version: ["edu", "mini v1"]
lang: de
tags: ["Informatik"]
difficult: mittel
---

# Die senseBox entscheidet {#head}

Du kannst dich nie entscheiden? Dann haben wir die Lösung für dein Problem! In diesem Projekt wird die senseBox zu einem Entscheider, dem du jede Frage stellen kannst und der für dich entscheidet, wenn du ihn schüttelst.

> Hinweis: Nicht jede Version der senseBox MCU ist mit einem Beschleunigungssensor ausgestattet. Prüfe mithife der [Docs](https://docs.sensebox.de/hardware/allgemein-sensebox-mcu/), ob dein Mikrocontroller den für dieses Projekt notwendigen Sensor besitzt.

## Aufbau

Der Aufbau für das Projekt ist einfach, du musst lediglich das Display mit Hilfe eines JST-JST-Kabels mit einem der fünf I2C Ports verbinden.

{% include image.html image=page.image0 %}

## Programmierung

### Schritt 1

Im ersten Schritt solltest du dir die Messwerte des Beschleunigungssensors auf dem Display anzeigen lassen.
Wenn du dir Messwerte auf dem Display anzeigen lassen möchtest, funktioniert dies immer gleich: Zuerst muss das Display im Setup() initialisiert werden und anschließend in der Endlosschleife() angegeben werden, WAS (Wert) auf dem Display, WIE (Schriftfarbe und Schriftgröße) und WO (Koordinaten) angezeigt werden soll. Bei Messwerten bietet es sich an, diese direkt mit einer Beschriftung zu versehen. Dies geht am einfachsten mit dem "Erstelle Text aus"-Block.
Für den Entscheider reicht es, die Beschleunigung in x-Richtung auszulesen.

{% include image.html image=page.image1 %}

### Schritt 2

Jetzt soll je nach Beschleunigung ein bestimmter Text auf dem Display angezeigt werden. Dazu musst du eine "Wenn-Dann"-Bedingung anlegen. Wenn die MCU geschüttelt wird, in unserem Beispiel also der gemessene Wert 1G überschritten wird, soll ein bestimmter Text angezeigt werden.
Den Block "wenn dann" findest du unter der Kategorie Logik. Nach der "Geschüttelt" Anzeige, solltest du eine Pause einfügen, damit genug Zeit bleibt, den Text zu lesen.

{% include image.html image=page.image2 %}

### Schritt 3

Bisher hast du einen Schüttelsensor programmiert. Im dritten Schritt soll aus diesem der Entscheider werden. Dazu musst du zuerst einen Zufallsgenerator programmieren, der angibt, ob deine Frage mit Ja oder Nein beantwortet werden soll. Dazu legst du eine Variable an und weist ihr einen ganzzahligen Zufallswert von 0 bis 1 zu.

{% include image.html image=page.image3 %}

Anschließend musst du weitere Bedingungen hinzufügen, die dafür sorgen, dass bei einer 0 als Zufallszahl mit 'Ja' und bei einer 1 mit 'Nein' geantwortet wird. Dazu musst du einen weiteren "wenn dann"-Block hinzufügen und ihn duch einen Klick auf das kleine Zahnrad oben links auf dem Block um ein "sonst wenn" erweitern.

{% include image.html image=page.image4 %}

Die beiden Bedingungen müssen nun ineinander verschachtelt werden, sodass wenn die MCU geschüttelt wird, eine Zufallszahl generiert und dementsprechend geantwortet wird.

## Gesamter Code

Du kannst dir die Lösung dieses Projektes direkt in Blockly [öffnen](https://blockly.sensebox.de/gallery/63bbd934d2853f0013b1df5f).
