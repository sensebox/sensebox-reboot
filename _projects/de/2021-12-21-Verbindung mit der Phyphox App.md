---
layout: project_page
title: "Verbindung der senseBox und Phyphox"
date: 2021-12-21
author: Verena
abstract: "Übertrage mit der senseBox gemessene Werte via Bluetooth an die Phyphox-App."
thumbnail:  /images/projects/Titelbild_Phyphox.png
image0: /images/projects/Phyphox-App/0.png
image1: /images/projects/Phyphox-App/1.png
image2: /images/projects/Phyphox-App/2.png
image3: /images/projects/Phyphox-App/3.png

material:
    - senseBox MCU
    - 1x JST-JST-Kabel
    - 1x Temperatursensor (HDC1080)
    - 1x Bluetooth-Bee
    
ide: blockly
version: ["edu"]   
lang: de
tags: ["Informatik", "Physik", "Phyphox"]
difficult: leicht
---
<head><title>Verbindung mit der Phyphox-App</title></head>

# Die Phyphox-App
Mit der kostenfreien App Phyphox kannst du dein Smartphone zum Experimentieren einsetzen und dabei unentdeckte Möglichkeiten deines täglichen Begleiters kennenlernen. Die App verwendet dazu die in Smartphones verbauten Sensoren und ersetzt somit kostspielige Versuchsaufbauten. Phyphox soll dazu beitragen, dass physikalische Zusammenhänge und wissenschaftliche Arbeitsweisen ohne viel Aufwand erlernt werden können. Durch die Übertragung via Bluetooth ist eine Beobachtung der Messwerte in Echtzeit möglich.  

## Aufbau
Zuerst verbindest du einen Sensor, beispielsweise den Temepratursensor (HDC1080), mit dem JST-JST-Kabel. Diesen schließt du an einem der fünf I2C/Wire-Anschlüsse deiner senseBox MCU an. Das Bluetooth-Bee wird auf den Steckplatz XBee1 des Mikrocontrollers gesteckt. 

{% include image.html image=page.image0 %}

## Programmierung

Das Ziel der Programmierung ist es, eine Verbindung zur Phyphox-App herzustellen. Diese soll die gemessenen Werte der Temperatur in einem geeigneten Graphen anzeigen.

### Schritt 1: Phyphox-Gerät einrichten
Die Programmierung deines Messgeräts erfolgt mit Blockly für senseBox. Initialisiere dort im Setup() zuerst ein Phyphox Gerät und benenne dies individuell. Wenn mehrere Messgeräte in einem Raum verwendet werden, kannst du über den Namen dein Messgerät wiederfinden. Mit dem Block ‚Erstelle Experiment‘ kannst du die Darstellung deiner Messwerte konfigurieren. Über den Kanal kannst du die Messwerte der Temperatur übermitteln, welche auf der y-Achse dargestellt werden sollen. Auf der x-Achse soll die Zeit in Sekunden abgebildet werden, weshlab hier der Block 'Zeitstempel' einzufügen ist. Möchtest du Werte zu verschiedenen Phänomenen übertragen, so muss für jeden weiteren Graphen ein neuer Kanal eingerichtet werden. 

{% include image.html image=page.image1 %}

### Schritt 2: Senden der Messwerte
In der Endlosschleife bindest du nun den Temperatursensor als Wert für den ersten Kanal ein. Über den Block 'Messintervall' kannst du einstellen, wie oft die Messwerte von der senseBox an die Phyphox-App gesendet werden sollen.
Damit ist der Programmcode fertig! Du kannst nun den Sketch kompilieren und auf die senseBox MCU übertragen.

{% include image.html image=page.image2 %}

## Verbindung mit der Phyphox-App
Öffnet die Phyphox App, klicke auf das + und wähle ‚Neues Experiment für Bluetooth-Gerät‘ aus. Es wird nun eine Liste von verfügbaren Messgeräten angezeigt. Klicke auf dein Messgerät, um die Verbindung herzustellen. Zum Einstellen des Messzeitraums für das Experiment klicke auf die drei Punkte und öffne den Punkt ‚Zeitautomatik‘. Da das Experiment 10 Minuten laufen soll, trage bei der Dauer 600 Sekunden ein.

{% include image.html image=page.image3 %}

Starte das Experiment mit einem Klick auf den ‚Start‘ Button. Die Messwerte der senseBox werden nun von der App aufgezeichnet. Nachdem das Experiment beendet wurde, kannst du über die drei Punkte 'Zustand speichern' auswählen und es benennen. 

# Hinweise
* Entferne das Tablet/ Smartphone nicht weiter als drei Meter vom Messgerät, sodass die Bluetooth-Verbindung bestehen bleibt
* Das Tablet/ Smartphone sollte während der Messung nicht ausgeschaltet werden
