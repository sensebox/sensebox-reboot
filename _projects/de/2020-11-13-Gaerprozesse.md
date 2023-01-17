---
layout: project_page
title: "Experiment zu Gärprozessen"
date: 2020-11-13
author: Verena
abstract: "Beobachte die Gärprozesse von Hefe unter verschiedenen Bedingungen"
thumbnail:  /images/projects/Titelbild_Gärprozesse.png
image0: /images/projects/Gärprozesse/0.png
image1: /images/projects/Gärprozesse/1.png
image2: /images/projects/Gärprozesse/2.png
image3: /images/projects/Gärprozesse/3.png


material:
    - senseBox MCU
    - 1x OLED-Display
    - 1x CO2-Sensor
    - 1x mSD-Bee mit SD-Karte
    - 2x JST-JST-Kabel
    - Hefe
    - warmes Zuckerwasser
    - abgeschlossenes Gefäß

ide: blockly
version: ["edu", "mini v1", "CO2-Ampel"]   
addons: ["CO2-Sensor"] 
lang: de
tags: ["Informatik", "Chemie"]
difficult: mittel
---
<head><title>Experiment zu Gärprozessen</title></head>

# Experiment zu Gärprozessen
Beim Backen von Brot, Pizza oder Gebäck ist häufig Hefe notwendig, die den Teig besonders locker macht. Damit dies geschieht, ist bekannt, dass man den Teig 'gehen lassen' muss. Aber was genau passiert währenddessen in dem Teig und welcher chemische Prozess verbirgt sich dahinter? Dieser Frage gehen wir in diesem kleinen Experiment zum Gärprozess nach.
Der CO2-Sensor hat dabei die Aufgabe, die Veränderung der CO2-Konzentration in Abhängigkeit von der Zeit zu erfassen. Da die Gärprozesse etwas Zeit in Anspruch nehemen können, empfiehlt es sich, die Daten auf der SD-Karte zu speichern und diese anschließend in einem geeigneten Progamm wie Excel auszuwerten.   

## Aufbau
Das Display ist in diesem Zusammenhang sinnvoll, um die Werte, die auf der SD-Karte gespeichert werden, zu überprüfen. Du schließt es mithilfe eines JST-JST-Kabels an einem der I2C/Wire Anschlüsse der senseBox MCU an. Ebenso verbindest du auch den CO2-Sensor mit der sneseBox MCU. Die SD-Karte steckst du in das mSD-Bee, welches du auf XBee-Steckplatz 2 platzierst. Um einen Gärprozess zu generieren, solltest du nun noch ein Hefegemisch herstellen. Dafür eignet sich beispielsweise folgendes Mengenverhältnis: 1 g Trockenhefe, 3 g Zucker, 20 g Wasser. Fülle das Gemisch in eine Glasschale, die du wiederum zusammen mit dem CO2-Sensor in ein größeres, geschlossenes Gefäß positionierst oder mit einer weiteren Schale überdeckst.  

{% include image.html image=page.image0 %}

## Programmierung
### Schritt 1: Variablen definieren
Da du das Display verwendest sowie Daten auf der SD-Karte speichern möchtest, müssen beide Komponenten zuerst einmal im `Setup()` eingebunden werden. Zudem ist es in der Endlosschleife notwendig, die beiden Variablen zu definieren, auf die du dich später beziehst. In diesem Fall bietet es sich an, die Variablen 'Zeit' und 'CO2' zu definieren und letztere in Verbindung mit dem CO2-Sensor zu setzen. Du benennst eine Variable um oder erstellst eine neue Variable, indem du bei den Blöcken unter der Kategorie `Variablen` auf den kleinen Pfeil in dem rosa unterlegten Feld klickst. Dort werden dir dann die unterschiedlichen Optionen und bereits genutzten Variablen aufgeführt.

{% include image.html image=page.image1 %}

