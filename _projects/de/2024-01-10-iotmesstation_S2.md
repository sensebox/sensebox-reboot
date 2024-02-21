---
layout: project_page
title: "IoT Messtation"
date: 2024-01-10
author: Verena
abstract: "Erstelle eine Messtation, die Messwerte für Temperatur, Luftfeuchte, Luftdruck, Helligkeit und UV-Intensität an die openSenseMap schickt."
thumbnail: /images/projects/home.jpg
image0: /images/projects/iot_messstation_S2/0.png
image1: /images/projects/iot_messstation_S2/1.png
image2: /images/projects/iot_messstation_S2/2.png
image3: /images/projects/iot_messstation_S2/3.png
image4: /images/projects/iot_messstation_S2/4.png
image5: /images/projects/iot_messstation_S2/5.png
material:
  - senseBox MCU-S2
  - 1x OLED Display
  - 1x Temperatur- und Luftfeuchtigkeitssensor
  - 1x Luftdrucksensor
  - 3x QWICC-Kabel 
ide: blockly
lang: de
version: ["edu-S2"]
tags: ["Informatik", "Geographie", "IoT"]
difficult: mittel
---

# IoT Messstattion

Ziel dieses Projektes ist es, eine senseBox Umweltstation aufzubauen. Am Ende wird die Messung diverser Umweltphänomene wie Temperatur, Luftfeuchte, Helligkeit und Luftdruck, sowie die Veröffentlichung der Daten auf der openSenseMap möglich sein!

## Aufbau

Schließe das Display und die Sensoren deiner Wahl mithilfe der QWICC-Kabel an den I2C-Anschlüssen der senseBox MCU-S2 an. Du hast nur zwei Anschlüsse, aber drei Sensoren - mithilfe eines QWIIC-Kabels kannt du beispielsweise den Luftdrucksensor an den QWIIC-Anschluss des Temperatur- und Luftfeuchtesensors anschließen. Die Photodiode zur Messung der Beleuchtungsstärke und das WiFi-Modul sind direkt auf dem Board integriert und müssen nicht zusätzlich angeschlossen werden.


<div class="panel panel-success">
  <div class="panel-heading">
    I2C Anschluss
  </div>
  <div class="panel panel-success">
    <div class="panel-body">
    Die Kommunikation des Sensors mit dem Mikrocontroller läuft über den seriellen Datenbus I²C. Anders, als bei einfachen digitalen oder analogen Eingängen, können an den Datenbus mehrere I²C-Geräte (wie z.B. Sensoren oder Displays) parallel geschaltet werden. Jedes Gerät hat dabei eine eindeutige Kennung, damit der Datenbus jedes Einzelne davon zuordnen und separat ansprechen kann.
    </div>
  </div>
</div>

{% include image.html image=page.image0 %}

## Vorbereitung

### Schritt 1: Registrierung auf der openSenseMap

