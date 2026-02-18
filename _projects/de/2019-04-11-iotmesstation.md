---
layout: project_page
title: "IoT Messstation"
date: 2019-05-17
author: Eric
abstract: "Erstelle eine Messstation, die Messwerte für Temperatur, Luftfeuchte, Niederschlagsmenge, Niederschlagsintensität, Luftdruck, Helligkeit und UV-Intensität an die openSenseMap schickt."
thumbnail: /images/projects/home.jpg
image1: /images/projects/iot_messstation/senseBox_Uebersicht.png
image2: /images/projects/iot_messstation/WiFi.png
image3: /images/projects/iot_messstation/upload_osem.svg
image0: /images/projects/iot_messstation/neueSenseBox.png
material:
  - senseBox MCU
  - 1x OLED Display
  - 1x Temperatur- und Luftfeuchtigkeitssensor
  - 1x Luftdrucksensor
  - 1x Niederschlagssensor
  - 1x Helligkeits- und UV-Sensor
  - 5x JST-Kabel
  - 1x Wifi-Bee
ide: blockly
lang: de
version: ["edu", "mini v1", "home"]
tags: ["Informatik", "Geographie", "IoT"]
difficult: mittel
---

# IoT Messstattion

Ziel dieses Projektes ist es, eine senseBox Umweltstation aufzubauen. Am Ende wird die Messung diverser Umweltphänomene wie Temperatur, Luftfeuchte, Niederschlagsmenge, Niederschlagsintensität, Helligkeit und Luftdruck, sowie die Veröffentlichung der Daten auf der openSenseMap möglich sein!

## Aufbau

Schließe die Sensoren deiner Wahl mithilfe der mitgelieferten JST-Kabel an die senseBox MCU an. Die meisten Sensoren werden über den I2C-Anschluss verbunden. Der Regensensor wird zunächst an die mitgelieferte Adapterplatine angeschlossen. Die Adapterplatine wird anschließend mithilfe eines JST-Kabels an den UART/Serial-Anschluss angeschlossen. Das Wifi-Bee wird auf den Steckplatz XBEE1 gesteckt.

Anders, als bei einfachen digitalen oder analogen Eingängen, können mehrere I2C-Geräte (wie z.B. Sensoren oder Displays) parallel geschaltet werden. Jedes Gerät hat dabei eine eindeutige Kennung, damit der Datenbus jedes Einzelne davon zuordnen und separat ansprechen kann.


## Vorbereitung

### Schritt 1: Registrierung auf der openSenseMap

