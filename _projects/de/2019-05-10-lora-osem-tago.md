---
layout: project_page
title: "LoRaWAN IoT-Wetterstation"
date: 2018-11-02
author: David
abstract: "Das LoRaWAN-Bee wird verwendet, um eine IoT-Wetterstation zu bauen"
thumbnail: /images/projects/Final_Temp.PNG
image1: /images/projects/lora-osem-tago/station_anlegen_ttn.PNG
image2: /images/projects/lora-osem-tago/station_anlegen_ttn_final.PNG
image3: /images/projects/lora-osem-tago/device_anlegen_ttn.PNG
image4: /images/projects/lora-osem-tago/device_anlegen_ttn_overview.PNG
image5: /images/projects/lora-osem-tago/Auswahl_OSEM.PNG
image6: /images/projects/lora-osem-tago/Auswahl_OSEM_2.PNG
image7: /images/projects/lora-osem-tago/osem_zusammenfassung.PNG
image8: /images/projects/lora-osem-tago/device_overview_right_format.PNG
image9: /images/projects/lora-osem-tago/Integration.PNG
image10: /images/projects/lora-osem-tago/tago_add_devices.PNG
image11: /images/projects/lora-osem-tago/Tago_add_dashboard.PNG
image12: /images/projects/lora-osem-tago/sensor_id_erkennen.PNG
image13: /images/projects/lora-osem-tago/Integration_osem.PNG
material:
    - senseBox MCU
    - 3x JST-Kabel 
    - 1x LoRa-Bee
    - 1x Temperatur-/Luftfeuchtigkeitssensor
    - 1x Luftdrucksensor
    - 1x Beleuchtungsstärke-/UV-Sensor
ide: arduino  
version: ["edu", "mini v1", "home"]
addons: ["LoRa-Bee"]  
lang: de
tags: ["Geographie", "Informatik", "LoRa", "TTN", "IoT"]
difficult: schwer
---
# LoRaWAN IoT-Sensorstation

