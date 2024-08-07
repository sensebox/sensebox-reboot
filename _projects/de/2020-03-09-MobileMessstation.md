---
layout: project_page
title: "Mobiler Datenlogger"
date: 2023-05-11
author: Mario
abstract: "Ein mobiler Datenlogger, der die Daten per WLAN an die openSenseMap sendet"
thumbnail:  /images/projects/MobilerDatenlogger.png
image0: /images/projects/mobile_feinstaubstation/wifi/AnlegenVariablen.png
image1: /images/projects/mobile_feinstaubstation/wifi/ZeigeDisplay.png
image2: /images/projects/mobile_feinstaubstation/wifi/RegistrierungOSEM.png
image3: /images/projects/mobile_feinstaubstation/wifi/SendeOSEM.png
material:
    - senseBox MCU
    - 1x OLED Display
    - 1x Temperatur und Luftfeuchtesensor (HDC 1080)
    - 1x Feinstaubsensor (SDS011 oder SPS30) inkl. Kabel
    - 1x GPS Modul
    - 1x WiFi-Bee
    - 2x JST-JST Kabel
ide: blockly
version: ["edu", "mini v1", "home"]   
addons: ["GPS", "Feinstaubsensor"] 
lang: de
tags: ["Informatik","Geographie"]
difficult: schwer
---
<head><title>Mobiler Feinstaublogger mit GPS</title></head>

# Mobiler Datenlogger für Feinstaubwerte
In diesem Projekt wird mit der senseBox ein mobiler Datenlogger gebaut, der die Messwerte über WLAN, mithilfe eines Handyhotspot, direkt an die openSenseMap überträgt. Der aktuelle Standort wird über das GPS-Modul bestimmt und zusätzlich zu den Messwerten übertragen. Solltest du kein GPS-Modul zur Verfügung haben, kannst du deine senseBox auch als stationäre Messstation auf der openSensemap registrieren und das Projekt trotzdem durchführen.  

## Aufbau
Stecke das WiFi-Bee auf den Steckplatz __XBEE1__. 
Das OLED Display, der Temperatur- und Luftfeuchtesensor und das GPS Modul werden mit jeweils einem JST-JST Kabel an die I2C Ports angeschlossen. Der Feinstaubsensor (SDS011) mit dem JST-Feinstaubkabel an einen der beiden Serial/UART Ports. Solltest du den Feinstaubsensor SPS30 nutzen, verbinde diesen ebenfalls mit einen der fünf I2C Ports.

## Registrierung auf der openSenseMap

Die Registrierung erfolgt auf der openSenseMap. Wähle dort als __Aufstellungsort__ **mobil** und lege einen ersten Standort fest (dieser wird nur für den Start benötigt). Wähle als Modell die senseBox:edu und füge die Messwerte für Temperatur, Luftfeuchtigkeit, Feinstaub (PM2.5) und Feinstaub (PM10) aus. 

 {% include image.html image=page.image2 %}

## Programmierung

Die Programmierung des Mobilen Datenlogger wird in [Blockly](https://blockly.sensebox.de) durchgeführt. Im ersten Schritt werden die Messwerte ausgelesen und als Variable gespeichert. Die Messwerte werden auf dem Display angezeigt und anschließend im Abstand von 10 Sekunden an die openSenseMap übertragen.

### Schritt 1: Auslesen der Sensoren und Anlegen der Variablen

Um die Messwerte der Sensoren nicht nur auf dem Display anzeigen zu lassen sondern auch in regelmäßigen Abständen an die openSenseMap zu versenden, werden diese zu Begin der Endlosschleife ausgelesen und in einer Variablen gespeichert. Lege für jeden Messwert eine neue Variable an und geben ihr einen sinnvollen Namen. 


{% include image.html image=page.image0 %}

### Schritt 2: Anzeigen der Messwerte auf dem Display

Initialisiere das Display im Setup() und füge den Block __Zeige auf dem Display__ in die Endlosschleife ein. Mit den Block __Schreibe Text/Zahl__ kannst du die jeweiligen Messwerte auf dem Display anzeigen lassen. Um mehrere Messwerte auf dem Display anzuzeigen, musst du jeweils die Platzierung (Verschiebung auf der Y-Achse) auf dem Display anpassen.


 {% include image.html image=page.image1 %}

Übertrage den Programmcode und überprüfe auf dem Display ob alle Messwerte korrekt angezeigt werden. 

### Schritt 3: Übertragen der Messwerte an die openSenseMap

Um Messwerte an die openSenseMap zu übertragen, muss eine Internetverbindung hergestellt werden. Da in diesem Projekt eine mobile Messstation gebaut wird ist es am einfachsten, den Hotspot deines Handy zu verwenden. 
Damit die Messwerte nicht jede Sekunde an die openSenseMap übertragen werden, ziehe zuerst den Block 'Messintervall' unter die Blöcke für das Display. (Tip: Mit einem Rechtsklick auf den Block __Zeige auf dem Display__ und der Option __Block zusammenfalten__ kannst du Platz sparen).
In den offenen Blockabschnitt wird nun der Block zum Verbinden mit der openSenseMap gezogen. Wähle in diesem Block als __Typ__ **Mobil** aus und kopiere deine senseBox ID, die du nach der Registrierung von der openSenseMap erhalten hast. Füge zudem den API-Schlüssel ein, der unter dem Punkt 'Sicherheit' zu finden ist, wenn du deine senseBox auf der openSenseMap editierst. 

Für jeden Messwert, den du nun senden möchtest, ziehe einen Block __Sende Messwert an die openSenseMap__ in den offenen Blockabschnitt, trage die entsprechenden Sensor ID's ein und verbinde den Block mit dem entsprechenden Messwert.

Damit die gemessenen Messwerte immer mit dem aktuellen Standort verknüpft werden, müssen 4 verschiedene Parameter vom GPS Modul abgefragt werden. Neben dem Längen und Breitengrad wird auch die Höhe über NN und ein Zeitstempel im RFC 3339 Format übertragen. 

## Gesamter Code

 {% include image.html image=page.image3 %}

 [Hier](https://blockly.sensebox.de/gallery/63b6d1b3d2853f0013b1da7f) findest du den gesamten Blockly-Code für die Verwendung des Feinstaubsensors SDS011.
 [Hier](https://blockly.sensebox.de/gallery/645ca8a8e20614001a3ff659) findest du den gesamten Blockly-Code für die Verwendung des Feinstaubsensors SPS30. Er hat den Vorteil, dass du neben PM2.5 und PM10 auch weitere Partikelgrößen (PM1.0, PM4.0) messen kannst.  


Beachte, dass das GPS Modul nach dem ersten Anschließen unter Umständen sehr lange benötigt, um ein erstes Standortsignal zu bekommen. Lege dazu die Box nach draußen und achte darauf, dass keine Gegenstände, wie Dächer oder Bäume, den Blick in den Himmel versperren.

