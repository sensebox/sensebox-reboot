---
layout: post
title: "Die neue senseBox MCU mini ist da!"
date: 2023-06-25
author: Gina
abstract: "Die senseBox MCU mini ist eine miniaturisierte Version der senseBox MCU. Auch mit diesem kleinen Board können viele Experimente und Projekte umgesetzt werden."
thumbnail: /images/blog/senseBox_MCU_mini.jpg 
image1: /images/blog/senseBox_MCU_mini_1.jpg
image2: /images/blog/senseBox_MCU_mini_2.jpg
lang: de
tag: News
---

# Was ist die senseBox MCU mini und wie kann sie eingesetzt werden?

Die neue senseBox MCU mini ist eine miniaturisierte Version der senseBox MCU. Wie der Name schon sagt, ist sie besonders klein und damit ein kompaktes Messgerät. Sie ist etwa so groß wie das Display und somit auch hervorragend für mobile Messungen geeignet.

{% include image.html image=page.image1 %}
{% include image.html image=page.image2 %}

## Technisches

Die Architektur basiert auf dem bekannten SAMD21 Prozessor. Zur Datenübertragung steht ein XBee-Slot zur Verfügung, kompatibel mit allen unseren Verbindungsmodulen, sowie ein Mikro-SD Steckplatz on board. Bei den Anschlüssen setzen wir auf das neue QWICC-System, womit alle unsere Sensoren zukünftig ausgestattet sein werden.

### Prozessor

Als Prozessor kommt ein ATSAMD21G18, basiert auf dem ARM Cortex-M0+ Prozessor der SAM D21 Familie von Microchip, zum Einsatz.

### Anschlüsse

Die Steckerbuchsen basieren auf dem QWIIC-System (JST SH4). Für Sensoren und Aktoren sind folgende Anschlüsse zu Hardwareschnittstellen verfügbar: Folgende Anschlüsse sind verfügbar:

    2*I2C
    1*UART
    1*I/O (mit zwei analogen/digitalen PINs, sowie 5V und GND)
    1*Lüfteranschluss (5V)

### Datenübertragung

Über den XBee kompatiblen Sockel werden UART oder SPI Module angeboten. Wahlweise kann die Datenübertragung dadurch per WLAN, LAN, LoRa oder Bluetooth in Echtzeit durchgeführt werden. Alternativ können die Daten auf einer Mikro-SD Karte abgespeichert werden.


## Programmierung

Die Programmierung des Messgerätes kann in unserer grafischen [Programmier- und Lernumgebung](https://blockly.sensebox.de/) durchgeführt werden. Wie die Programmierung in Blockly funktioniert, erfährst du [hier](https://sensebox.de/projects/de/2022-12-19-messstation-mini). Die Programmierung in Arduino ist äquivalent zur „normalen“ [senseBox MCU](https://docs.sensebox.de/category/arduino/).

Mehr dazu erfährst du auch in unserer [Anleitung](https://docs.sensebox.de/hardware/allgemein-sensebox-mcu-mini/). 

## Shop

Die senseBox MCU mini ist als Bausatz der [senseBox:mini V2](https://sensebox.kaufen/product/sensebox-mini-v2) oder einzeln als [Board](https://sensebox.kaufen/product/sensebox-mcu-mini) erhältlich!
