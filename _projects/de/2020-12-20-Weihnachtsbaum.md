---
layout: project_page
title: "Intelligenter Weihnachtsbaum"
date: 2020-12-20
author: Verena
abstract: "Überprüfe die Versorgung deines Weihnachtsbaums mit der senseBox"
thumbnail:  /images/projects/Titelbild_Weihnachtsbaum.png
image0: /images/projects/Weihnachtsbaum/0.png
image1: /images/projects/Weihnachtsbaum/1.png
image2: /images/projects/Weihnachtsbaum/2.png
image3: /images/projects/Weihnachtsbaum/3.png

material:
    - senseBox MCU
    - OLED-Display
    - 2x JST-JST-Kabel
    - 1x JST-Adapterkabel
    - 1x Bodenfeuchtesensor
    - 1x Temperatursensor (HDC1080)
    - 1x 470Ω Widerstand
    - 1x RGB-LED
    
ide: blockly
version: ["edu", "mini"]   
addons: ["Weihnachten"] 
lang: de
tags: ["Informatik", "Biologie"]
difficult: mittel
---
<head><title>Intelligenter Weihnachtsbaum</title></head>

# Überprüfe die Versorgung deines Weihnachtsbaums mit der senseBox
Weihnachten rückt immer näher und damit auch die Zeit, den Weihnachtsbaum aufzustellen. Damit dieser möglichst lange schön bleibt und keine Nadeln verliert, ist es besonders wichtig, die richtigen Voraussetzungen zu schaffen. Dazu gehören eine ausreichende Wasserversorgung sowie eine angemessene Raumtemperatur. Die senseBox hilft dir dabei, diese beiden Phänomene zu überwachen, sodass du möglichst lange die Schönheit deines Weihnachtsbaums genießen kannst.

## Aufbau
Zuerst verbindest du das Display mit dem JST-JST-Kabel. Dies schließt du an einem der fünf I2C/Wire-Anschlüsse deiner senseBox MCU an. Ebenso verbindest du den Temperatursensor mit deiner senseBox MCU. Der Bodenfeuchtesensor wird hingegen an einem der drei Digital-Ports angeschlossen. Je nachdem, welchen du wählst, solltest du den Port (A, B oder C) in Blockly anpassen. Um die RGB-LED zum Leuchten bringen zu können, benötigst du die restlichen Komponenten. Die untenstehende Abbildung zeigt dir detailliert, wie der Aufbau aussehen sollte. Dabei ist es wichtig zu beachten, dass die langen Beinchen der LED jeweils mit dem roten und schwarzen Kabel verbunden werden sowie das kurze Beinchen mit einem Widerstand und einem grünen oder gelben Kabel. Als Anschluss auf der senseBox wählst du wieder einen Digital-Port aus. Die kleinen Ziffern an der Stelle des grünen oder gelben Kabels zeigen dir, welchen digitalen Pin du in Blockly auswählen solltest. 

{% include image.html image=page.image0 %}

## Programmierung

Das Ziel der Programmierung ist es, dass die RGB-LED je nach Wasserstand im Tannenbaumständer die Farbe von grün über gelb zu rot wechselt und auf dem Display die Wasserversorgung sowie die Temperatur angezeigt wird.

### Schritt 1: Display initialisieren und Variablen definieren
Zu Beginn solltest du im Setup() das Display initialisieren, damit dort anschließend die Messwerte angezeigt werden können. Danach werden in der Endlosschleife zwei Variablen definiert: Zum einen die Variable 'Wasserversorgung', die mithilfe des Bodenfeuchtesensors den Wassergehalt im Tannenbaumständer angibt. Hier wird als Einheit der volumetrische Wassergehalt verwendet und Prozente zwischen 0 und 50 ausgegeben. Wir messen hier keinen Anteil von Wasser beispielsweise im Boden, sondern den Wasserstand. Daher ist es wichtig, den Sensor senkrecht zu platzieren, sodass sich die Spitze etwa am Ende des Tannenbaumstamms befindet. Je niedriger der Wasserstand ist, desto niedriger ist folglich auch der Wert, der gemessen wird, da der Sensor dann nicht mehr komplett von Wasser umgeben ist. Je nach Wasserstand wechselt die RGB-LED mit dem folgeden Programmcode die Farbe von grün über gelb zu rot. Zum anderen gibt es die Variable 'Temperatur', die die Temperatur der Umgebungsluft in Grad Celsius misst. Sie dient dazu, den Tannenbaum vor zu großer Hitze zu schützen und dich darauf aufmerksam zu machen, eventuell die Heizung etwas runter zu drehen, falls es zu warm ist.   

{% include image.html image=page.image1 %}

### Schritt 2: Anzeige auf dem Display

Die Generierung der Anzeige auf dem Display startet mit dem Block 'Display löschen', damit alle Informationen durchlaufend korrekt angezeigt werden. Verwende anschließend die Blöcke 'Zeige auf dem Display' und 'Schreibe Text Zahl'. Hier kannst du durch einen Klick auf das Zahnrädchen weitere Elemente hinzufügen, sodass du 'Wert' sowohl die Wasserversorgung als auch die Temepratur mithile eines Textbausteins und der jeweiligen Variabel angezeigt werden.  

{% include image.html image=page.image2 %}

### Schritt 3: Die 'wenn...mache'-Bedingung
Je nach Wasserstand soll die RGB-LED in einer anderen Farbe leuchten. Dafür musst du die 'wenn...mache'-Bedingung verwenden und diese um zwei 'sonst wenn...mache'-Elemente erweitern. Im ersten und besten Fall ist der Tannenbaumständer mit genügend Wasser gefüllt und die RGB-LED leuchtet grün. Im zweiten Fall befindet sich noch etwas Wasser im Tannenbaumständer, allerdings könnte dies bald verbraucht sein, weshalb die RGB-LED gelb leuchtet. Im letzten und schlechtesten Fall befindet sich fast gar kein Wasser mehr im Tannenbaumständer, weshalb die senseBox dich mit einer roten RGB-LED und einer Anzeige auf dem Display warnt.   

{% include image.html image=page.image3 %}

Wir hoffen, dass dir dieses Projekt dabei hilft, deinen Weihnachtsbaum optimal versorgen zu können und wünschen dir somit einen schönen 4. Advent und wunderbare Weihnachtstage!