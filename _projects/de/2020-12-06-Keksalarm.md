---
layout: project_page
title: "Keksalarm"
date: 2020-12-06
author: Verena
abstract: "Kreiere eine Alaramanlage, um deine Kekse vor Dieben zu schützen"
thumbnail:  /images/projects/Titelbild_Keksalarm.png
image0: /images/projects/Keksalarm/0.png
image1: /images/projects/Keksalarm/1.png
image2: /images/projects/Keksalarm/2.png
image3: /images/projects/Keksalarm/3.png

material:
    - senseBox MCU
    - 1x OLED-Display
    - 1x JST-JST-Kabel
    - 2x JST-Adapterkabel
    - 1x Piezo
    - 1x Ultraschalldistanzsensor
    - 1x Keksdose
    
ide: blockly
version: ["edu", "mini"]   
addons: ["Weihnachten"] 
lang: de
tags: ["Informatik"]
difficult: mittel
---
<head><title>Keksalarm</title></head>

# Eine Alarmanlage kreieren, die deine Kekse vor Dieben schützt
Am zweiten Advent liegt der Duft von frisch gebackenen Plätzchen in der Luft. Damit du dir sicher sein kannst, dass niemand Umbefugtes die Keksdose öffnet, erstellen wir in diesem Projekt eine kleine Alarmanlage. Diese ist ausgestattet mit einem Ultraschalldistanzsensor und einem Piezo. Das Ziel ist es also, dass ein hörbares Signal ausgelöst wird, sobald der Deckel deiner Keksdose geöffnet wird. 

## Aufbau
Der Ultraschallsensor wird auf das Breadboard gesteckt und mit Hilfe des Adapterkabels an einem der drei Digital/Analog-Ports angeschlossen. Das schwarze Kabel wird mit dem GND Pin des Sensors, das rote Kabel mit dem VCC Pin, das grüne mit dem ECHO Pin und das gelbe mit dem TRIG Pin verbunden. Die Pins des Sensors sind auf seiner Vorder- und Rückseite beschriftet. Am besten schließt du den Sensor so an, dass die Kabel hinter dem Sensor liegen, da sie sonst die Messungen verfälschen können. Der Piezo wird ähnlich wie eine einfarbige LED angeschlossen. Das kürzere Beinchen wird mit dem Minuspol (schwarzes Kabel) und das längere Beinchen mit einem digitalen Pin (grünes oder gelbes Kabel) verbunden. Du kannst einen Widerstand vorschalten, dies ist aber nicht nötig und führt nur dazu, dass der Piezo leiser wird. Zudem bietet es sich an, das Display anzuschließen, damit dir die Abstandswerte des Ultraschalldistanzsensors angezeigt werden können. Verwende dafür das JST-JST-Kabel und verbinde es mit einem I2C/Wire-Steckplatz.

{% include image.html image=page.image0 %}

Wie genau du den Ultraschalldistanzsensor anbringst, ist von deiner Keksdose abhängig. Beispielswiese könntest du ihn unter dem Deckel kleben, sodass die Alarmanlage anspringt, sobald sich der Abstand zwischen Deckel und Inhalt bzw. Dosenboden vergrößert.

## Programmierung

Das Ziel der Programmierung ist es, dass der Piezo zu piepen beginnt, sobald der vom Ultraschalsensor gemessene Abstand einen Grenzwert übererschreitet. Dieser soll zudem auf dem Display angezeigt werden.

### Schritt 1: Messwerte auf dem Display anzeigen lassen

Um Werte auf dem Display anzeigen lassen zu können, muss dies zuerst im Setup() initialisiert werden. Da du in diesem Programm viel mit dem Abstand zwischen Dosendeckel und Dosenboden arbeiten wirst, empfiehlt es sich, hierfür eine Variable in der Endlosschleife anzulegen. Dafür benötigst du die Blöcke 'Schreibe Element' aus der Kategorie 'Variablen' sowie den passenden Block zum Ultraschalldistanzsensor. Bei letzterem solltest du beachten, dass der richtige Port (A, B oder C) ausgewählt ist. Diesen findest du bei den Digital-Anschlüssen auf der senseBox MCU. Anschließend verwendest du noch die Blöcke 'Zeige auf dem Display' und 'Schreibe Text/ Zahl', um den Abstand auf dem Display anzeigen zu lassen.  

{% include image.html image=page.image1 %}

### Schritt 2: Alarmanlage einschalten

In unserem Fall wird der Ultraschall-Distanzsensor mit der senseBox MCU unter dem Keksdeckel befestigt, sodass der Alarm losgehen soll, falls der Abstand zwischen Deckel und Dosenboden größer ist als die gesamte Höhe der Keksdose (20 cm). Dafür verwenden wir eine 'wenn...mache' Bedingung, in der wir die vorherige Aussage integrieren. Damit der Piezo ein Piepen und keinen durchgängigen Ton ausgibt, muss ein 'Warte-Block' aus der Kategorie 'Zeit' verwendet werden. Dadurch wird der Piezo dann in regelmäßigen Abständen ein- und ausgeschaltet. Des Weiteren kannst du neben dem Abstand in cm zusätzlich einen beliebigen Text anzeigen lassen, der den Keksdieb dazu auffordert, lieber keinen deiner Kekse zu essen. 

{% include image.html image=page.image2 %}

### Schritt 3: Alarmanlage ausschalten
Bisher wird die Alarmanlage nur eingeschaltet und nicht wieder ausgeschaltet. Damit letzteres auch geschieht, kannst du die 'wenn...mache'-Bedingung durch einen Klick auf das Zahnrädchen um ein 'sonst' erweitern. Das beschriebt dann den Fall, wenn sich der Abstand nicht verändert und deine Kekse in Sicherheit sind. Hier sollte sowohl der Piezo ausgeschaltet als auch auf dem Display Entwarnung gegeben werden. Damit ist die Programmierung abgeschlossen.

{% include image.html image=page.image3 %}

In diesem Sinne wünschen wir euch einen schönen zweiten Advent und viel Spaß bei der Durchführung des Projekts! 