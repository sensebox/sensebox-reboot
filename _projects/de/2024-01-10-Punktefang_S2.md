---
layout: project_page
title: "Gehe auf Punktefang!"
date: 2024-01-10
author: Verena
abstract: "Programmiere dein eigenes Spiel mit der senseBox!"
thumbnail:  /images/projects/Titelbild_Punktefang.png
image0: /images/projects/Punktefang_S2/0.png
image1: /images/projects/Punktefang_S2/1.png
image2: /images/projects/Punktefang_S2/2.png
image3: /images/projects/Punktefang_S2/3.png
image4: /images/projects/Punktefang_S2/4.png
image5: /images/projects/Punktefang_S2/5.png
image6: /images/projects/Punktefang_S2/6.png
image7: /images/projects/Punktefang_S2/7.png
image8: /images/projects/Punktefang_S2/8.png
image9: /images/projects/Punktefang_S2/9.png

material:
    - senseBox MCU-S2
    - 1x OLED-Display
    - 1x QWIIC-Kabel
    
ide: blockly
version: ["edu-S2"]   
lang: de
tags: ["Informatik", "Physik"]
difficult: schwer
---
<head><title>Gehe auf Punktefang!</title></head>

# Eine intelligente Straßenbeleuchtung bauen und programmieren
Du kennst bestimmt noch die ersten Computerspiele aus den 80er-Jahren, wie zum Beispiel Pong oder Tetris Auf alten zweifarbigen Fernsehern wurden in 2-D spannende und einfache Spiele erstellt. Einfache grafische Elemente wurden kombiniert mit tollen Spielkonzepten, und es entstanden Spiele mit Suchtpotenzial. Mit dem Beschleunigungssensor der MCU-S2 kannst du nun ein ähnliches Spiel programmieren!

## Aufbau
Der Aufbau für das Projekt ist relativ einfach, da der Beschleunigungssennsor (MPU6050) bereits auf der senseBox MCU-S2 aufgelötet ist und direkt genutzt werden kann. Das Display verbindest du mit dem QWIIC-Kabel mit dem I2C-Port. 

{% include image.html image=page.image0 %}

## Programmierung

Die Programmierung des kleinen Spiels erfolgt schrittweise, da verschiedene Bereiche nacheinander abgedeckt werden müssen. Neben den grafischen Komponenten müssen die Spielsteuerung und das Gewinnprinzip programmiert werden. Diese drei Bereiche werden in den folgenden Schritten erklärt und zusammengefügt

### Schritt 1: Spielsteuerung – der Fänger

#### Auslesen des Beschleunigungssensors
Vom Smartphone kennt man die Spielsteuerung über den Bewegungssensor des Handys. Für dieses Spiel soll eine ähnliche Steuerung gebaut werden. Im ersten Schritt ist es wichtig zu verstehen, welche Messwerte der Beschleunigungssensor erfasst und welche drei Bewegungsrichtungen erfasst werden können. Der Beschleunigungssensor kann über den folgenden Block ausgelesen werden:

{% include image.html image=page.image1 %}

Der Block für den Beschleunigungssensor hat ein Drop-down-Menü, in dem die Richtung eingestellt wird, in der die Beschleunigung gemessen werden soll. Die Beschleunigung kann in x-, y- und z-Richtung gemessen werden.

Um die Messwerte besser verstehen zu können, soll im ersten Schritt der Sensor ausgelesen und alle Messwerte auf dem Display angezeigt werden. Achte dabei auf die Anpassung der Y-Koordinate, damit die Messwerte untereinander und nicht übereinander angezeigt werden:

{% include image.html image=page.image2 %}

Kompiliere den Code und teste ihn mit deiner senseBox. 
Die Messwerte des Beschleunigungssensors für die x-, y- und z-Achse werden dir als g-Kraft angezeigt.

#### Darstellung eines Punktes
Für das Spiel werden die Beschleunigungswerte auf der x- und y-Achse verwendet. Mithilfe der Bewegung der senseBox MCU-S2 soll ein kleiner Punkt auf dem Display gesteuert werden. In der Toolbox findest du die Blöcke für das Display. Der Block 'Zeichne Punkt' kann verwendet werden, um einen Punkt mit einer bestimmten Größe auf dem Display anzeigen zu lassen.

{% include image.html image=page.image3 %}

Um einen Punkt zu zeichnen, müssen drei verschiedene Parameter angegeben werden: die x- und y-Koordinate auf dem Display und der Radius. Der Radius wird in Pixeln angegeben und sollte nicht zu groß sein. In diesem Beispiel wird immer ein Radius von 3 Pixeln verwendet. Das Display hat auf seiner x-Achse 128 und auf der y-Achse 64 Pixel, die Messwerte des Beschleunigungssensors liegen allerdings zwischen -1 und 1 beim normalen Bewegen der Platine. An dieser Stelle kann eine praktische Funktion aus der Informatik verwendet werden: das Mapping.

#### Mapping
Mapping ist ein nützliches Prinzip aus der Informatik und hilft dabei, Sensorwerte umzurechnen und in Programmen zu verwenden. Grundlegend werden Werte zwischen einer oberen und unteren Grenze neuen Werten zwischen einer oberen und unteren Grenzen zugeordnet. 
Durch den Block 'Verteile Wert' werden die Messwerte dynamischen zwischen dem Minimum und dem Maximum auf 0 bis 128 verteilt.

