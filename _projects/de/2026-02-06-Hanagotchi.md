---
layout: project_page
title: "Hanagotchi"
date: 2026-02-06
author: Emma
abstract: Das virtuelle Haustier, was deinen Pflanzen hilft
thumbnail: /images/projects/Titelbild_Hanagotchi.jpg
image0: /images/projects/Hanagotchi/Aufbau.jpeg
image1: /images/projects/Hanagotchi/Setup.png
image2: /images/projects/Hanagotchi/alle_Variablen.png
image3: /images/projects/Hanagotchi/wenn_dann_Helligkeit.png
image4: /images/projects/Hanagotchi/schlafendes_Hanagotchi.png
image5: /images/projects/Hanagotchi/normales_Hanagotchi.png
image6: /images/projects/Hanagotchi/hungriges_Hanagotchi.png
image7: /images/projects/Hanagotchi/Kauanimation.png
image8: /images/projects/Hanagotchi/Sperre_falsch.png
image9: /images/projects/Hanagotchi/Sperre_nicht.png
image10: /images/projects/Hanagotchi/Sperre_wahr.png
image11: /images/projects/Hanagotchi/Wassergehalt.png
image12: /images/projects/Hanagotchi/zu_warm_Hanagotchi.png
image13: /images/projects/Hanagotchi/Fertiger_TemperaturBlock.png
image14: /images/projects/Hanagotchi/Fast_Fertig.png
image15: /images/projects/Hanagotchi/sehr_zufriedenes_Hanagotchi.png
image16: /images/projects/Hanagotchi/Kompletter_Code.png
image17: /images/projects/Hanagotchi/Display_Code.png
image18: /images/projects/Hanagotchi/Hanagotchi.png

material:
    - senseBox MCU S2
    - 1x OLED-Display (optional)
    - 1x LED-Matrix
    - 1x Button (on board)
    - 1x Lichtsensor
    - 1x Temperatur- und Feuchtigkeitssensor
    - 1x Bodenfeuchtesensor (SMT50)
    - 4-5x QWIIC-Kabel
    - 1x Adapterboard
    - 1x Pflanze
ide: blockly
lang: de
version: edu-S2
tags: ["Informatik"]
difficult: mittel
---
# Das Hanagotchi {#head}
Um die Jahrtausendwende waren Tamagotchi und auch Digimon absoluter Kult. Das sind Taschen-Haustiere, die die ganze Zeit umsorgt und gefüttert werden müssen. Aber genau wie Haustiere müssen auch Pflanzen gepflegt werden. Das Hanagotchi ist ein kleines, virtuelles Monster, dass dir hilft, dich um deine Pflanze zu kümmern. Fun Fact: Tamagotchi setzt sich aus den Worten Ei (auf Japanisch Tamago) und Armbanduhr (auf Englisch Watch) zusammen, da sie aus Eiern schlüpfen und rund um die Uhr versorgt werden müssen. Auch Hanagotchis sind immer da, sie schlüpfen aber nicht aus einem Ei. Das Wort Hana bedeutet auf Japanisch Blume und genau das sind sie ja auch: immer da und nachtragender als jedes Tamagotchi, wenn man mal das Füttern vergisst.

In diesem Projekt bauen wir also unser eigenes kleines digitales Haustier. Es reagiert auf Helligkeit, Temperatur, Bodenfeuchte und natürlich unser Streicheln (Knopf drücken). Auf der LED-Matrix zeigt es uns an, wie es ihm geht bzw. was es aktuell macht. Los geht's!"

{% include image.html image=page.image18 %}

## Aufbau 
Die LED-Matrix wird an einem der Digital-Ports angeschlossen. Hierbei ist es wichtig, dass später im Code auch der richtige angegeben wird. In diesem Projekt ist es der zweite, also Port B. Auch der Bodenfeuchtesensor wird mithilfe des Adapterboards mit einem QWIIC-Kabel in einem der Digital-Ports angeschlossen, in diesem Fall Port A. Die Sensoren für Licht und Temperatur werden jeweils mit einem Kabel an einen der I2C-Ports angeschlossen, können aber auch in Reihe geschaltet werden. Wer die gemessenen Werte auf dem Display sehen möchte, muss auch das Display mit einem der Kabel an einen der Ports schließen.

{% include image.html image=page.image0 %}

## Programmierung


### Setup und Variablen
Zuallererst muss die LED-Matrix im Setup initialisiert werden. Falls du das Display mitbenutzen möchtest, musst du es auch noch initialisieren.

{% include image.html image=page.image1 %}

Um den Code zu vereinfachen, werden alle Werte als Variablen angelegt. Das ist außerdem sehr praktisch, weil sie so leicht anpassbar sind, z.B. wenn deine Pflanze draußen steht, oder du die Werte genau dieser Pflanzenart anpassen möchtest. Die hier genutzten Werte sind nur allgemein. Die Sensoren, die du angeben musst, sind Temperatur, Bodenfeuchtigkeit und Licht.