### Schritt 2: Werte auf dem Display anzeigen lassen
Damit dir die Werte des Sensors auf dem Display angezeigt werden, benötigst du die Blöcke 'Zeige auf dem Display' sowie 'Schreibe Text/ Zahl'. Für eine übersichtlichere Darstellung verwende den Block 'Erstelle Text aus' in Verbindung mit den bereits definierten Variablen und ändere den Wert der y-Koordinate, sodass sich die Texte nicht überlappen, sondern untereinander angezeigt werden. Wähle zuletzt den Block 'Display löschen', damit die Werte auf dem Display stets aktualisiert angezeigt werden.  

{% include image.html image=page.image2 %}

### Schritt 3: Daten auf SD-Karte speichern
Damit die Daten in einem angemessenen zeitlichen Abstand auf der SD-Karte gespeichtert werden, verwende den Block 'Messintervall in ms' aus der Kategorie 'Zeit'. Bevor die Daten auf der SD-Karte geschrieben werden können, muss die notwendige Datei geöffnet werden. Überlege dir anschließend, wie die Daten dargestellt werden sollen. Es bietet sich die Trennung durch ein Semikolon sowie ein Zeilenumbruch nach jedem Messintervall an. 

Damit sind die Programmierung und der Aufbau abgeschlossen. 

Der fertige Programmcode ist in der folgenden Abbildung zu sehen.

{% include image.html image=page.image3 %}

Den gesamten Blockly-Sketch findest du [hier](https://blockly.sensebox.de/gallery/63b69e07d2853f0013b1d9e0).

Hast du nun den Programmcode auf die senseBox übertragen und den Sensor zusammen mit dem Hefegemisch in einem abgeschlossenen Gefäß positioniert, heißt es zuerst einmal abwarten. Falls du ein durchsichtiges Gefäß verwendest, kannst du beobachten, wann die Hefe beginnt, den Zucker abzubauen und Kohlenstoffdioxid zu produzieren. Mit dem oben genannten Mischverhältnis empfiehlt es sich, das Experiment für ca. 30 Minuten laufen zu lassen und anschließend mit der Datenauswertung zu beginnen. 

## Auswertung der Daten
Die Daten wurden auf der SD-Karte gespeichert und können verwendet werden, um die Veränderung der CO2-Konzentration bei Gärprozessen zu interpretieren. 
Die TXT-Datei sollte nach folgendem Schema aufgebaut sein: 'Zeit in ms; Co2-Konzentration in ppm;'. Die Semikolons ermöglichen dir eine anschauliche Dartsellung in Excel.
Kopiere dazu die Daten der TXT-Datei und füge sie in die erste Spalte in Excel ein. Nun stehen allerdings die Zeit und die CO2-Konzentration in einer Spalte. Um dies zu ändern, klicke auf den Button 'Strg' sowie anschließend auf 'Textkonvertierungs-Assistenten verwenden'. Hier kannst du im zweiten Schritt nun einstellen, dass Semikolons als Trennzeichen erkannt werden sollen. Tätigst du diese Einstellung, wird dir nun in 'Spalte A' die Zeit und in 'Spalte B' die CO2-Konzentration angezeigt. 
Diese Werte kannst du nutzen, um ein Diagramm zu erstellen, dass die minütliche CO2-Konzentration in einem Graphen abbildet.  

## Weiterführende Ideen und Anpassungen
Das hier vorgestellte Experiment findet unter aeroben Bedingungen statt, da die Anwesenheit von Sauerstoff gewährleistet ist. Die Hefezellen atmen folglich und bauen den Zucker vollständig zu Kohlenstoffdioxid und Wasser ab. Dabei gewinnen sie viel Energie, bilden aber kaum Alkohol. Letzterer kann entstehen, falls den Hefezellen der Sauerstoff entzogen wird (anaerobe Bedingungen). In diesem Fall findet eine Gärung statt, bei dem Glucose und Fructose zu Ethanol und Kohlenstoffdioxid abgebaut wird. Auf diesem Weg kann also beispielsweise eigenständig Wein hergestellt werden. Alternativ kann in dem Experiment zudem die Variable der Temperatur verändert werden, um die Bedeutung dieser für den Gärprozess zu erfassen. 

