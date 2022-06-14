---
layout: project_page
title: "Datenupload von SD-Karte im CSV-Format mit Blockly"
date: 2022-06-14
author: Paul
abstract: "Ein Tutorial zum CSV-Datenupload mit der senseBox"
thumbnail: /images/projects/Titelbild_CSV.png
image0: /images/projects/csv-upload/set-rtc.png
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
tags: ["CSV","SD", "OpenSenseMap"]
difficult: leicht #Verwende leicht, mittel, schwer, sehr schwer
---
# CSV-Upload mit Blockly
In diesem Projekt wird gezeigt, wie Daten mit Blockly auf eine SD-Karte geschrieben werden können und wie man diese anschließend auf die OpenSenseMap hochlädt.

## Aufbau
Stecke deinen SD-Bee auf den Steckplatz XBEE2 und schließe einen beliebigen Sensor an die MCU an. Zum Schluss schließt du noch die RTC an die MCU an und legst die Batterie ein.

## Vorbereitung auf der OpenSenseMap
Die Box sollte bereits mit passenden Sensoren auf der OpenSenseMap registriert sein. In diesem Projekt wird von einer stationären Box ausgegangen, es ist aber auch möglich, mobile Boxen per SD-Upload mit der OpenSenseMap zu verbinden.

Falls Du noch nicht weißt, wie man eine Box auf der OpenSenseMap registriert, schau [hier](https://sensebox.de/projects/de/2019-04-11-iotmesstation.html#schritt-1-registrierung-auf-der-opensensemap) nach.

## Programmierung in Blockly

Öffne [Blockly](https://blockly-react.netlify.app/). Die weitere Programmierung erfolgt jetzt in zwei Schritten:

### Schritt 1: Zeit der RTC setzen:

Als erstes muss die RTC einmal auf die aktuelle Uhrzeit eingestellt werden, damit die openSenseMap nachher auch weiß, wann die Messungen vorgenommen wurden. Das macht das folgende Programm:
{% include image.html image=page.image0 %}

Kompiliere es und lade es auf deine MCU hoch. **Dieser Schritt muss nur einmal gemacht werden, ab jetzt merkt sich die RTC die Zeit selbstständig**

