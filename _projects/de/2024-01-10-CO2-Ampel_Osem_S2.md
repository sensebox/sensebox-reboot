---
layout: project_page
title: "IoT CO2-Ampel"
date: 2024-01-10
author: Verena
abstract: "Übertragt die Daten eurer CO2-Ampel per Wlan auf die openSenseMap."
thumbnail:  /images/projects/Titelbild_CO2-Ampel_Osem.png
image0: /images/projects/CO2-Ampel_Osem_S2/0.png
image1: /images/projects/CO2-Ampel_Osem_S2/1.png
image2: /images/projects/CO2-Ampel_Osem_S2/2.png
image3: /images/projects/CO2-Ampel_Osem_S2/3.png
image4: /images/projects/CO2-Ampel_Osem_S2/4.png
image5: /images/projects/CO2-Ampel_Osem_S2/5.png
image6: /images/projects/CO2-Ampel_Osem_S2/6.png

material:
    - senseBox MCU-S2
    - 1x CO2-Sensor
    - 1x OLED-Display
    - 2x QWIIC-Kabel

ide: blockly
version: ["edu-S2"]   
addons: ["CO2-Sensor"] 
lang: de
tags: ["Informatik", "IoT", "Chemie"]
difficult: mittel
---
<head><title>Datenübertragung mit der CO2-Ampel</title></head>

# Datenübertragung mit der CO2-Ampel
In diesem Projekt erfährst du, wie du die Daten, die mit der CO2-Ampel in deinem Klassenraum erfasst werden, auf die openSenseMap übertragen kannst. Somit wird deine CO2-Ampel Teil eines Citizen Science Projektes und du kannst deine Luftqualität im Raum mit der vieler anderer Schulen vergleichen. Dieses Projekt lässt sich auch mit der senseBox:edu S2 mit einem zusätzlichen [CO2-Sensor](https://sensebox.kaufen/product/co2-sensor) durchführen. 

## Aufbau
Das Wifi-Modul und die RGB-LED sind bereits auf dem Board der MCU-S2 integriert, sodass du diese nicht separat anschließen musst. Das OLED-Display und der CO2-Sensor werden mit jeweils einem QWIIC-Kabel an einen der zwei I2C-Anschlüsse angeschlossen. 

{% include image.html image=page.image0 %}

## Programmierung

Das Ziel der Programmierung ist es, dass die CO2-Ampel die Temperatur sowie den CO2-Gehalt der Luft auf dem Display anzeigt und je nach Luftqualität die Farbe der RGB-LED ändert. Zusätzlich sollen die erfassten Daten per Wlan minütlich an die openSenseMap gesendet werden. 

### Schritt 1: Display und Internetverbindung einrichten
Damit eine Verbindung zu deinem Wlan-Router hergestellt werden kann, muss der Block 'Verbinde mit Wlan' aus der Kategorie Web/ Wifi ins Setup integriert sowie die nötigen Informationen dort eingegeben werden. In Schulen kommt es häufig zu Problemen mit dem vorhandenen WLAN-Netzwerk. Verwende daher den mobilen Hotspot deines Smartphones und gebe die dazugehörigen Informationen in die passenden Felder ein. Des Weiteren ist es notwendig, das Display und die RGB-LED an dieser Stelle zu initialisieren. 

{% include image.html image=page.image1 %}

### Schritt 2: Variablen definieren

Um deinen Code übersichtlicher zu gestalten und die Messwerte an die openSenseMap schicken zu können, sollten zu Beginn die Variablen definiert werden. In diesem Fall benötigen wir zwei Variablen: 'CO2' für den CO2-Gehalt der Luft sowie 'temp' für die Temperatur im Raum. 

{% include image.html image=page.image2 %}

### Schritt 3: Die 'wenn...mache'-Bedingung

Nun kannst du festlegen, was gemacht werden soll, falls die gemessenen Werte des CO2-Sensors kritische Werte über- oder unterschreiten. In unserem Beispiel haben wir uns nach einer Empfehlung des Umweltbundesamtes gerichtet, die vorgibt, wann die Luftqualität so schlecht ist, dass das Infektionsrisiko erhöht ist und das Lüften des Raumes dringend empfohlen wird. Im ersten Fall (CO2 < 1000ppm) ist alles im grünen Bereich, weshalb bei der RGB-LED der Wert 255 bei grün eingetragen ist. Im nächsten Fall (1000ppm-1500ppm) hat die Luftqualität schon nachgelassen, weshalb die RGB-LED gelb leuchten soll. Diese Farbe erhältst du durch die angegebene Mischung aus rot und grün. Im schlechtesten Fall überschreitet der CO2-Gehalt der Luft den Wert von 1500ppm und die RGB-LED leuchtet rot.  

>**Tipp:** Den ursprünglichen 'wenn...mache' Block aus der Kategorie 'Logik' kannst du durch einen Klick auf das Zahnrädchen durch den 'sonst wenn'-Baustein erweitern. 

{% include image.html image=page.image3 %}


### Schritt 4: Werte auf dem Display anzeigen lassen
Damit dir die Werte auf dem Display angezeigt werden, benötigst du die Blöcke 'Zeige auf dem Display' sowie 'Zeige Messwerte'. Hier kannst du zum einen mit Textbausteinen arbeiten, mit denen du den Titel und die Einheit benennst. Zum anderen kannst du deine zuvor definierten Variablen als Messwert 1 und Messwert 2  nutzen. Des Weiteren empfiehlt es sich, vor der Ausgabe der Werte den Block 'Display löschen' einzubauen, damit die aktuellen Werte korrekt angezeigt werden. 

{% include image.html image=page.image4 %}


### Schritt 5: Übertragen der Messwerte an die openSenseMap
Für ein effizientes Versenden der Daten reicht es aus, wenn dies minütlich geschieht. Daher kannst du aus der Kategorie 'Zeit' den Block 'Messintervall' verwenden und hier das Intervall anpassen. In der Kategorie Web/openSensemap findest du die Blöcke, die benötigt werden, um die erfassten Daten per Wlan zu übertragen. Als Wert des Sensors kannst du hier ernut die vorhandenen Variablen nutzen. Nun ist es wichtig, dass du die freien Felder ausfüllst. Die dazugehörigen Informationen erhältst du im nächsten Schritt.  

{% include image.html image=page.image5 %}

## Registrierung auf der openSenseMap
Du hast nun alle notwendigen Schritte der Programmierung in Blockly abgeschlossen. Jetzt muss deine CO2-Ampel nur noch auf der openSenseMap registriert werden. Besuche dazu die Seite der [openSenseMap](https://opensensemap.org/), registriere dich und lege eine neue Box an. Gebe anschließend den Standort deiner stationären senseBox an und wähle als Sensor unter der Kategorie 'edu' zweimal den CO2-Sensor: Einmal für die Temperatur und einmal für den CO2-Gehalt der Luft. Mit der Bestätigung deiner Angaben erhältst du dann die nötigen IDs und Kennzeichnungen, die du im letzten Block deines Codes bei Blockly eintragen musst.
Den API-Schlüssel findest du im Gegensatz zu den IDs nicht in der Übersicht, sondern unter dem Punkt 'Sicherheit', wenn du deine senseBox editierst. 

{% include image.html image=page.image6 %}

## Gesamter Code

Den gesamten Blockly-Sketch kannst du [hier](https://blockly.sensebox.de/gallery/63b69bbbd2853f0013b1d9ce) abrufen.


