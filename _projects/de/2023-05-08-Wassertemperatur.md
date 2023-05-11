---
layout: project_page
title: "Messung der Wassertemperatur"
date: 2023-05-08
author: Verena
abstract: "Beobachtung der Gefrier- und Siedekurven von Wasser mit einem Waserthermometer und der Phyphox App."
thumbnail:  /images/projects/Titelbild_Wassertemperatur.png
image0: /images/projects/Wassertemperatur/0.png
image1: /images/projects/Wassertemperatur/1.png
image2: /images/projects/Wassertemperatur/2.png
image3: /images/projects/Wassertemperatur/3.png
image4: /images/projects/Wassertemperatur/4.png
image5: /images/projects/Wassertemperatur/5.png
material:
    - senseBox MCU 
    - OLED Display
    - Wasserthermometer inkl. Anschlusskabel
    - One-Wire Adapter
    - Bluetooth-Bee
    - JST-JST Kabel
    - evtl. Powerbank
ide: blockly
version: ["edu"]   
lang: de
tags: ["Phyphox", "Chemie"]
addons: ["Bluetooth-Bee", "Wasserthermometer"]  
difficult: leicht
---

In diesem Projekt lernst du, Gefrier- und Siedekurven für Wasser zu erstellen. Für die Messung verwendest du die senseBox mit einem Wasserthermometer, welche die Daten via Bluetooth an die Phyphox-App sendet. In der App kannst du deine Datenerhebung verfolgen und den dort sichtbaren Graphen zur Beobachtung der Gefrier- und Siedekurven nutzen.

## Aufbau
Stecke das Bluetooth Bee auf den Steckplatz XBee 1 der senseBox MCU. Verbinde den Wassertemperatursensor-Sensor mit einem der Steckplätze des One-Wire Adapters. Diesen schließt du dann mit dem JST-JST Kabel an einen der drei Digital-Ports an.

{% include block.html image=page.image0 %}

{% include block.html image=page.image1 %}

Verbinde zum Schluss die senseBox MCU mit dem USB-Kabel mit deinem Laptop, sodass diese mit Strom versorgt wird. Nachdem du den Programmcode (siehe Programmierung) auf die senseBox MCU übertragen hast, kannst du eine Stromversorgung beispielsweise auch mit einer Powerbank sicherstellen. Stelle für das Experiment einen Behälter mit 500 ml Wasser bereit. Zusätzlich benötigst du die Möglichkeit das Wasser gefrieren oder erhitzen zu lassen.  

## Programmierung

Die Programmierung deines Messgeräts erfolgt mit [Blockly für senseBox](https://blockly.sensebox.de). 
Initialisiere dort im Setup() zuerst ein Phyphox-Gerät und benenne dies individuell. Mit dem Block ‚Erstelle Experiment‘ kannst du die Darstellung deiner Messwerte konfigurieren. Bei der Messung der Wassertemperatur bietet sich eine Abbildung der Zeit in Sekunden auf der x-Achse sowie eine Darstellung der Temperatur in Grad Celsius auf der y-Achse an.

{% include block.html image=page.image2 %}

In der Endlosschleife bindest du das Wasserthermometer ein und wählst den Port aus, an welchem du den Sensor mit dem Verbindungskabel angeschlossen hast. Diesen kannst du auf der senseBox MCU ablesen.
Damit ist der Programmcode fertig! Du kannst nun den Sketch kompilieren und auf die senseBox MCU übertragen.

{% include block.html image=page.image3 %}


## Verbindung mit der Phyphox-App

Öffnet die Phyphox App, klicke auf das + und wähle ‚Neues Experiment für Bluetooth-Gerät‘ aus. 

Dir wird nun eine Liste von verfügbaren Messgeräten angezeigt. Klicke auf dein Messgerät, um die Verbindung herzustellen. Zum Einstellen des Messzeitraums für das Experiment klicke auf die drei Punkte und öffne den Punkt ‚Zeitautomatik‘. Möchtest du das Wasser beispielsweise mit einem Wasserkocher erhitzen, so reichen 10 Minuten (600 Sekunden) für die Dauer des Experiments aus. Möchtest du hingegen den Gefrierpunkt bestimmen, während das Wasser im Gefrierfach ist, so solltest du mehrere Stunden für den Ablauf des Experiments einplanen. 

Starte das Experiment mit einem Klick auf den ‚Start‘ Button. Die Messwerte der senseBox werden nun von der App aufgezeichnet. Beobachte nun den Temperaturverlauf, wenn sich der Aggregatzustand des Wassers zweischen fest, flüssig und gasförmig verändert. 

{% include block.html image=page.image4 %}

{% include block.html image=page.image5 %}

## Gesamter Code

 Schaue dir den Programmcode in Blockly an: [Messung der Wassertemperatur](https://blockly.sensebox.de/gallery/63b59c8fd2853f0013b1d8a5)

