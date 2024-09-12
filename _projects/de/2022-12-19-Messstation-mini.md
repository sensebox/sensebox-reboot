---
layout: project_page
title: "Mini-Umweltmessstation"
date: 2022-12-19
author: Verena
abstract: "Eine Messstation mit der senseBox:mini, die die Messwerte auf dem Display anzeigt und auf der SD-Karte speichert."
thumbnail:  /images/projects/Mini-Umweltmessstation.png
image0: /images/projects/Messstation-mini/0.png
image1: /images/projects/Messstation-mini/1.png
image2: /images/projects/Messstation-mini/2.png
image3: /images/projects/Messstation-mini/3.png
image4: /images/projects/Messstation-mini/4.png
image5: /images/projects/Messstation-mini/5.png
image6: /images/projects/Messstation-mini/6.png
material:
    - senseBox MCU mini
    - OLED Display
    - Umweltsensor BME680
    - Mikro SD-Karte
    - 2x JST-Qwicc-Kabel
ide: blockly
version: ["mini v2"]   
lang: de
tags: ["Informatik", "Geographie"]
difficult: leicht
---

In diesem Projekt wird die senseBox:mini verwendet, um eine Umweltmessstation zu bauen. Mithilfe des Umweltsensors werden im ersten Schritt Messwerte, wie Temperatur, Luftdruck oder Luftfeuchtigkeit, auf dem Display angezeigt und im zweiten Schritt auf der SD-Karte gespeichert. Damit können die genannten Umweltphänome über einen längeren Zeitraum erhoben und anschließend analysiert werden. 

## Aufbau
Stecke die Mikro SD-Karte in den dafür vorgesehenen SD-Kartenslot. Das OLED Display und der Umweltsensor werden mit jeweils einem Kabel an einen der zwei I2C Anschlüsse angeschlossen. 

{% include block.html image=page.image0 %}

{% include block.html image=page.image1 %}

## Programmierung

Die Programmierung der Messstation wird in [Blockly](https://blockly.sensebox.de) durchgeführt. Wähle dafür die senseBox MCU mini als Board aus. 
Im ersten Schritt werden die Messwerte ausgelesen und auf dem Display angezeigt. Danach kannst du das Projekt beenden oder mit der Speicherunmg der Umweltphänomene auf der SD-Karte fortfahren.

### Schritt 1: Die Anzeige eines Umwletphänomens auf dem Display 

Initialisiere das Display im __Setup()__ und füge den Block __Zeige auf dem Display__ in die Endlosschleife ein. Mit dem Block __Schreibe Text/Zahl__ kannst du die jeweiligen Messwerte auf dem Display anzeigen lassen. Füge dafür bei 'Wert' den Block __Erstelle Text aus__ aus der Kategorie 'Text' ein. Mithilfe eines Textfeldes kannst du dann die Beschriftung zum jeweiligen Sensorwert hinzufügen. Letzterer wird dir angezeigt, indem du den __Umweltsensor (BME680)__ als Block einfügst und das entsprechende Umweltphänomen auswählst. Damit alle Messwerte dauerhaft aktualisiert werden, füge den Block __Display löschen__ am Ende deines Programms hinzu. 

{% include block.html image=page.image2 %}


### Schritt 2: Anzeige weiterer Messwerte auf dem Display

Um weitere Messwerte auf dem Display anzeigen zu lassen, kannst du das Vorgehen aus Schritt 1 wiederholen. Kopiere die bestehenden Blöcke und ändere die jeweilige Beschriftung sowie die Auswahl des Umweltphänomens. Damit alle Messwerte auch tatsächlich angezeigt werden, musst du jeweils die Platzierung auf dem Display anpassen. Du kannst die Höhe des Textes durch die Angabe der Pixel auf der y-Achse bestimmen. Diese kann zwischen 0 und 64 variieren. Um den Text für drei Messwerte in einem geeigneten Abstand auf dem Display anzeigen zu lassen, empfehlen sich beispielsweise 20er Schritte.

 {% include block.html image=page.image3 %}


### Schritt 3: Speichern des Messwerte auf der SD-Karte 

Damit du die Entwicklung der Messwerte über einen längeren Zeitraum überprüfen kannst, empfiehlt sich deren Speicherung auf der SD-Karte. Als erstes muss dafür im Setup eine Datei erstellt werden, in der anschließend die gespeicherten Daten zu finden sind. Anschließend legst du das Intervall fest, in dem die Messwerte erhoben werden sollen. Je nach Anwendungskontext sind hier verschiedene Zeiträume zu empfehlen. Als nächstes muss die zuvor erstellte Datei auf der SD-Karte geöffnet werden, damit die entsprechenden Messwerte dort eingetragen werden können. Füge dafür zuerst eine Beschriftung und anschließend die dazugehörigen Sensorwerte ein. Mit der Aktivierung des Zeilenumbruchs und dem Einfügen eines Simikolons werden dir die Messwerte anschließend übersichtlich dargestellt.  

 {% include block.html image=page.image4 %}


## Gesamter Code

 {% include block.html image=page.image5 %}

 Schaue dir den Programmcode in Blockly an: [Mini-Umweltmessstation](https://blockly.sensebox.de/gallery/63b59c8fd2853f0013b1d8a5)

 Kompiliere nun den Progranmmcode und übertrage ihn anschließend auf die senseBox MCU mini. 
 Nach der Datenerhebung kannst du die SD-Karte mit deinem Laptop oder PC auslesen. In einem einfachen Textprogramm werden dir dann die erhoben Umweltdaten angezeigt. Diese kannst du anschließend in Excel oder weiteren Datenverarbeitungsprogrammen importieren und beispielsweise analysieren und visualisieren. 
