---
layout: project_page
date: 2024-04-02
author: Verena
title: "Animiertes Namensschild"
abstract: "Nutze die LED-Matrix, um ein leuchtendes und animiertes Namensschild zu erstellen."
thumbnail: /images/projects/Titelbild_Namensschild.png
image0: /images/projects/Namensschild/0.png
image1: /images/projects/Namensschild/1.png
image2: /images/projects/Namensschild/2.png

material:
  - senseBox MCU S2
  - 1x LED-Matrix
  - 1x QWIIC-Kabel
ide: blockly
version: ["edu-S2"]
lang: de
tags: ["Informatik"]
difficult: leicht
---

Mithilfe der senseBox MCU S2 und der LED-Matrix lassen sich animierte Texte und Bilder anzeigen. In diesem Projekt nutzen wir beide Komponenten, um ein leuchtendes Namensschild zu erstellen.

## Aufbau

Verbinde die LED-Matrix mit einem QWIIC-Kabel und schließe sie an Port A der GPIO-Schnittstelle an. Damit ist der Aufbau abgeschlossen. 

{% include image.html image=page.image0 %}

## Programmierung

### Schritt 1: LED-Matrix initialisieren

Zuerst muss die LED-Matrix im Setup() initialisiert werden. Hier kannst du den Port auswählen, an dem du die Matrix angeschlossen hast (in unserem Fall 'A') sowie die Helligkeit der LED anpassen. Es empfiehlt sich, hier die vorgegebenen Einstellungen unverändert zu lassen.

{% include image.html image=page.image1 %}

### Schritt 2: Anzeige des Namens 

Mit dem Block 'Zeige Text/ Zahl' kannst du nun die Farbe bestimmen, in der der Text angezeigt werden soll. Einen passenden Block findest du in der Kategorie 'LED'. Bei 'Input' kannst du nun einen beliebigen Text, z.B. deinen Namen, angeben. Dafür benötigst du den Block mit einem freien Textfeld aus der Kategorie 'Text'. Das gesetzte Häkchen bei Auto-Scroll führt automatisch dazu, dass sich der Text bewegt und von rechts nach links durch die LED-Matrix läuft.  

{% include image.html image=page.image2 %}

Kompiliere nun den Programmcode und übertrage ihn auf deine senseBox MCU S2. 
