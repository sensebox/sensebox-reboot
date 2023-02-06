---
layout: project_page
title: "TTN Mapper in unter 10 Minuten"
date: 2020-03-06
author: Felix & Paul
abstract: "Mit dem LoRa-Bee und GPS Modul bauen wir einen senseBox TTN Mapper"
thumbnail: /images/projects/ttn-mapper-de.png

material:
    - senseBox MCU
    - 1x JST-JST-Kabel 
    - 1x LoRa-Bee
    - 1x GPS Modul
ide: blockly  
version: ["edu", "mini v1"]
addons: ["LoRa-Bee", "GPS-Modul"]  
lang: de
tags: ["Geographie", "Informatik", "IoT", "TTN"]
difficult: mittel
image1: /images/projects/TTNv3/add-application.png
image2: /images/projects/TTNv3/add-device.png
image3: /images/projects/TTNv3/register-device.png
image4: /images/projects/TTNv3/register-device-euis.png
image5: /images/projects/TTN-Mapper/add-integration.png
image6: /images/projects/TTN-Mapper/find-ttn-mapper-integration.png
image7: /images/projects/TTN-Mapper/ttn-mapper-integration.png
image8: /images/projects/TTN-Mapper/payload-format.png
image9: /images/projects/TTN-Mapper/blockly-activation-de.png
image10: /images/projects/TTN-Mapper/formatting.png
image11: /images/projects/TTN-Mapper/blockly-gps-de.png
image12: /images/projects/TTN-Mapper/ttn-mapper.jpeg

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

{% include image.html image=page.image1 %}


Nun musst du in deiner neuen Application noch ein Device hinzufügen. Klicke auf "+ Add end Device" und füge ein neues Device (z.B. eine senseBox hinzu).

{% include image.html image=page.image2 %}


Wähle jetzt oben **Manually** aus. Als **Frequency Plan** muss *Europe 863-870 MHz (SF9 for RX2 - recommended)*, als **LoRaWAN version** die Option *MAC V1.0.2* und als **Regional Parameters Version** die Option *PHY V1.0.2 REV A* ausgewählt werden.

{% include image.html image=page.image3 %}

Im nächsten Schritt müssen die EUIs eingetragen werden. Die DevEUI kann von TTNv3 über den Button automatisch generiert werden. Pro Application können jedoch nur 50 EUIs genutzt werden, da diese einmalig sein müssen. Die AppEUI kann über den Button mit Nullen gefüllt werden und der AppKey kann auch wieder automatisch generiert werden.

{% include image.html image=page.image4 %}


Abschließend kannst du deinem Device noch eine ID geben oder die automatisch generierte ID nutzen.

Jetzt kannst du einfach auf **Register end device** klicken und dein Device wird erstellt. 

Fertig, TTN "kennt" nun deine senseBox.

Da wir die Daten später an den TTN Mapper senden möchten, musst Du jetzt noch eine "Integration" hinzufügen. Dafür gehst du im Menü an der Seite auf "Integrations" und dann zu Webhooks. Hier sollte jetzt dieses Menü auftauchen:

{% include image.html image=page.image5 %}

Hier klickst du jetzt auf "+ Add Webhook" in der oberen rechten Ecke. Im nun erscheinenden Auswahlmenü suchst du die Option "TTN Mapper" und klickst diese an:

{% include image.html image=page.image6 %}



Gib deine E-Mail Adresse an und gebe einen Experimente Namen an. Du könntest den Experimente Namen auch auslassen, bist dann aber nicht mehr in der Lage deine eigenen Messungen auf dem TTN Mapper zu identifizieren. Außerdem musst du der Integration noch eine beliebige ID geben. Klicke dann auf "Create ttn mapper webhook".

{% include image.html image=page.image7 %}