Ziel ist es, eine senseBox Sensorstation mit LoRaWAN Modul zu entwickeln. Die Daten werden über das freie Netzwerk [TheThingsNetwork](https://www.thethingsnetwork.org/) ins Internet gesendet.
Die Messwerte der Sensoren für Beleuchtungsstärke & UV, Temperatur & Luftfeuchtigkeit und Luftdruck sollen dabei übermittelt werden. Anschließend können die Daten zusätzlich zur openSenseMap auch auf der Plattform [tago.io](https://tago.io/) angezeigt werden.

## Grundlagen
Das TheThingsNetwork ist eine communitybasierte Initiative zur Errichtung eines globalen LPWAN-Internet-of-Things-Netzwerks. Über das Netzwerk können kostenlos und über große Distanzen Daten übermittelt werden. Mehr dazu findest du [hier](https://de.wikipedia.org/wiki/The_Things_Network). Bevor du mit dem Projekt beginnst, überprüfe ob ein Gateway - der LoRaWan - in deiner Nähe bereitgestellt ist. Am einfachsten kannst du dies über die Website  [ttnmapper](https://ttnmapper.org/) machen. 

## Aufbau
Die Sensoren werden mit JST-Kabel mit der I2C/Wire Ports der senseBox MCU verbunden. Das LoRa-Bee wird auf den XBEE1 Steckplatz gesteckt.

>Beachte: Es gibt zwei verschiedene Luftdruck-Sensoren (BMP280 & DPS310). Anhand der Beschriftung auf dem Luftdruck-Sensor kannst du deinen Typ identifizieren. Achte bei der Programmierung darauf, dass du den richtigen Sensorblock auswählst. 

## Registrierung bei TheThingsNetwork und auf der openSenseMap

Für dieses Beispiel musst du nicht programmieren, sondern nutzt den Sketch der von der openSenseMap generiert wird. Um den Code richtig generieren zu lassen, brauchst du jedoch einige Informationen aus dem TheThingsNetwork.

### Registrierung auf TheThingsNetwork und anlegen einer Application

Besuche die Website [thethingsnetwork.org](https://www.thethingsnetwork.org/) und erstelle einen Account. Wenn du eingeloggt bist, siehst du in der Kopfzeile auf der rechten Seite der Startseite deinen Nutzernamen. Klicke darauf, um ein Dropdown-Menü zu öffnen, und wähle dort **"Console"**. Als Nächstes musst du einen Network-Cluster auswählen. Wenn du in Europa bist, wähle **"Europe1"**. Nun befindest du dich in der Konsolen-Umgebung von *The Things Network*. Um Daten an *The Things Network* senden zu können, klicke hier auf **"Create Application"**. 

{% include image.html image=page.image1 %}


Gib anschließend eine eindeutige *Application ID* an. Alle anderen Auswahlmöglichkeiten kannst du unverändert lassen. Wenn du zufrieden bist kannst du auf "Create Application" klicken, um die App bei TheThingsNetwork zu registrieren.

{% include image.html image=page.image2 %}

Nun musst du in deiner neuen Application noch ein Device hinzufügen. Gehe dafür unter der Rubrik **"Devices"** auf "register device". Klicke auf **"Enter end device specifics manually"** um Frequenz, LoRaWAN Version und Regionale Parameter wie im Screenshot zu setzen. Als **"JoinEUI"** kannst du eine Zahlenfolge aus Nullen eingeben.

{% include image.html image=page.image3 %}

Klicke dann auf **"Confirm"**. Als nächstes musst du **"DevEUI"**, **"AppKey"** und **"NwkKey"** generieren, indem du an den entsprechenden Stellen auf **"Generate"** klickst. Zuletzt musst du noch eine einzigartige **"Device ID"** angeben. Wenn du nun auf **"Register end device"** klickst, kommst du auf eine Übersichtsseite mit allen Informationen zu deinem registrierten Gerät.

{% include image.html image=page.image4 %}

Im letzten Schritt müssen die Daten von TTN zur openSenseMap weitergeleitet werden. Füge dazu der TTN Application eine neue Webhook Integration hinzu. Die möglichkeit dazu findest du in der TTN Konsole im Menü auf der linken Seite. Nach einem Klick auf **"+ Add webhook"** wähle **"Custom webhook"** und gib dem neuen Webhook eine ID, z.B. osem. Als Webhook Format wähle JSON aus und die Base URL für den Endpoint ist https://ttn.opensensemap.org/v3. Außerdem muss noch Uplink messages aktiviert wreden. Der Rest der Einstellungen kann so bleiben, wie sie sind. Nun ganz unten auf **“Add webhook”** klicken und schon ist die Weiterleitung zur openSenseMap eingerichtet.

{% include image.html image=page.image13 %}


### Registrierung auf der openSenseMap

Falls du noch keinen Account hast, registriere dich auf der openSenseMap und lege eine neue senseBox an. Akzeptiere die Datenschutzerklärung und gib der Station einen Namen. Gib an, ob die Station drinnen oder draußen steht. Wähle deinen Standort und wähle anschließend in der Rubrik Hardware die "senseBox:home V2" aus. Wähle dann dein Set-up mit LoRa-Bee und den verwendeten Sensoren.

{% include image.html image=page.image5 %}

Da du das LoRa-Bee gewählt hast, öffnet sich automatisch die Rubrik TheThingsNetwork - TTN. Dort musst du nun die "Application ID" und die "Device ID" eingeben, wie du diese bei TTN bestimmt hast.

{% include image.html image=page.image6 %}

Du kommst dann auf eine Übersichtsseite. Dort musst du **"Device EUI"**, **"Application EUI"** und **"Application Key"** angeben. Als nächstes kannst dort auf "Compile" klicken und erhälst eine Zusammenfassung. In dieser findest du auch den Arduino Code, der schon für deine Station vorbereitet ist und nur noch kompiliert, runtergeladen und auf das Gerät gespielt werden muss.

{% include image.html image=page.image7 %}

Wie du in der Beschreibung des Codes lesen kannst, ist es hier wichtig, das Format der Schlüssel richtig einzusetzen. Die "Device EUI" und die "Application EUI" werden im 
```lsb``` Format kopiert und eingefügt. Der AppKey im ```msb``` Format. 

Beim Kopieren der Schlüssel musst du deshalb darauf achten, dass deine Device Overview wie im folgenden Bild eingestellt ist. Du kannst das Format der Darstellung ändern,
indem du auf die Icons am Anfang drückst (<> und ->)

{% include image.html image=page.image8 %}

## Sensordaten mithilfe TagoIO auf dem Handy darstellen

Abschließend möchten wir noch eine kleine Funktion vom Anbieter tago.io benutzen, durch die man Daten seiner auf TheThingsNetwork registrierten Stationen in einem Dashboard ansehen kann.

Gehe dafür in deinem TTN-Profil auf deine Application und wähle "Webhook". Dort sollte es jetzt bereits eine Webhook geben, welche benutzt wird, um die Daten an die openSenseMap zu schicken. Wähle dort nun **"+ Add webhook"** und wähle **"TagoIO"**. Dann kannst du eine eindeutige ID frei wählen und musst dir außerdem eine "Autorization" aussuchen. Diese brauchst du später wieder, um auf deine Werte zugreifen zu können. 

{% include image.html image=page.image9 %}

    
Gehe nun auf https://tago.io und lege dir einen Account an. Wähle „I am Developer“, da du später eigene Geräte anlegen möchtest. 
In der Übersicht deines Accounts findest du nun die Option „Devices“. Klicke dort auf „Add Device“ und wähle dann die Option „Custom The Things Network“ aus.
Gib deinem Device einen Namen und eine kurze Beschreibung. Danach musst du noch die Device EUI aus TTN kopieren und einfügen. 
Diese findest du wieder unter der „Device Overview“ in deinem TTN Account. Dann musst du auch noch deinen vorher gewählten Authorization Code eingeben. 
Abschließend klickst du auf „Create Device“ und bist fertig. 

{% include image.html image=page.image10 %}


Nun kannst du auf die Sensorwerte des Devices zugreifen und deine eigenen Dashboards bauen. Gehe dazu auf „Dashboards“ in deinem TagoIO Account und wähle „Add Dashboard“. 
Gib dem Dashboard einen Namen und klicke auf „Add Widget“. Hier kannst du zwischen verschiedenen Darstellungsweisen der Werte wählen. Hier wird im Folgenden ein „Line“ Diagramm gewählt.

{% include image.html image=page.image11 %} 


Gib dem Diagramm einen Titel und wähle dann dein Device aus, falls du mehrere hast. Nun gibst du noch die Variable, die du ausgeben möchtest, ein. Hier wählst du die Sensor ID deiner senseBox aus. 
Welche Sensor ID zu welchem Sensor gehört, findest du in deinem openSenseMap Account unter dem Punkt „Sensors“. In diesem Fall wurde der Temperaturwert gewählt und kann nun angezeigt werden. 

{% include image.html image=page.image12 %} 

Da es auch eine App von TagoIO gibt, ist das auch eine gute Möglichkeit, deine Sensorwerte mobil anzuzeigen.
Es stehen dir natürlich auch weitere Dashboards und Optionen über TagoIO zur Verfügung. 
