---
layout: project_page
title: "Einparkhilfe"
date: 2019-12-11
author: Björn
abstract: "Die Einparkhilfe, die jeder aus dem Auto kennt."
thumbnail: /images/projects/Titelbild_Einparkhilfe.jpg
image0: /images/projects/Einparkhilfe/Einparkhilfe_Aufbau.png
image1: /images/projects/Einparkhilfe/Schritt1.png
image2: /images/projects/Einparkhilfe/Schritt2.png
image3: /images/projects/Einparkhilfe/Schritt3.png
imageSolution: /images/projects/Einparkhilfe/Loesung.png
material:
    - senseBox MCU
    - 1x OLED-Display
    - 1x Ultraschall-Distanzsensor
    - 1x Piezo/ Summer
    - 1x JST-Adapterkabel
    - 1x JST-JST-Kabel
ide: blockly
lang: de
version: edu
tags: ["Informatik"]
difficult: mittel
---
# Einparkhilfe {#head}

Das Auto rückwärts einzuparken kann eine schwierige Sache sein. Mit einen
Parksensor im Auto wird es jedoch deutlich leichter. Aber wie funktioniert ein solcher
Helfer?

## Aufbau 
Der Ultraschallsensor wird auf das Breadboard gesteckt und mit Hilfe des Adapterkabels
an einen Digital/Analog Port angeschlossen. Das schwarze Kabel wird mit dem GND Pin
des Sensors, das rote Kabel mit dem VCC Pin, das grüne mit dem ECHO Pin und das gelbe
mit dem TRIG Pin verbunden. Die Pins des Sensors sind auf seiner Vorder- und Rückseite
beschriftet. Am besten schließt du den Sensor so an, dass die Kabel hinter dem Sensor
liegen, da sie sonst die Messungen verfälschen können.
Der Piezo wird ähnlich wie eine einfarbige LED angeschlossen. Das kürzere Beinchen
wird mit dem Minuspol (schwarzes Kabel), das längere Beinchen mit einem digitalen Pin
(grünes oder gelbes Kabel) verbunden. Du kannst einen Widerstand vorschalten, dies ist
aber nicht nötig und führt nur dazu, dass der Piezo leiser wird.
{% include image.html image=page.image0 %}

## Programmierung
Das Ziel der Programmierung ist es, eine Einparkhilfe zu kreieren, die umso schneller piept, je näher das Auto an einen Gegenstand heranfährt.

### Schritt 1

Um nun eine Einparkhilfe zu programmieren solltest du dir als ersten Schritt die Messwerte
des Ultraschallsensors auf dem Display anzeigen lassen. So kannst du nachher
besser einschätzen, welche Abstände für deinen Parkhelfer passend sind. Außerdem
macht die Arbeit in kleinen Schritten die Fehlersuche deutlich leichter. Verwende dafür eine Variable, die du als bei der Erstellung 'int' definieren musst.
Um dir die Messwerte anzeigen zu lassen, benötigst du folgende Blöcke:

{% include image.html image=page.image1 %}

### Schritt 2

Wenn dir nun die Messwerte angezeigt werden, folgt der nächste Schritt. Du musst Entscheidungen
hinzufügen, die festlegen, wie schnell bei welcher Entfernung gepiept werden soll.
Umgesetzt wird dies mit dem „wenn...mache“ Block aus der Kategorie Logik.
Als erstes fängst du am besten mit einer einzelnen Bedingung an, die den Piezo dann piepen lässt, 
wenn die gemessene Distanz kleiner als 10cm ist.

{% include image.html image=page.image2 %}

### Schritt 3
Nun musst du noch weitere Entscheidungen hinzufügen, sodass sich die Frequenz des
Piepens je nach Entfernung verändert. Dazu kannst du mit dem Zahnrädchen oben links im „wenn
mache“ Block weitere Entscheidungen hinzufügen. In diesen solltest du dann die Wartezeit
nach dem Piepen, sowie die jeweilige Distanz anpassen. Außerdem brauchst du
noch den „und“ Block aus der Kategorie Logik, um für die mittlere und letzte Bedingung die Anfags- und Enddistanz festzulegen. Am Ende muss der Piezo ausgeschaltet werden, wenn das Auto weit genug von einem Gegenstand entfernt ist. 

{% include image.html image=page.image3 %}

### Fertiger Code
Den gesamten Code in Blockly findest du [hier](https://blockly.sensebox.de/gallery/63bbe977d2853f0013b1df78). 



