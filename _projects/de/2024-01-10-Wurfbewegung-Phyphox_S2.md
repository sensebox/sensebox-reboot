---
layout: project_page
title: "Analyse von Wurfbewegungen"
date: 2024-01-10
author: Verena
abstract: "Analysiere Wurfbewegungen unter variablen Bedingungen mihilfe der Phyphox-App."
thumbnail:  /images/projects/Titelbild_Wurfbewegungen.png
image0: /images/projects/Wurfbewegungen_S2/0.png
image1: /images/projects/Wurfbewegungen_S2/1.png
image2: /images/projects/Wurfbewegungen_S2/2.png
image3: /images/projects/Wurfbewegungen_S2/3.png

material:
    - senseBox MCU-S2
    - 1x Bluetooth-Bee
    - 1x Powerbank/ Akku
    - 1x Beschleunigungssensor (on Board)
    - evtl. Ball, Schaumstoff

ide: blockly
version: ["edu-S2"]   
lang: de
tags: ["Informatik", "Physik", "Phyphox"]
difficult: mittel
---
<head><title>Analyse von Wurfbewegungen unter variablen Bedingungen</title></head>

# Erfasse die Beschleunigungsdaten der senseBox
In Physik stellt das Zusammenwirken verschiedener Kräfte einen zentralen Gegnstandsbereich dar. Dabei sind vor allem die Phänomene der Kraft, Trägheit und Beschleunigung, beispielsweise bei einem freien Fall, von Relevanz. Ein Wurf der senseBox, die durch das Bluetooth-Bee mit der Phyphox App verbunden ist, ermöglicht die zeitgleiche Betrachtung der Beschleunigungsdaten in unterschiedliche Richtungen auf dem Smartphone oder Tablet. Dadurch kann die Nachvollziehbarkeit der erhobenen Messwerte unterstützt, sowie eine Grundlage für weitergehende Berechnungen gelegt werden.

## Aufbau
Der Beschleunigungssensor ist direkt im Mikrocontroller der senseBox integriert, sodass dieser nicht angeschlossen werden muss. Das Bluetooth-Bee wird auf den Steckplatz XBee des Mikrocontrollers gesteckt. 

{% include image.html image=page.image0 %}

## Programmierung

Das Ziel der Programmierung ist es, eine Verbindung zur Phyphox-App herzustellen. Diese soll die gemessenen Werte der Beschleunigung in geeigneten Graphen anzeigen.

### Schritt 1: Phyphox-Gerät einrichten
Die Programmierung deines Messgeräts erfolgt mit Blockly für senseBox. Initialisiere dort im Setup() zuerst ein Phyphox-Gerät und benenne dies individuell. Mit dem Block ‚Erstelle Experiment‘ kannst du die Darstellung deiner Messwerte konfigurieren. Bei der Messung der Beschleunigung bietet sich eine Abbildung der Zeit in Sekunden auf der x-Achse sowie eine Darstellung der Beschleunigung auf der y-Achse an. Da letztere in drei Richtungen erfolgt sowie insgesamt erfasst werden kann, muss für jede Richtung ein neuer Graph mit dem zugehörigen Kanal für den erfassten Wert erstellt werden. Letzteres gleichst du mit den Angaben in der Endlosschleife ab, sodass jeweils ein Kanal einer Beschleunigungsrichtung zugehörig ist (siehe unten). Im Beispiel siehst du nur zwei der vier notwendigen Blöcke für die gewünschten Graphen. 

{% include image.html image=page.image1 %}

### Schritt 2: Senden der Messwerte
In der Endlosschleife bindest du den Beschleunigungssensor ein und wählst die gewünschte Richtung aus (x-, y-, z-Achse oder Gesamt) aus. Zudem verwendest du denselben Kanal wie in den obigen Blöcken.

{% include image.html image=page.image2 %}

Damit ist der Programmcode fertig! Du kannst nun den Sketch kompilieren und auf die senseBox MCU übertragen. Nun solltest du eine Stromversorgung mit einer Powerbank sicherstellen, sodass du die senseBox frei bewegen kannst. Um die senseBox beim Experiment zu schützen, empfiehlt sich beispielsweise ein gefütteter Ball oder Schaumstoff. Des Weiteren werden Gewichte mit 2kg benötigt. 


## Verbindung mit der Phyphox-App
Öffnet die Phyphox App, klicke auf das + und wähle ‚Neues Experiment für Bluetooth-Gerät‘ aus. Es wird nun eine Liste von verfügbaren Messgeräten angezeigt. Klicke auf dein Messgerät, um die Verbindung herzustellen. Zum Einstellen des Messzeitraums für das Experiment klicke auf die drei Punkte und öffne den Punkt ‚Zeitautomatik‘. Da ein Wurf nur wenig Zeit in Anspruch nimmt, reicht für das Experiment eine Dauer von 10 Sekunden aus. Betätige anschließend den Button ‚Zeitautomatik aktivieren‘.

{% include image.html image=page.image3 %}

Starte das Experiment mit einem Klick auf den ‚Start‘ Button. Die Messwerte der senseBox werden nun von der App aufgezeichnet. 
Für die Durchführung des Experiments empfiehlt es sich, unterschiedliche Wurfbewegungen (waagerecht, senkrecht nach oben oder senkrecht nach unten (freier Fall)) zu betrachten. Pro Wurfbewegung werden die unterschiedlichen Einflüsse auf die Beschleunigung untersucht, dabei kannst du das Gewicht sowie die Höhe und Weite variieren. Letzteres steuerst du, indem du die senseBox in einem Ball waagerecht oder senkrecht wirfst. Denke dabei daran, dass die Bluetooth-Verbindung bei einer zu großen Entfernung abbricht.

Nachdem die Experimente jeweils beendet wurden, kannst du über die drei Punkte 'Zustand speichern' auswählen und es benennen. Die gespeicherten Graphen geben dir nun die Möglichkeit, die unterschiedlichen Einflüsse auf die Wurfbewegung zu analysieren.

## Gesamter Code

Den fertigen Programmcode in Blockly findest du hier: [Analyse von Wurfbewegungen](https://blockly.sensebox.de/gallery/63b59d69d2853f0013b1d8c7)