Zuletzt musst du das Payload Format bei TTN auf Javascript umstellen und den Decodercode in die Konsole kopieren. Dazu klickst du auf den Reiter Payload formatters, dann auf Uplink und wählst dann Javascript aus. In das nun erscheinende Feld kopierst du folgenden Code 
```
function Decoder(b, port) {
  var lat = (b[0] | (b[1] << 8) | (b[2] << 16) | (b[3] << 24)) / 10000000;
  var lon = (b[4] | (b[5] << 8) | (b[6] << 16) | (b[7] << 24)) / 10000000;
  var alt = (b[8] | (b[9] << 8)) / 10; // in m
  var pdop = (b[10] | (b[11] << 8)) / 100;

  return {
    latitude: lat,
    longitude: lon,
    altitude: alt,
    hdop: pdop,
  };
}
```
und klickst auf "Save changes". Nun entschlüsselt TTN die Nachrichten selbstständig für TTN-Mapper.

{% include image.html image=page.image8 %}

## Blockly 

Öffne [Blockly](https:https://blockly-react.netlify.app/) und beginne mit dem Code für deine senseBox MCU. Um die TTN Infrastruktur zu nutzen müssen wir zunächst eine Activation starten. Dazu nutzen wir die OTAA Activation. Alternativ gibt es auch die ABP Activation, diese ist jedoch in TTN komplizierter einzurichten und wird deshalb hier vermieden. Je nach Anwendungsfall kannst Du das Übertragungsintervall anpassen. Bitte denke daran, dass TTN unter einer Fair Use Policy läuft. Das bedeutet, dass man seine Übertragungsrate möglichst gering halten sollte. 

{% include image.html image=page.image9 %}



Füge nun deine TTN EUIs ein. Achte darauf, dass Du die Keys im richtigen Format einfügst. "Device EUI" und "Application EUI" müssen im ``lsb`` Format genutzt werden. Der "AppKey" im ``msb`` Format. 

Beim Kopieren der Keys musst du deshalb bei TTN in der Device Overview die Einstellungen wie hier gezeigt vornehmen. Du kannst das Format ändern indem Du auf die Icons am Anfang (<> und ⇆) klickst.


{% include image.html image=page.image10 %}

Zum Versenden der Daten an TTN Mapper nutzen wir den neuen TTN Mapper Block in Blockly, hier muss nichts weiter verändert werden:

{% include image.html image=page.image11 %}

Den gesamten Blockly-Sketch findest du [hier](https://blockly.sensebox.de/gallery/63b6d65dd2853f0013b1da8e).

Kompiliere nun den Sketch und lade ihn auf die senseBox MCU. Sie sollte nun auf GPS Daten warten und diese zum TTN übertragen. 

Nun kannst du einen Akku anschließen und den LoRa Empfang in deiner Umgebung messen.

## TTN Mapper

Deinen persönlichen TTN Mapper findest Du unter dem Namen deines Experiments. Öffne

[https://ttnmapper.org/experiments/?experiment=EXPERIMENT_NAME](https://ttnmapper.org/experiments/?experiment=EXPERIMENT_NAME)

und ersetze EXPERIMENT_NAME mit dem Namen deines Experiments. Es dauert ein bisschen bis die senseBox GPS Daten empfängt. Zwischendurch kannst Du die Seite neu laden um die neuesten Messungen zu sehen.

{% include image.html image=page.image12 %}



## Hilfe

Du kannst in der TTN Konsole nachschauen ob LoRa Daten bei TTN ankommen. Klicke in deiner Application auf den `Data` Tab und die neusten Nachrichten sollten nach kurzer Zeit auftauchen. Falls keine Nachrichten ankommen schau nochmal über deine EUIs und dessen Format. Ansonsten könnte es sein, dass in deiner Umgebung kein LoRa Gateway in Reichweite ist.

Es kann eine Weile dauern bis das GPS Modul Daten empfängt. Manchmal dauert es mehrere Stunden bei der ersten Nutzung. Wurden aber einmal Daten empfangen sollte es beim nächsten mal schneller funktionieren. Die Nutzung einer kleinen Knopfzelle verbessert den GPS Empfang.