Damit du die Werte deiner Messstation von überall aus abrufen kannst, können die Werte im Internet auf der [openSenseMap](https://www.opensensemap.org/) hochgeladen werden. Dafür muss ein Benutzerkonto auf ebendieser Plattform erstellt werden. Rufe die [openSenseMap](https://www.opensensemap.org/) in einem Internet-Browser auf. Klicke in der oberen Leiste auf den Menüpunkt "Registrierung". Fülle dort alle freien Felder aus. Achte darauf, deine E-Mail Adresse korrekt einzugeben, da du diese für die nächsten Schritte noch benötigst.

{% include image.html image=page.image1 %}

### Schritt 2: Anlegen einer neuen 'senseBox'

Ist die Registrierung abgeschlossen, melde dich an und wähle über das Dropdown Menü (siehe Bild) den Punkt "Neue senseBox" aus. Hier kannst du deiner Messstation einen Namen geben, eine Position angeben und die Phänomene, die du messen möchtest, bestimmen. Wichtig ist, dass du auch nur die Sensoren angibst, die du auch zur Verfügung hast. Nachdem das erledigt ist, siehst du eine Übersicht, in der dir deine registrierte senseBox mit den dazugehörigen Sensoren angezeigt wird.

<div class="panel panel-success">
  <div class="panel-heading">
  Sensor IDs: Die Sensor IDs können genutzt werden, um Sensoren zu unterscheiden. Jede senseBox und jeder Sensor, der auf der [openSenseMap](https://www.opensensemap.org/) registriert ist, besitzt eine einzigartige ID. Beim Hochladen der Messwerte werden diese IDs benötigt, damit die openSenseMap weiß, zu welchen Sensoren die Messwerte gehören.
  </div>
</div>

{% include image.html image=page.image2 %}

## Programmierung

### Schritt 1: Anfang der Programmierung

Super, die Registrierung auf der [openSenseMap](https://www.opensensemap.org/) ist abgeschlossen! Nun kannst du dich der Programmierung widmen. Gehe hierfür auf die [Blockly](https://blockly.sensebox.de) Seite oder nutze den [senseBox - Code Editor](https://blockly.sensebox.de/codeeditor). Der Umgang mit Blockly sollte dir aus vorherigen Anleitungen bekannt sein. Falls dem nicht so ist, besuche die [senseBox Go](https://sensebox.de/go) Seite.
Im ersten Schritt wird eine Verbindung mit dem Internet über WiFi hergestellt. Hierfür brauchst du den Namen und das Passwort für das WLAN, welches du zum Datenupload benutzen möchtest. Die hierfür verwendeten Blöcke befinden sich in der Kategorie `Web`->`WiFi`.

{% include image.html image=page.image3 %}

### Schritt 2: Verbindung zur openSenseMap und hochladen der Messwerte

Hast du den korrekten Netzwerknamen und das Passwort eingegeben, kann nun eine Verbindung zur openSenseMap hergestellt werden. Damit es bei dieser Verbindung keine Probleme gibt, empfiehlt sich vor allem in der Schule die Verwendung eines mobilen Hotspots über das Smartphone. Dafür muss der Hotspot am Handy aktiviert und ebenfalls der Netzwerkname und das Passwort im vorgesehenen Feld in Blockly eingetragen werden. Um das Netzwerk nicht zu überlasten, werden die Messwerte alle 60 Sekunden übertragen. Den passenden Block hierfür findest du in der Kategorie `Zeit`. Ziehe diesen in die Endlosschleife und ändere das Messintervall zu 60000 Millisekunden. Nun soll alle 60 Sekunden eine Verbindung zur openSenseMap hergestellt werden. Den Block dafür findest du in der Kategorie `Web`-> `openSenseMap`. Ähnlich, wie bei der Verbindug über WiFi aus Schritt 1, musst du in diesem Block deine senseBox ID aus Schritt 2 der Vorbereitung angeben. In diesem Block kannst du nun alle Sensoren, die du registriert hast, angeben und somit hochladen. Dafür wird der Block `Sende Messwerte an die openSenseMap` aus der Kategorie `Web`-> `openSenseMap` benötigt. An diesen Block kann nun der Wert für den Sensor aus der Kategorie `Sensoren` eingefügt werden.
Abhängig davon, welche Blockly-Version du nutzt, muss zusätzlich der API-Schlüssel angegeben werden. Dieser ist unter dem Punkt "Sicherheit" zu finden, wenn du deine senseBox über den Button im Dashboard editierst. 

{% include image.html image=page.image4 %}

Wichtig! Achte auch hier darauf, dass du die Sensor IDs in den Block `Sende Messwerte an die openSenseMap` einfügst.

### Schritt 3: Anzeige der Messwerte auf dem Display

Um zu überprüfen, ob alle Sensoren plausible Werte messen, kann zusätzlich eine Anzeige der Messwerte auf dem Display programmiert werden. Dafür muss zunächst das Display im Setup initialisiert werden. 
Anschließend wird mit den Blöcken 'Zeige auf dem Display' und 'Zeige Messwerte' gearbeitet. Letzterer formatiert die Anzeige automatisch und du musst in den Lücken ausschließlich die Beschriftung des Messwerts, den verwendeten Sensor und die dazugehörige Einheit angeben. In diesem Fall passen nur zwei Messwerte gleichzeitig auf das Display, daher kannst du den 'Display löschen'-Block und einen 'Warte'-Block aus der Katgeorie Zeit verwenden, um die Anzeige nach beispielsweise 5 Sekunden wechseln zu lassen. Für die Anzeige der nächsten zwei Messwerte verwendest du die gleichen Blöcke nochmal. 

{% include image.html image=page.image5 %}

### Schritt 3: Code übertragen

Übertrage den Code auf die senseBox, wie auf [senseBox Go](https://sensebox.de/de/go-edu.html) beschrieben.

### Schritt 4: Fertig!

Herzlichen Glückwunsch! Du hast eine eigene Messstation programmiert. Für was du die senseBox sonst noch nutzen kannst, erfährst du in anderen spannenden [Projekten](https://sensebox.de/de/projects.html).

## Gesamter Code

Den fertigen Blockly-Code findest du [hier](https://blockly.sensebox.de/gallery/620ba2e5830e5000189b8d74).