Über das Mapping können wir nun einen Punkt auf dem Display anzeigen lassen, der sich je nach Lage der senseBox MCU-S2 verschiebt. Beachte hierbei, dass die x-Achse auf dem Display nicht der x-Achse des Beschleunigungssensors entspricht.

{% include image.html image=page.image4 %}

### Schritt 2: Der gejagte Punkt

Die Spielsteuerung ist fertig, jetzt fehlt noch der gejagte Punkt! Dieser Punkt soll an einer zufälligen Position auf dem Display angezeigt und von dem anderen Punkt, der über die Bewegung der MCU gesteuert wird,
gefangen werden. Zufallszahlen lassen sich über Blockly sehr einfach erstellen, in der Toolbox unter Mathematik befindet sich der Block 'ganzzahliger Zufallswert zwischen 1 und 100'. Für die x-Koordinate muss eine Zahl zwischen 10 und 118 und für die y-Koordinate eine Zahl zwischen 10 und 54 generiert werden. Da es fast unmöglich ist, Punkte zu fangen, die direkt am Displayrand liegen, werden von den Koordinaten
jeweils 10 Pixel abgezogen. Die generierten Zufallszahlen speichern wir unter den float-Variablen randomX und randomY ab, da diese für das Spiel noch in einem anderen Zusammenhang verwendet werden. Das Erstellen der Zufallszahlen lassen wir zunächst im Setup durchführen, sodass wir einen zufälligen Punkt bekommen und dieser anschließend angezeigt wird.

{% include image.html image=page.image5 %}

### Schritt 3: Das Fangen

Im aktuellen Programm sollten nun immer zwei Punkte zu sehen sein: Der eine Punkt bewegt sich über die Steuerung der MCU-S2, und der zweite ist bewegungslos. Der nächste Schritt des Programms ist das Fangen. Das Fangen des Punkts lässt sich über eine Wenn-Dann-Bedingung realisieren. Wenn die x- und y-Koordinaten des Punkts, der über die MCU-S2 gesteuert wird, gleich den zufällig erstellen Koordinaten sind, wurde der Punkt gefangen.

{% include image.html image=page.image6 %}

Die Wenn-Dann-Bedingung setzt sich aus zwei Bedingungen zusammen, die mit dem logischen UND verknüpft werden. Wenn die Bedingungen erfüllt sind, dann wird das Display gelöscht, und auf dem Display wird angezeigt, dass der Punkt gefangen wurde. Damit das Spiel auch wirklich endet, füge noch den Block 'Warte für immer' aus der Kategorie Zeit in die Wenn-Dann-Bedingung ein.

### Schritt 4: Erweiterung

Bisher ist das Spiel noch nicht wirklich ausgefeilt. Der zufällige Punkt wird nur einmal erstellt, und das Spiel ist bereits vorbei, wenn der Punkt gefangen wurde. In diesem Schritt wird das Spiel erweitert, sodass es ein Endlosspiel wird. Folgende Schritte müssen dafür durchgeführt werden. Zum einen muss fortlaufend ein neuer Punkt generiert werden, wenn der vorherige Punkt gefangen worden ist.

Damit immer wieder ein neuer Punkt generiert wird, muss das Erstellen in der Endlosschleife passieren. Anstelle der Anzeige auf dem Display, dass der Punkt gefangen wurde, werden in der Wenn-Dann-Bedingung neue Koordinaten erstellt. So wird sichergestellt, dass immer, wenn du einen Punkt gefangen hast, direkt ein neuer erstellt wird.

{% include image.html image=page.image7 %}

### Schritt 5: Spielzeit & Zähler

Ein Spiel ist natürlich erst dann vollständig, wenn es eine Spielzeit und einen Spielstandzähler gibt. Die Spielzeit kann über den Block 'Messintervall' erfasst werden, für den Zähler des Spielstands wird eine neue Variable des Typs 'int' angelegt, die immer um eins hochgezählt wird, wenn die Bedingungen zum Fangen eines Punkts erfüllt wird.

{% include image.html image=page.image8 %}

Den Block zum Anlegen und Hochzählen der Variablen findest du in der Kategorie Mathematik. Die Variable kannst du in der Kategorie 'Variablen' selbst erstellen und im Setup festlegen, dass die Zählung bei null startet.
Wenn die Spielzeit abgelaufen ist, werden auf dem Display »Spiel beendet« und die Anzahl der gefangenen Punkte angezeigt werden.

{% include image.html image=page.image9 %}

Am Ende wird das Programm wieder mit dem Block 'Warte für immer' beendet.
Baue den Programmcode der einzelnen Bestandteile zusammen und übertrage das Programm auf die senseBox MCU-S2. Anschließend kannst du einen kleinen Wettstreit mit Freunden und der Familie starten, wer die
meisten Punkte fängt.

!! Den gesamten Blockly-Sketch findest du [hier](https://blockly.sensebox.de/gallery/642e7500d2853f0013b357e6).


