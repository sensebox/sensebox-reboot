---
layout: project_page
title: "Optimierung von Lüftungsstrategien"
date: 2024-01-10
author: Verena
abstract: "Messe die CO2-Konzentration in deinem Zimmer mithilfe der Phyphox-App."
thumbnail:  /images/projects/Titelbild_Lueftungsstrategien.png
image0: /images/projects/Lüftungsstrategien_S2/0.png
image1: /images/projects/Lüftungsstrategien_S2/1.png
image2: /images/projects/Lüftungsstrategien_S2/2.png
image3: /images/projects/Lüftungsstrategien_S2/3.png

material:
    - senseBox MCU-S2
    - 1x CO2-Sensor
    - 1x Bluetooth-Bee
    - 1x QWICC-Kabel 
    - evtl. Batterie
    
ide: blockly
version: ["edu-S2"]   
lang: de
tags: ["Informatik", "Physik", "Phyphox"]
difficult: leicht
---
<head><title>Optimierung von Lüftungsstrategien mithilfe von Phyphox</title></head>

# Messe die CO2-Konzentration in deinem Zimmer
In diesem Projekt findest du heraus, wie hoch die CO2-Konzentration in deinem Zimmer ist. Für die Messung verwendest du die senseBox, welche die Daten via Bluetooth an Phyphox sendet. In der App kannst du deine Datenerhebung verfolgen und den dort sichtbaren Graphen als Ausgangslage für die Interpretation der CO2-Konzentration und folglich der Lüftungsstrategien nutzen.  

## Aufbau
Zuerst verbindest du den CO2-Sensor mit dem QWIIC-Kabel. Diesen schließt du an einen der beiden I2C-Anschlüsse deiner senseBox MCU-S2 an. Das Bluetooth-Bee wird auf den Steckplatz XBee des Mikrocontrollers gesteckt. Bei Bedarf schließt du die Batterie inkl. Batteriepack an den Anschluss 'Battery' an. 

{% include image.html image=page.image0 %}

## Programmierung

Das Ziel der Programmierung ist es, eine Verbindung zur Phyphox-App herzustellen. Diese soll die gemessenen Werte der CO2-Konzentration und der Temperatur in einem geeigneten Graphen anzeigen.

### Schritt 1: Phyphox-Gerät einrichten
Die Programmierung deines Messgeräts erfolgt mit Blockly für senseBox. Initialisiere dort im Setup() zuerst ein Phyphox-Gerät und benenne dies individuell. Wenn mehrere Messgeräte in einem Raum verwendet werden, kannst du über den Namen dein Messgerät wiederfinden. Mit dem Block ‚Erstelle Experiment‘ kannst du die Darstellung deiner Messwerte konfigurieren. Da der CO2-Sensor sowohl die CO2-Konzentration als auch die Temperatur messen kann, empfehlen sich zwei Graphen. Über den ersten Kanal kannst du die CO2-Konzentration übermitteln und auf der x-Achse die Zeit in Sekunden sowie auf der y-Achse die erhobenen Messwerte in parts per million (ppm) abbilden. Über den zweiten Kanal kannst du die erhobenen Daten zur Temperatur übermitteln und diese auf der y-Achse in Grad Celsius abbilden, während auf der x-Achse erneut die Zeit in Sekunden als Orientierung dient. 

{% include image.html image=page.image1 %}

### Schritt 2: Senden der Messwerte
In der Endlosschleife bindest du den CO2-Sensor ein und wählst zum einen die Temperatur und zum anderen die CO2-Konzentration als Messwerte aus. Über den Block 'Messintervall' kannst du einstellen, wie oft die Messwerte von der senseBox an die Phyphox App gesendet werden sollen.

{% include image.html image=page.image2 %}

 Damit ist der Programmcode fertig! Du kannst nun den Sketch kompilieren und auf die senseBox MCU übertragen.

[Hier](https://blockly.sensebox.de/gallery/63b5a057d2853f0013b1d900) kannst du den fertigen Programmcode in Blockly abrufen. 

## Verbindung mit der Phyphox-App
Öffnet die Phyphox App, klicke auf das + und wähle ‚Neues Experiment für Bluetooth-Gerät‘ aus. Es wird nun eine Liste von verfügbaren Messgeräten angezeigt. Klicke auf dein Messgerät, um die Verbindung herzustellen. Zum Einstellen des Messzeitraums für das Experiment klicke auf die drei Punkte und öffne den Punkt ‚Zeitautomatik‘. Da das Experiment 10 Minuten laufen soll, trage bei der Dauer 600 Sekunden ein.

{% include image.html image=page.image3 %}

Starte das Experiment mit einem Klick auf den ‚Start‘ Button. Die Messwerte der senseBox werden nun von der App aufgezeichnet. 
Gehe nun schrittweise vor und öffne bzw. schließe das Fenster nach einigen Minuten vollständig oder teilweise. Nachdem das Experiment beendet wurde, kannst du über die drei Punkte 'Zustand speichern' auswählen und es benennen. Der gespeicherte Graph gibt dir nun die Möglichkeit, dein Lüftungsverhalten auf Grundlage der CO2-Konzentration zu analysieren und geeignete Strategien abzuleiten. 

