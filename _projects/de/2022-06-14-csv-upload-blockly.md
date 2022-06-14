---
layout: project_page
title: "Datenupload von SD-Karte im CSV-Format mit Blockly"
date: 2022-06-14
author: Paul
abstract: "Ein Tutorial zum CSV-Datenupload mit der senseBox"
thumbnail: /images/projects/Titelbild_CSV.png
image0: /images/projects/csv-upload/set-rtc.png
image1: /images/projects/csv-upload/setup-main.png
image2: /images/projects/csv-upload/loop-main.png
material:
    - senseBox MCU
    - SD-Karte
    - SD-Bee
    - RTC
    - Beliebiger Umweltsensor
ide: blockly    
lang: de
addons:  #Gib hier an wenn zusätzliche Komponenten verwendet werden
version: ["edu", "mini", "home"]
tags: ["CSV","SD", "openSenseMap"]
difficult: leicht #Verwende leicht, mittel, schwer, sehr schwer
---
# CSV-Upload mit Blockly
In diesem Projekt wird gezeigt, wie Daten mit Blockly auf eine SD-Karte geschrieben werden können und wie man diese anschließend auf die openSenseMap hochlädt.

## Aufbau
Stecke deinen SD-Bee auf den Steckplatz XBEE2 und schließe einen beliebigen Sensor an die MCU an. Zum Schluss schließt du noch die RTC an die MCU an und legst die Batterie ein.

## Vorbereitung auf der openSenseMap
Die Box sollte bereits mit passenden Sensoren auf der openSenseMap registriert sein. In diesem Projekt wird von einer stationären Box ausgegangen, es ist aber auch möglich, mobile Boxen per SD-Upload mit der openSenseMap zu verbinden.

Falls Du noch nicht weißt, wie man eine Box auf der openSenseMap registriert, schau [hier](https://sensebox.de/projects/de/2019-04-11-iotmesstation.html#schritt-1-registrierung-auf-der-OpenSenseMap) nach.

## Programmierung in Blockly

Öffne [Blockly](https://blockly-react.netlify.app/). Die weitere Programmierung erfolgt jetzt in zwei Schritten:

### Schritt 1: Zeit der RTC setzen:

Als erstes muss die RTC einmal auf die aktuelle Uhrzeit eingestellt werden, damit die openSenseMap nachher auch weiß, wann die Messungen vorgenommen wurden. Das macht das folgende Programm:
{% include image.html image=page.image0 %}

Kompiliere es und lade es auf deine MCU hoch. **Dieser Schritt muss nur einmal gemacht werden, ab jetzt merkt sich die RTC die Zeit selbstständig**

### Schritt 2: Hauptprogramm:
Lösche den ``Setze Uhrzeit/Datum der RTC`` Block aus Blockly und baue folgendes Programm nach:

Im Setup befinden sich die zwei Blöcke ``Initialisiere RTC`` und ``Erstelle Datei auf SD-Karte``.

{% include image.html image=page.image1 %}

Den Dateinamen kannst du frei wählen, er darf aber **nicht länger als 8 Buchstaben** sein, als Dateiformat wähle bitte ``.csv``.

Der Loop sieht folgendermaßen aus:

{% include image.html image=page.image2 %}

Die Blöcke ``Intervall`` und ``Zeitstempel (RFC 3339)`` findest du im *Zeit* Reiter auf der linken Seite, die Blöcke zur SD-Karte im *SD* Reiter und die Sensorblöcke unter *Sensoren*. 
**Pass auf, dass der Dateiname im Setup mit dem im Loop übereinstimmt!**
Trage bei sensorID die passende **sensorID** aus der openSenseMap ein und wähle dein Messintervall. Falls du mehrere Sensoren speichern willst, kannst du unter den ``Speichere Messwert``-Block weitere solcher Blöcke anfügen, du findest sie im *SD*-Reiter.

Jetzt kannst du das Programm kompilieren und auf die MCU übertragen.

## Upload zur openSenseMap
Wenn deine Station ein paar Messdaten gesammelt hat, kannst du diese auf die openSenseMap hochladen. 