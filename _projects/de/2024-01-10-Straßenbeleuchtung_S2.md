---
layout: project_page
title: "Intelligente Straßenbeleuchtung"
date: 2024-01-10
author: Verena
abstract: "Programmiere ein Licht, das automatisch angeschaltet wird, sobald es dunkel wird."
thumbnail:  /images/projects/Titelbild_Straßenbeleuchtung.png
image0: /images/projects/Straßenbeleuchtung/0.png
image1: /images/projects/Straßenbeleuchtung/1.png
image2: /images/projects/Straßenbeleuchtung/2.png
image3: /images/projects/Straßenbeleuchtung/3.png


material:
    - senseBox MCU-S2
    - 1x OLED-Display
    - 1x QWIIC-Kabel
    
ide: blockly
version: ["edu-S2"]   
lang: de
tags: ["Informatik", "Physik"]
difficult: mittel
---
<head><title>Intelligente Straßenbeleuchtung</title></head>

# Eine intelligente Straßenbeleuchtung bauen und programmieren
In Deutschland werden jährlich etwa 750 Millionen Euro für die Beleuchtung von Straßen, Plätzen und Brücken ausgegeben. Dabei ist die Beleuchtung gar nicht notwendig, solange es noch hell ist. Gestalte die Beleuchtung für eine Smart City intelligent und energiesparsam, sodass sie nur dann leuchtet, wenn es dunkel ist.

## Aufbau
Eine Photodiode zur Messung der Beleuchtungsstärke und die RGB-LED sind drekt auf dem Board verbaut, sodass sie nicht separat angeschlossen werden müssen. Zur Uberprüfung der Messwerte der Beleuchtungsstärke macht es jedoch Sinn, zusätzlich ein Display anzuschließen. Verbinde dafür das Display mit einem QWIIC-Kabel und verbinde es mit dem I2C-Anschluss der MCU-S2.  

{% include image.html image=page.image0 %}

## Programmierung

Das Ziel der Programmierung ist es, die RGB-LED einzuschalten, wenn die Beleuchtungsstärke unter 10 Lux fällt. Die Meswerte des Lichtsensors sollen auf dem Display angezeigt werden. 

### Schritt 1: Initialisierung der RGB-LED und des Displays 

Um die Messwerte anzeigen zu lassen, musst du zuerst das Display programmieren. Dazu muss es ebenso wie die RGB-LED im Setup initialisiert werden. 

{% include image.html image=page.image1 %}

### Schritt 2: Anzeige der Messwerte auf dem Display

In der Endlosschleife wird angegeben, dass Text angezeigt werden soll. Nutze dafür die Blöcke 'Zeige auf dem Display' und 'Schreibe Text/ Zahl'. Bei 'Wert' kombinierst du mit dem Block 'Erstelle Text aus' aus der Katgeorie 'Text' nun die Beschriftung und den Messwert des Lichtsensors. Füge zudem ein 'Display löschen'-Block ein, damit die Messwerte nicht zu schnell aktualisiert werden und weiterhin lesbar sind. 

{% include image.html image=page.image2 %}

### Schritt 2: Auftsellen der Bedingung

Um eine Beziehung zwischen der LED und dem Wert des Lichtsensors herzustellen, benötigst du den ‚wenn...mache‘-Block mit der ergänzenden ‚sonst‘-Funktion. Du stellst mithilfe verschiedener Blöcke aus den Kategorien Logik (<), Mathematik (10), Sensoren und LED nun folgende Bedingung auf: Wenn die Beleuchtungsstärke kleiner ist als 10 Lux, wird die RGB-LED in der Farbe gelb eingeschaltet - sonst bleibt sie aus (Farbe: schwarz). Da ausschließlich die RGB-LED 'on Board' verwendet wird, können die Einstellungen bei Anzahl (1) und Position (0) unverändert bleiben. 
Durch den Warteblock aus der Katgeorie 'Zeit' kannst du den Durchlauf des Programms in der Endlosschleife etwas verlangsamen.

{% include image.html image=page.image3 %}

Übertrage nun den Programmcode und teste ihn, indem du den Lichtsensor auf dem Board mit deiner Hand abdunkelst. 

!! Den gesamten Blockly-Sketch findest du [hier](https://blockly.sensebox.de/gallery/642e7500d2853f0013b357e6).


