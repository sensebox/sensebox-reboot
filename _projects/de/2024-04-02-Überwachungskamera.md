---
layout: project_page
date: 2024-04-02
author: Verena
title: "Überwachungskamera"
abstract: "Die Anzeige der senseBox gibt eine Warnung aus, sobald sich unbefugte Personen nähern."
thumbnail: /images/projects/Titelbild_Überwachung.png
image0: /images/projects/Überwachung/0.png
image1: /images/projects/Überwachung/1.png
image2: /images/projects/Überwachung/2.png
image3: /images/projects/Überwachung/3.png

material:
  - senseBox MCU S2
  - 1x LED-Matrix
  - 1x ToF-Sensor
  - 2x QWIIC-Kabel
ide: blockly
version: ["edu-S2"]
lang: de
tags: ["Informatik"]
difficult: leicht
---

Du kannst mithilfe der senseBox verschiedene Dinge vor Dieben und unbefugten Personen schützen. Das Ziel dieses Projektes ist es, dass die senseBox dauerhaft den Satz 'Bitte nicht anfassen!' auf der LED-Matrix ausgibt. Sobald sich eine Person nicht daran hält und weniger als 50cm Abstand zum ToF-Sensor hat, wechselt der Text der Anzeige und es erscheint: 'STOPP - Finger weg!'. 

## Aufbau

Verbinde die LED-Matrix mit einem QWIIC-Kabel und schließe sie an Port A der GPIO-Schnittstelle an. Das andere QWIIC-Kabel verbindest du mit dem ToF-Sensor und schließt es an einen der beiden I2C-Ports an.

{% include image.html image=page.image0 %}

## Programmierung

### Schritt 1: LED-Matrix initialisieren

Zuerst muss die LED-Matrix im Setup() initialisiert werden. Hier kannst du den Port auswählen, an dem du die Matrix angeschlossen hast (in unserem Fall 'A') sowie die Helligkeit der LED anpassen. Es empfiehlt sich, hier die vorgegebenen Einstellungen unverändert zu lassen.

{% include image.html image=page.image1 %}

### Schritt 2: Die logische Verknüpfung

Um die oben genannte Bedingung zu erfüllen, brauchst du den 'Wenn...mache...sonst'-Block aus der Kategorie 'Logik'. Zudem brauchst du das 'kleiner als'-Zeichen (<) aus der selben Kategorie, um die maximale Distanz von 50cm (Kategorie: Mathematik) festlegen zu können. Wenn diese Distanz unterschritten wird, wird der Text 'STOPP - Finger Weg' auf der LED-Matrix angezeigt. Diesen Text fügst du mithilfe eines Textfelds aus der Kategorie 'Text' bei 'Input' ein. Die Farbe kannst du vorab beliebig auswählen.

{% include image.html image=page.image2 %}

### Schritt 3: Die Alternative (sonst...)

Wird die Distanz nicht unterschritten, gibt die Alarmanlage die herkömmliche Warnung 'Bitte nicht anfasssen' aus. Nutze auch hier wieder den Block 'Zeige Text/ Zahl' für die LED-Matrix und wähle eine beliebige Farbe aus.  

{% include image.html image=page.image3 %}

Positioniere die senseBox nun neben Gegenständen, die überwacht werden sollen und lasse sie Personen automatisch warnen, bevor sie sich nähern. 