Damit du die Werte deiner Messstation von überall aus abrufen kannst, können die Werte im Internet auf der [openSenseMap](https://www.opensensemap.org/) hochgeladen werden. Dafür muss ein Benutzerkonto auf ebendieser Plattform erstellt werden. Rufe die [openSenseMap](https://www.opensensemap.org/) in einem Internet-Browser auf. Klicke in der oberen Leiste auf den Menüpunkt "Registrierung". Fülle dort alle freien Felder aus. Achte darauf, deine E-Mail Adresse korrekt einzugeben, da du diese für die nächsten Schritte noch benötigst.

### Schritt 2: Anlegen einer neuen 'senseBox'

Ist die Registrierung abgeschlossen, melde dich an und wähle über das Dropdown Menü (siehe Bild) den Punkt "Neue senseBox" aus. Hier kannst du deiner Messstation einen Namen geben, eine Position angeben und die Phänomene, die du messen möchtest, bestimmen. Wichtig ist, dass du auch nur die Sensoren angibst, die du auch zur Verfügung hast. Nachdem das erledigt ist, siehst du eine Übersicht, in der dir deine registrierte senseBox mit den dazugehörigen Sensoren angezeigt wird.

{% include image.html image=page.image0 %}

<div class="panel panel-success">
  <div class="panel-heading">
  Sensor IDs: Die Sensor IDs können benutzt werden, um Sensoren zu unterscheiden. Jede senseBox und jeder Sensor, der auf der [openSenseMap] (https://www.opensensemap.org/) registriert ist, besitzt eine einzigartige ID. Beim Hochladen der Messwerte werden  diese IDs benötigt, damit die openSenseMap weiß, zu welchen Sensoren die Messwerte gehören
  </div>
</div>

{% include image.html image=page.image1 %}

## Programmierung

### Schritt 1: Anfang der Programmierung

Super, die Registrierung auf der [openSenseMap](https://www.opensensemap.org/) ist abgeschlossen! Nun kannst du dich der Programmierung widmen. Gehe hierfür auf die [Ardublockly](https://blockly.sensebox.de/ardublockly/?lang=de&board=sensebox-mcu) Seite oder nutze den [senseBox - Code Editor](https://blockly.sensebox.de/codeeditor). Der Umgang mit Ardublockly sollte dir aus vorherigen Anleitungen bekannt sein. Falls dem nicht so ist, besuche die [senseBox Go](https://sensebox.de/de/go-edu.html) Seite.
Im ersten Schritt wird eine Verbindung mit dem Internet über WiFi hergestellt. Hierfür brauchst du den Namen und das Passwort für das WLAN, welches du zum Datenupload benutzen möchtest. Die hierfür verwendeten Blöcke befinden sich in der Kategorie `Web`->`WiFi`.

{% include image.html image=page.image2 %}

### Schritt 2: Verbindung zur openSenseMap und hochladen der Messwerte

Hast du den korrekten Netzwerknamen und das Passwort eingegeben, kann nun eine Verbindung zur openSenseMap hergestellt werden. Damit es bei dieser Verbindung keine Probleme gibt, empfiehlt sich vor allem in der Schule die Verwendung eines mobilen Hotspots über das Smartphone. Dafür muss der Hotspot am Handy aktiviert und ebenfalls der Netzwerkname und das Passwort im vorgesehenen Feld in Blockly eingetragen werden. Um das Netzwerk nicht zu überlasten, werden die Messwerte alle 60 Sekunden übertragen. Den passenden Block hierfür findest du in der Kategorie `Zeit`. Ziehe diesen in die Endlosschleife und ändere das Messintervall zu 60000 Millisekunden. Nun soll alle 60 Sekunden eine Verbindung zur openSenseMap hergestellt werden. Den Block dafür findest du in der Kategorie `Web`-> `openSenseMap`. Ähnlich, wie bei der Verbindug über WiFi aus Schritt 1, musst du in diesem Block deine senseBox ID aus Schritt 2 der Vorbereitung angeben. In diesem Block kannst du nun alle Sensoren, die du registriert hast, angeben und somit hochladen. Dafür wird der Block `Sende Messwerte an die openSenseMap` aus der Kategorie `Web`-> `openSenseMap` benötigt. An diesen Block kann nun der Wert für den Sensor aus der Kategorie `Sensoren` eingefügt werden.
Abhängig davon, welche Blockly-Version du nutzt, muss zusätzlich der API-Schlüssel angegeben werden. Dieser ist unter dem Punkt "Sicherheit" zu finden, wenn du deine senseBox über den Button im Dashboard editierst. 

{% include image.html image=page.image3 %}

Wichtig! Achte auch hier darauf, dass du die Sensor IDs in den Block `Sende Messwerte an die openSenseMap` einfügst.

### Schritt 3: Code übertragen

Übertrage den Code auf die senseBox, wie auf [senseBox Go](https://sensebox.de/de/go-edu.html) beschrieben.

### Schritt 4: Fertig!

Herzlichen Glückwunsch! Du hast eine eigene Messstation programmiert. Für was du die senseBox sonst noch benutzen kannst, erfährst du in anderen spannenden [Projekten](https://sensebox.de/de/projects.html).

## Gesamter Code

Die fertigen Blockly Blöcke findest du [hier](https://blockly.sensebox.de/gallery/620ba2e5830e5000189b8d74).
