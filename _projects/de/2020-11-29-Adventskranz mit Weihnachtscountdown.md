---
layout: project_page
title: "Advendtskranz mit Weihnachtscountdown"
date: 2020-11-29
author: Verena
abstract: "Erstelle einen automatischen Adventskranz mit der senseBox"
thumbnail:  /images/projects/Titelbild_Adventskranz.png
image0: /images/projects/Adventskranz/0.png
image1: /images/projects/Adventskranz/1.png
image2: /images/projects/Adventskranz/2.png
image3: /images/projects/Adventskranz/3.png
image4: /images/projects/Adventskranz/4.png

material:
    - senseBox MCU
    - OLED-Display
    - 1x JST-JST-Kabel
    - 2x JST-Adapterkabel
    - 3x Steckkabel
    - 4x 470Ω Widerstand
    - 4x LED (gelb)
    
ide: blockly
version: ["edu", "mini"]   
addons: ["Weihnachten"] 
lang: de
tags: ["Informatik"]
difficult: mittel
---
<head><title>Advendtskranz mit Weihnachtscountdown</title></head>

# Einen automatischen Adventskranz mit Weihnachtscountdown erstellen
Um zusammen mit euch in die Weihnachtszeit zu starten, zeigt euch dieses Projekt, wie ihr mithilfe der senseBox einen automatischen Adventskranz mit integriertem Weihnachtscountdown generieren könnt. Die verwendeten LEDs schalten sich an jedem Adventssonntag automatisch ein und auf dem Display ist zu sehen, wie viele Tage bis Weihnachten verbleiben. 

## Aufbau
Zuerst verbindest du das Display mit dem JST-JST-Kabel. Dies schließt du an einem der fünf I2C/Wire-Anschlüssen deiner senseBox MCU an. Um die LEDs zum Leuchten bringen zu können, benötigst die restlichen Komponenten. Die untenstehende Abbildung zeigt dir detailliert, wie der Aufbau aussehen sollte. Dabei ist es wichtig zu beachten, dass die langen Beinchen der LEDs (Pluspol) jeweils mit einem Widerstand und einem grünen oder gelben Kabel mit dem digitalen Port verbunden werden: Die ersten beiden LEDs werden an Digital A (also den digitalen Pins 1 und 2), die letzten beiden LEDs an Digital B (also den digitalen Pins 3 und 4) angeschlossen. Die kurzen Beinchen der LEDs (Minuspol) sollten immer mit einem schwarzen Kabel (GND) verbunden sein. Damit genug Anschlüsse vorhanden sind, dienen die Steckkabel teilweise als Überbrückung.

{% include image.html image=page.image0 %}

## Programmierung

Das Ziel der Programmierung ist es, dass sich die LEDs an jedem Andventssonntag automatisch einschalten und ein Weihnachtscountdown auf dem Display angezeigt wird.

### Schritt 1: Variable definieren und Display initialisieren
Zu Beginn solltest du im Setup() eine Variable definieren, damit darauf aufbauend ein Countdown erstellt werden kann. Diese kannst du beispielsweise als 'Countdown' bezeichnen. Als Höchstwert des Countdowns solltest du die Anzahl an Tagen einstellen, die noch bis Weihnachten verbleiben. Führst du dieses Projekt am 1. Advent durch, so sind es 26 Tage, ansonsten die jeweilge Differenz weniger. Da du das Display als Anzeige verwendest, solltest du dies anschließend mit einem Block im Setup() initialisiseren. 

{% include image.html image=page.image1 %}

### Schritt 2: Schleife erstellen

Damit sich die LEDs nacheinander von selbst einschalten, muss eine Schleife verwendet werden. In diese bettest du deine zuvor definierte Variable 'Countdown' ein und legst fest, dass sie von 26 bis 0 in regelmäßigen Abständen um -1 verringert wird. Diesen Abstand bestimmst du durch den Warte-Block. In der folgenden Abbildung sind dort 86400000 Millisekunden eingetragen, was umgerechnet einen Tag entspricht, sodass nach 24 Stunden die Anzahl der Tage im Countdown passend verändert wird.  

{% include image.html image=page.image2 %}

### Schritt 3: LEDs automatisch steuern
Deine bisher programmierte Schleife kannst du sowohl für die Anzeige des Countdowns als auch für die Steuerung der LEDs nutzen. Für letzteres benötigst du 'wenn...mache'-Bedingungen, die festlegen, ab welchem Tag eine neue LED angeschaltet werden soll. Mit den unten zu findenden Angaben werden jeweils die Adventssonntage im Jahr 2020 angesteuert, an denen sonst auch üblicherweise eine weitere Kerze angezündet wird. An dieser Stelle ist zu beachten, dass du den Start des Countdowns auf den Beginn deiner Projektdurchführung und der ab dann verbleibenden Anzahl an Tagen bis Weihnachten anpasst. Zudem solltest du überprüfen, an welchem PIN deine jeweilige LED angeschlossen ist. Diesen kannst du auf der senseBox MCU an den kleinen Ziffern neben den digitalen Ports ablesen. 

{% include image.html image=page.image3 %}

### Schritt 4: Countdown auf dem Display anzeigen lassen
Nun hast du bereits einen Adventskranz programmiert, bei dem sich die LEDs an jedem Adventssonntag automatisch einschalten. Diesen kannst du noch um einen Countdown ergänzen, der die verbleibenden Tage bis Weihnachten zählt. Verwende dafür die Blöcke 'Zeige auf dem Display' und 'Schreibe Text/ Zahl'. Durch einen Klick auf das Zahnrädchen des letzten Blocks, kannst du ihn um ein weiteres Element ergänzen, sodass eine Textkombination erstellt werden kann. In diesem Fall wurde 'Noch x Tage bis Weihnachten' gewählt. Damit das ganze Programm einmal pro Tag abgespielt wird, ziehe den bereits verwendeten 'Warte'-Block an das Ende der Schleife. Damit hast du die Programmierung abgeschlossen!

{% include image.html image=page.image4 %}

In diesem Sinne wünschen wir euch eine schöne und besinnliche Weihnachtszeit, in der etwas Spaß bei der Durchführung neuer Projekte mit der senseBox nicht fehlen darf!  