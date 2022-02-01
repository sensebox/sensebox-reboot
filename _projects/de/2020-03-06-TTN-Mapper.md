---
layout: project_page
title: "Erstelle einen TTN Mapper in unter 10 Minuten"
date: 2020-03-06
author: Felix & Paul
abstract: "Mit dem LoRa-Bee und GPS Modul bauen wir einen senseBox TTN Mapper"
thumbnail: /images/projects/ttn-mapper-de.png

material:
    - senseBox MCU
    - 1x JST-Kabel 
    - LoRa-Bee
    - GPS Modul
ide: blockly  
version: ["edu", "mini"]
addons: ["LoRa-Bee"]  
lang: de
tags: ["Geographie", "Informatik", "LoRa", "TTN", "Blockly"]
difficult: mittel
---
# senseBox TTN Mapper

Das Ziel ist die Entwicklung eines TTN Mappers mit Hilfe des LoRa Bees und des GPS Moduls. Die Daten werden über das freie [TheThingsNetwork](https://www.thethingsnetwork.org/) zum TTN Mapper übertragen. Der [TTN Mapper](http://ttnmapper.org/) ist eine Karte auf welcher man Orte mit TTN Empfang kartieren kann. Mithilfe der senseBox wollen wir uns an der Platform beteiligen.


## Hardware

<div class="row">
	<div class="post-image">
			<img loading="lazy" src="https://sensebox.kaufen/api/public/uploads/1584028489927-TTN-Mapper.png" alt="TTN-Mapper-Shop - Logo" data-zoomable/>
	</div>
</div>

Für das Projekt brauchst du eine senseBox MCU, ein LoRa-Bee sowie ein GPS Modul. Im senseBox Shop gibt es bereits ein fertiges Set: [https://sensebox.kaufen/product/sensebox-ttn-mapper-set](https://sensebox.kaufen/product/sensebox-ttn-mapper-set)

Verbinde das LoRa-Bee mit XBEE1 deiner senseBox MCU. Verbinde außerdem das GPS Modul mit einem I2C Steckplatz.

Zusätzlich brauchst du eine möglichst mobile Stromversorgung. Am einfachsten ist eine USB Powerbank oder ein Akku mit passendem Anschluss für die senseBox MCU.

## Registrierung auf TheThingsNetwork und anlegen einer Application

Gehe auf die [TTN-Console](eu1.cloud.thethings.network) und erstelle dir dort einen Account. Sobald du angemeldet bist, klicke auf **Go to applications**. Hier klickst du jetzt oben in der rechten Ecke auf **Add Application**. Die ID und den Namen kannst du frei wählen.

![](/images/projects/TTNv3/add-application.png)

Nun musst du in deiner neuen Application noch ein Device hinzufügen. Klicke auf "+ Add end Device" und füge ein neues Device (z.B. eine senseBox hinzu).

![](/images/projects/TTNv3/add-device.png)

Wähle jetzt oben **Manually** aus. Als **Frequency Plan** muss *Europe 863-870 MHz (SF9 for RX2 - recommended)*, als **LoRaWAN version** die Option *MAC V1.0.2* und als **Regional Parameters Version** die Option *PHY V1.0.2 REV A* ausgewählt werden.

![](/images/projects/TTNv3/register-device.png)

Im nächsten Schritt müssen die EUIs eingetragen werden. Die DevEUI kann von TTNv3 über den Button automatisch generiert werden. Pro Application können jedoch nur 50 EUIs genutzt werden, da diese einmalig sein müssen. Die AppEUI kann über den Button mit Nullen gefüllt werden und der AppKey kann auch wieder automatisch generiert werden.

![](/images/projects/TTNv3/register-device-euis.png)

Abschließend kannst du deinem Device noch eine ID geben oder die automatisch generierte ID nutzen.

Jetzt kannst du einfach auf **Register end device** klicken und dein Device wird erstellt. 

Fertig, TTN "kennt" nun deine senseBox.

Da wir die Daten später an den TTN Mapper senden möchten, musst Du jetzt noch eine "Integration" hinzufügen. Dafür gehst du im Menü an der Seite auf "Integrations" und dann zu Webhooks. Hier sollte jetzt dieses Menü auftauchen:

![](/images/projects/TTN-Mapper/add-integration.png)

Hier klickst du jetzt auf "+ Add Webhook" in der oberen rechten Ecke. Im nun erscheinenden Auswahlmenü suchst du die Option "TTN Mapper" und klickst diese an:

![](/images/projects/TTN-Mapper/find-ttn-mapper-integration.png)


Gib deine E-Mail Adresse an und gebe einen Experimente Namen an. Du könntest den Experimente Namen auch auslassen, bist dann aber nicht mehr in der Lage deine eigenen Messungen auf dem TTN Mapper zu identifizieren. Außerdem musst du der Integration noch eine beliebige ID geben. Klicke dann auf "Create ttn mapper webhook".

![](/images/projects/TTN-Mapper/ttn-mapper-integration.png)

Zuletzt musst du das Payload Format bei TTN auf Cayenne LPP unstellen. Dazu klickst du auf den Reiter Payload formatters, dann auf Uplink und wählst dann Cayenne LPP aus und klickst auf "Save changes". Nun entschlüsselt TTN die Nachrichten selbstständig nach der [Cayenne LPP Spezifikation](https://developers.mydevices.com/cayenne/docs/lora/#lora-cayenne-low-power-payload).

![](/images/projects/TTN-Mapper/cayenne.png)

## Blockly 

Öffne [Blockly](https://blockly.sensebox.de/ardublockly/?board=sensebox-mcu?lang=de) und beginne mit dem Code für deine senseBox MCU. Um die TTN Infrastruktur zu nutzen müssen wir zunächst eine Activation starten. Dazu nutzen wir die OTAA Activation. Je nach Anwendungsfall kannst Du das Übertragungsintervall anpassen. Bitte denke daran, dass TTN unter einer Fair Use Policy läuft. Das bedeutet, dass man seine Übertragungsrate möglichst gering halten sollte. 

![](/images/projects/TTN-Mapper/blockly-activation-de.png)

Füge nun deine TTN EUIs ein. Achte darauf, dass Du die Keys im richtigen Format einfügst. "Device EUI" und "Application EUI" müssen im ``lsb`` Format genutzt werden. Der "AppKey" im ``msb`` Format. 

Beim Kopieren der Keys musst du deshalb bei TTN in der Device Overview die Einstellungen wie hier gezeigt vornehmen. Du kannst das Format ändern indem Du auf die Icons am Anfang (<> und ⇆) klickst.

![](/images/projects/TTN-Mapper/formatting.png)

Es gibt verschiedene Wege LoRa Daten zu versenden. In diesem Fall nutzen wir das Cayenne Low Power Payload (LPP) da es sehr einfach ist und bereits fertiger Code für diesen Anwendungsfall existiert. Von TTN Mapper gibt es aber folgende Informationen zum Cayenne LPP:

> When using the Cayenne LPP data format, the GPS coordinates will be decoded into a different JSON format which is also supported. Cayenne LPP does not contain the GPS accuracy, and therefore this data will be considered as inferior and will carry less weight in calculation of coverage, and will be deleted first during data cleanup. [Quelle](https://www.thethingsnetwork.org/docs/applications/ttnmapper/)

![](/images/projects/TTN-Mapper/blockly-gps-de.png)

Wähle den `Sende als Cayenne Nachricht` Block und sende eine Koordinaten Messung. Füge die entsprechenden GPS Blöcke ein. Den Channel brauchst Du nicht zu ändern.

Kompiliere nun den Sketch und lade ihn auf die senseBox MCU. Sie sollte nun auf GPS Daten warten und diese zum TTN übertragen. 

Nun kannst du einen Akku anschließen und den LoRa Empfang in deiner Umgebung messen.

## TTN Mapper

Deinen persönlichen TTN Mapper findest Du unter dem Namen deines Experiments. Öffne

[https://ttnmapper.org/experiments/?experiment=EXPERIMENT_NAME](https://ttnmapper.org/experiments/?experiment=EXPERIMENT_NAME)

und ersetze EXPERIMENT_NAME mit dem Namen deines Experiments. Es dauert ein bisschen bis die senseBox GPS Daten empfängt. Zwischendurch kannst Du die Seite neu laden um die neuesten Messungen zu sehen.

![](/images/projects/TTN-Mapper/ttn-mapper.jpeg)

## Hilfe

Du kannst in der TTN Konsole nachschauen ob LoRa Daten bei TTN ankommen. Klicke in deiner Application auf den `Data` Tab und die neusten Nachrichten sollten nach kurzer Zeit auftauchen. Falls keine Nachrichten ankommen schau nochmal über deine EUIs und dessen Format. Ansonsten könnte es sein, dass in deiner Umgebung kein LoRa Gateway in Reichweite ist.

Es kann eine Weile dauern bis das GPS Modul Daten empfängt. Manchmal dauert es mehrere Stunden bei der ersten Nutzung. Wurden aber einmal Daten empfangen sollte es beim nächsten mal schneller funktionieren. Die Nutzung einer kleinen Knopfzelle verbessert den GPS Empfang.
