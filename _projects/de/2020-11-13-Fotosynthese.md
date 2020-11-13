---
layout: project_page
title: "Fotosyntheseleistung erfassen"
date: 2020-11-13
author: Verena
abstract: "Beobachte die Fotosyntheseleistung einer Pflanze, indem du den CO2-Gehalt misst"
thumbnail:  /images/projects/Titelbild_Fotosynthese.jpg
image0: /images/projects/Fotosynthese/0.png
image1: /images/projects/Fotosynthese/1.png
image2: /images/projects/Fotosynthese/2.png

material:
    - CO2-Ampel Set oder
    - senseBox MCU
    - OLED-Display
    - CO2-Sensor
    - 2x JST-JST-Kabel
    - Pflanze 
    - verschließbares Gefäß

ide: blockly
version: ["edu", "mini", "CO2-Ampel"]   
addons: ["CO2-Sensor"] 
lang: de
tags: ["Informatik", "Biologie"]
difficult: leicht
---
<head><title>Fotosyntheseleistung erfassen</title></head>

# Fotosyntheseleistung einer Pflanze erfassen
Das Ziel dieses Projektes ist es, das Prinzip der Fotosynthese zu veranschaulichen, indem du den CO2-Gehalt in einem abgeschlossenen Gefäß, in dem sich eine Pflanze befindet, misst und die Daten graphisch auf dem Display der senseBox anzeigen lässt. Durch die Umwandlung von Kohlenstoffdioxid in Sauerstoff sollte der CO2-Gehalt abnehmen und gleichzeitig auch die Fotosyntheseleistung, sobald der Schwellwert an CO2 unter ein Minimum fällt. 

## Aufbau
Verbinde den CO2-Sensor mit einem JST-Kabel mit einem der fünf I2C/Wire-Anschlüsse der senseBox MCU. Ebenso gehst du vor, um das Display anzuschließen (siehe Abbildung). Da die Veränderung des CO2-Gehalts der Umgebungsluft einer Pflanze erfasst werden soll, platziere eine eingepflanzte Pflanze in ein lichtdurchlässiges Gefäß und lege den CO2-Sensor hinzu, während der Rest deiner senseBox außerhalb des Gefäßes bleibt. Verschließe das Gefäß anschließend, sodass kein Luftaustausch stattfinden kann. 

{% include image.html image=page.image0 %}

## Programmierung

Das Ziel der Programmierung ist es, den Verlauf des CO2-Gehalts innerhalb des Gefäßes graphsich auf dem angeschlossenen Display darzustellen.  

### Schritt 1: Display initialisieren und Messintervall festlegen
Da du das Display als Anzeige verwendest, sollte dies zuerst im Setup() initialisisert werden. Zudem kannst du anschließend in der Endlosschleiße festlegen, in welchem Messintervall die CO2-Konzentration bestimmt und angezeigt werden soll. In diesem Beispiel wurden 60000 ms (1 Minute) gewählt, da dieses Intervall genügt, um einen Eindruck über die Entwicklung der CO2-Konzentration zu erhalten.

{% include image.html image=page.image1 %}

### Schritt 2: Diagramm auf dem Display anzeigen lassen

Unter der Kategorie 'Display' findest du die Blöcke 'Zeige auf dem Display' und 'Zeichne Diagramm'. Diese benötigst du, um das Diagramm zu konfigurieren. Dabei ist es wichtig, dass du die Lücken des letzten Blocks sinnvoll ausfüllst. Überlege dir also, welche CO2-Konzentration in dem Gefäß realistisch ist und inwieweit sich diese verändern kann. Während diese Werte der y-Achse zugeordnet werden, gibt die x-Achse einen Überblick über die vergangene Zeit (t). Auch hier solltest du darüber nachdenken, welche Intervalle sinnvoll sind, um Veränderungen zu sehen. Als 'Wert' verwendest du den passenden Block zum CO2-Sensor (Sensirion SCD30).  

{% include image.html image=page.image2 %}

## Weiterführende Ideen und Anpassungen

Je nachdem, über welchen Zeitraum und wie genau du die Fotosyntheseleistung der Pflanze erfassen möchtest, kannst du dir entweder die Werte einzeln auf dem Display anzeigen lassen und eigenständig in einer Tabelle notieren oder die Werte auf einer SD-Karte speichern und anschließend mit einem Datenverarbeitungsprogramm wie Excel auswerten.
Des Weiteren könntest du das Experiment um weitere unabhängige Variablen ergänzen, wie beispielsweise durch die Verringerung des Lichteinfalls oder durch einer Veränderung der Temperatur. Damit könntest du dann die Auswirkungen unterschiedlicher Faktoren auf die Fotosyntheseleistung der Pflanze untersuchen.  