Zusätzlich musst du für jeden Sensor einen spezifischen Wert festlegen, der als Schwellwert benutzt wird. 

{% include image.html image=page.image2 %}

Der Lichtsensor misst die Helligkeit in deinem Raum, stelle ihn also auf „Beleuchtungsstärke in Lux“ ein. So wird das Hanagotchi immer dann schlafen, wenn es dunkel wird. Der Temperatursensor signalisiert, wann es zu warm, bzw. zu kalt für deine Pflanze ist. Auch das wird von dem kleinen Tier gezeigt, indem es seine Farbe ändert. Der Bodenfeuchtesensor zeigt dir, wann es Zeit ist, deine Pflanze zu gießen und das Hanagotchi hungrig ist. Für diese Funktionen ist es jetzt wichtig, dass für das Programm klar definiert ist, wann welcher Zustand zutrifft. Und falls zwei und mehr gleichzeitig eintreffen, welcher am wichtigsten ist. Deshalb werden hier mehrere Wenn-Dann-Bedingungen benötigt.



### Anordnung nach Wichtigkeit

#### Lichtsensor
Als erstes wird deswegen der Lichtsensor wichtig. Denn wenn es schläft, wird das Hanagotchi nichts Anderes benötigen. Du erstellst jetzt also einen Wenn-Dann-Block. Die Bedingung ist in diesem Fall, dass der Lichtsensor eine Beleuchtungsstärke von höchstens 20 Lux misst. Dafür kannst du einfach die von dir erstellten Variablen benutzen, wie hier gezeigt.

{% include image.html image=page.image3 %}

Die Aktion, die ausgeführt werden soll, ist das schlafende Hanagotchi auf der LED-Matrix zu zeigen. 
WICHTIG!: Du musst jedem Motiv, das du für die Bitmap erstellst, einen eigenen Namen geben, damit das Programm sie alle erkennt.

{% include image.html image=page.image4 %}

Als nächstes erweiterst du den Block um eine Sonst-Funktion erweitern. Das machst du, indem du auf das kleine blaue Zahnrad klickst, und den Block hinzufügst. Hier werden die weiteren Aktionen des Tierchens bestimmt.
In den Block platzierst du jetzt den Normalzustand deines Haustiers, also wie es aussehen soll, wenn es ihm rund um gut geht.

{% include image.html image=page.image5 %}

Übertrage das Programm auf deine senseBox und probiere es aus! Schläft das Krokodil, wenn es dunkel ist?

#### Bodenfeuchtesensor
Danach folgt eine weitere Wenn-Dann-Bedingung. Hier wird jetzt in mehreren Schritten die Temperatur- und „Hunger“-Funktion eingestellt. Auch hier ist wieder wichtig zu beachten, was als Aktion Vorrang hat. In diesem Fall ist es der Wassergehalt in der Erde. Die Bedingung ist also, dass die gemessene Bodenfeuchte mindestens 40% sein muss. Auch hier musst du den Block jetzt um die Sonst-Funktion erweitern: wenn die Pflanze nicht genügend Wasser bekommt, wird das Hanagotchi hungrig. In diesen Abschnitt wird also die Anzeigen des hungrigen Monsters eingefügt.

{% include image.html image=page.image6 %}

Jetzt bestimmst du noch, was passiert, wenn der Wassergehalt über 40% liegt, also was in den Mache-Bereich des Blocks gehört. Und was machen wir, wenn wir etwas essen? Wir kauen es erstmal. Genau das muss auch das Hanagotchi machen. Für diese Animation sind mehrere Bilder nötig, um die Abfolge der Bewegung darzustellen. Zwischen den Bildern muss auch immer eine kurze Wartezeit abgespielt werden, damit unser Auge sie überhaupt alle wahrnehmen kann. Hier ist nochmal wichtig, auch wenn es die gleichen Bilder sind, musst du ihnen unterschiedliche Namen geben, da sie an verschiedenen Stellen stehen. Damit die Bilderfolge mehrmals abgespielt wird, muss sie in einer Wiederholung stattfinden. Wie oft die Aktion wiederholt wird, kannst du selbst entscheiden.

{% include image.html image=page.image7 %}

Aber natürlich ist das kleine Tier auch irgendwann fertig mit Essen. Damit es aber nicht die ganze Zeit weiter kaut, solange eine ausreichende Bodenfeuchte gibt, musst du eine Wahr-Falsch-Variable (boolean) benutzen.

Sie dient dazu, zu erkennen, wann die Aktion bereits ausgeführt wurde, also nicht mehr nötig ist. Sie bewirkt aber auch, dass das Hanagotchi wieder kaut, sobald der Wassergehalt im Topf wieder sinkt und du erneut deine Pflanze gießt. Die Variable musst du dafür jetzt an verschiedenen Stellen einsetzen: Als erstes musst du zurück zum Setup. Hier fügst du die Variable ein und stellst sie auf „Falsch“. Das heißt, dass wenn das Programm anfängt, die Aktion noch nicht ausgeführt wurde.

{% include image.html image=page.image8 %}

Jetzt musst du zurück zu dem letzten Wenn-Dann-Block, wo die Bodenfeuchte definiert wurde. Hier fügst du jetzt eine weitere Wenn-Dann-Bedingung im noch leeren Mache-Bereich ein.

Die Aktion, die ausgeführt werden soll, ist jetzt die Wiederholung der Kaubewegung. Die Bedingung dafür ist, dass sie noch nicht ausgeführt wurde. Das hast du vorher im Setup bestimmt. 

{% include image.html image=page.image9 %}

Wenn diese Beding erfüllt ist, wird so aber automatisch die Kauanimation ausgeführt. Damit das jetzt aber nicht die ganze Zeit so weitergeht, musst du vor der Wiederholungsschleife die Variable auf „wahr“ einstellen. 

{% include image.html image=page.image10 %}

Der letzte Schritt ist jetzt sicherzustellen, dass die Animation wieder passiert, wenn der Wert nochmal von Neuem überschritten wird. Dafür musst du in den Sonst-Bereich des Wenn-Dann-Blocks, wo auch das Bild von dem hungrigen Krokodil ist. Vor den Bitmap-Block setzt du jetzt also wieder die Variable auf falsch, sodass das Programm denkt, dass die Aktion noch nicht ausgeführt wurde, wie ganz am Anfang.

{% include image.html image=page.image11 %}

#### Temperatursensor
Jetzt fehlt noch der Temperatursensor. Ob der Pflanze zu warm oder zu kalt ist, ist aber nicht so wichtig, wie ihr genügend Wasser zu geben. Deshalb, musst du eine weitere Wenn-Dann-Bedingung benutzen. Die Bedingung ist, dass die gemessene Temperatur höchstens so hoch wie das von dir definierte Maximum ist. Auch hier kannst du wieder die Variablen vom Anfang benutzen. Wenn diese trotzdem überschritten wird, soll das Tier seine Farbe ändern, um zu signalisieren, dass ihm zu warm ist. 

{% include image.html image=page.image12 %}

Natürlich spürt das Hanagotchi aber auch, wenn ihm zu kalt ist. Dafür erweiterst du den Block jetzt um die Sonst-Wenn-Funktion. Dieses Mal benutzt du in der Bedingung aber nicht die maximale, sondern die minimale Temperatur. Die gemessene Temperatur muss also mindestens diesen Wert überschreiten. Auch hier wird die Temperatur durch einen Farbwechsel angezeigt.

{% include image.html image=page.image13 %}

{% include image.html image=page.image14 %}

#### Button
Die beste Funktion deines kleinen Freunds kommt aber erst jetzt: genau wie ein richtiges Haustier ist es erst vollkommen glücklich, wenn du es streichelst. Aber auch nur dann, wenn es sonst rund um zufrieden ist. Unter den Temperaturabschnitt, setzt du jetzt also eine weitere Bedingung. Wenn der Button auf dem Board gedrückt ist, dann wird ein sehr glückliches Hanagotchi gezeigt. 

{% include image.html image=page.image15 %}

{% include image.html image=page.image16 %}

### Optional: Anzeigen der Werte auf dem Display

Falls du dich entschieden hast, das Display zu benutzen, musst du noch die Werte anzeigen lassen. Unter den äußersten Wenn-Dann-Block platzierst du jetzt also den „Display löschen“-Block. Das ist wichtig, damit nur die aktuellen Werte und nichts Anderes angezeigt wird. Dann benutzt du den Block „Zeige auf Display“, um die folgenden Blöcke hinein zu platzieren. Die einfachste Variante ist jetzt, dreimal den „Schreibe Text/Zahl“-Block einzufügen. Auch hier kannst du wieder die Variablen vom Anfang als Werte einsetzen. Wichtig zu beachten ist jetzt aber, dass alle drei Werte eine unterschiedliche y-Koordinate haben, damit sie sich nicht überlagern und unlesbar werden. 

{% include image.html image=page.image17 %}

Jetzt musst du die senseBox nur noch mit Strom versorgen, und du hast ein kleines Hanagotchi.

## Ausblick

Dieses Projekt ist nur eine Vorlage, wie dein senseBox-Haustier aussehen könnte. 
Du kannst sowohl diese Version des Codes übernehmen oder optimieren, als auch neue Funktionen hinzufügen oder andere Sensoren benutzen. Beispielsweise kannst du ein anderes Tier wählen, oder was ganz Anderes anzeigen lassen. Oder du benutzt es nicht nur für deine Pflanze, sondern für die Luftqualität bei dir zu Hause. Das Hanagotchi kannst du also vollständig personalisieren und gestalten und benutzen, wie du willst. 

## Gesamter Code

Den gesamten Blockly-Code findest du hier: [Blockly Code Hanagotchi](https://blockly.sensebox.de/gallery/69c3b246f58c360012b7268d)