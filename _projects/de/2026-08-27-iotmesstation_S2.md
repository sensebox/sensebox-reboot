---
layout: project_page
title: "IoT Messstation"
date: 2026-08-27
author: Joscha
abstract: "Erstelle eine Messstation, die Messwerte für Temperatur und Luftfeuchtigkeit an die openSenseMap schickt."
thumbnail: /images/projects/home.jpg
image0: /images/projects/iot_messstation_S2/0.png
image1: /images/projects/iot_messstation_S2/1.png
image2: /images/projects/iot_messstation_S2/2.png
image3: /images/projects/iot_messstation_S2/3.png
image4: /images/projects/iot_messstation_S2/4.svg
image5: /images/projects/iot_messstation_S2/5.png
material:
  - senseBox MCU-S2
  - 1x OLED Display
  - 1x Temperatur- und Luftfeuchtigkeitssensor (HDC1080)
  - 1x Luftdrucksensor (DPS310)
  - 1x Helligkeits- und UV-Sensor (VEML6070)
  - 4x JST-Kabel
ide: circuitpython
lang: de
version: ["edu-S2"]
tags: ["CircuitPython", "Informatik", "Geographie", "IoT"]
difficult: mittel
---

# IoT Messstation

Ziel dieses Projektes ist es, eine senseBox Umweltstation aufzubauen. Am Ende wird die Messung diverser Umweltphänomene wie Temperatur, Luftfeuchte, Luftdruck und UV-Strahlung, sowie die Veröffentlichung der Daten auf der openSenseMap möglich sein!

## Aufbau

Schließe das Display und die Sensoren deiner Wahl mithilfe der QWIIC-Kabel an den I2C-Anschlüssen der senseBox MCU-S2 an. Du hast nur zwei Anschlüsse, aber drei Sensoren - mithilfe eines QWIIC-Kabels kannt du beispielsweise den Luftdrucksensor an den QWIIC-Anschluss des Temperatur- und Luftfeuchtesensors anschließen. Die Photodiode zur Messung der Beleuchtungsstärke und das WiFi-Modul sind direkt auf dem Board integriert und müssen nicht zusätzlich angeschlossen werden.


<div class="panel panel-success">
  <div class="panel-heading">
  </div>
  <div class="panel panel-success">
    <div class="panel-body">
	Anders, als bei einfachen digitalen oder analogen Eingängen, können mehrere I2C-Geräte (wie z.B. Sensoren oder Displays) parallel geschaltet werden. Jedes Gerät hat dabei eine eindeutige Kennung, damit der Datenbus jedes Einzelne davon zuordnen und separat ansprechen kann.
    </div>
  </div>
</div>

{% include image.html image=page.image0 %}

## Vorbereitung

### Schritt 1: Registrierung auf der openSenseMap

Damit du die Werte deiner Messstation von überall aus abrufen kannst, können die Werte im Internet auf der [openSenseMap](https://www.opensensemap.org/) hochgeladen werden. Dafür muss ein Benutzerkonto auf ebendieser Plattform erstellt werden. Rufe die [openSenseMap](https://www.opensensemap.org/) in einem Internet-Browser auf. Klicke in der oberen Leiste auf den Menüpunkt "Registrierung". Fülle dort alle freien Felder aus. Achte darauf, deine E-Mail Adresse korrekt einzugeben, da du diese für die nächsten Schritte noch benötigst.

{% include image.html image=page.image1 %}

### Schritt 2: Anlegen einer neuen 'senseBox'

Ist die Registrierung abgeschlossen, melde dich an und wähle über das Dropdown Menü (siehe Bild) den Punkt "Neue senseBox" aus. Hier kannst du deiner Messstation einen Namen geben, eine Position angeben und die Phänomene, die du messen möchtest, bestimmen. Wichtig ist, dass du auch nur die Sensoren angibst, die du auch zur Verfügung hast. Nachdem das erledigt ist, siehst du eine Übersicht, in der dir deine registrierte senseBox mit den dazugehörigen Sensoren angezeigt wird.

<div class="panel panel-success">
  <div class="panel-heading">
  Sensor IDs: Die Sensor IDs können genutzt werden, um Sensoren zu unterscheiden. Jede senseBox und jeder Sensor, der auf der [openSenseMap](https://www.opensensemap.org/) registriert ist, besitzt eine einzigartige ID. Beim Hochladen der Messwerte werden diese IDs benötigt, damit die openSenseMap weiß, zu welchen Sensoren die Messwerte gehören.
  </div>
</div>

{% include image.html image=page.image2 %}

## Programmierung

### Schritt 0: Vorbereitung

Lade die benötigten Bibliotheken:
- adafruit_dps310
- adafruit_veml6070
- adafruit_requests
- adafruit_connection_manager
- adafruit_displayio_ssd1306
- adafruit_display_text
- adafruit_bus_device
- adafruit_register 

aus dem [CircuitPython Bundle](https://circuitpython.org/libraries) herunter.  

Beachte dabei, dass du die deiner installierten CircuitPython Version entsprechnde Bundleversion runterlädst. Die Bibliothek für den HDC1080 findest du [hier](https://github.com/sensebox/CircuitPython_HDC1080/archive/refs/heads/main.zip). Kopiere die Bibliotheken auf deine senseBox MCU S2. Dazu muss CircuitPython auf deine senseBox MCU S2 installiert werden. Folge dazu diesem <a href="https://docs.sensebox.de/docs/editors/circuitpython/circuitpython_esp32">Tutorial</a>

### Schritt 1: Bibliotheken importieren

Beim Programmieren mit CircuitPython beginnst du damit, die Bibliotheken von deiner senseBox MCU-S2 in den Code zu importieren.

```python
import time
import board
import digitalio
from hdc1080 import HDC1080
from adafruit_dps310 import DPS310
from adafruit_veml6070 import VEML6070
import wifi
import adafruit_requests
import adafruit_connection_manager
from i2cdisplaybus import I2CDisplayBus
import displayio
import adafruit_displayio_ssd1306
import terminalio
from adafruit_display_text import label
```

### Schritt 2: WLAN und openSenseMap konfigurieren

Nun hinterlegst du die WLAN-Zugangsdaten sowie die benötigten IDs und den Authentifizierungs-Token für die openSenseMap. Diese Werte werden später im Programm verwendet, um die WLAN-Verbindung herzustellen und die Messdaten an die openSenseMap zu übertragen.

```python
# WLAN Zugangsdaten
CIRCUITPY_WIFI_SSID = "Dein_WLAN_Name"
CIRCUITPY_WIFI_PASSWORD = "Dein_WLAN_Passwort"

# openSenseMap Zugangsdaten
SENSEBOX_ID = "Deine_senseBox_ID"
TEMP_SENSOR_ID = "Sensor_ID_fuer_Temperatur"
HUMIDITY_SENSOR_ID = "Sensor_ID_fuer_Luftfeuchtigkeit"
PRESSURE_SENSOR_ID = "Sensor_ID_fuer_Luftdruck"
UV_RAW_SENSOR_ID = "Sensor_ID_fuer_UV"
AUTH_TOKEN = "Dein_Access_Token"
```

### Schritt 2: Hardware initialisieren

Als Nächstes initialisierst du die benötigte Hardware. Dazu aktivierst du zunächst die Stromversorgung der I/O-Schnittstellen und startest die I²C-Verbindung. Anschließend richtest du die angeschlossenen Sensoren sowie das OLED-Display ein, damit alle Komponenten über den gemeinsamen I²C-Bus angesprochen werden können.

```python
# I/O-Stromversorgung der senseBox MCU-S2 aktivieren
io_enable_pin = digitalio.DigitalInOut(board.IO_POWER)
io_enable_pin.direction = digitalio.Direction.OUTPUT
io_enable_pin.value = False

time.sleep(0.5)

# I²C-Schnittstelle initialisieren
i2c = board.I2C()

# Sensoren initialisieren
hdc1080 = HDC1080(i2c)
dps310 = DPS310(i2c, address=0x76)
veml6070 = VEML6070(i2c)

# Display initialisieren
displayio.release_displays()
display_bus = I2CDisplayBus(i2c, device_address=0x3D)
display = adafruit_displayio_ssd1306.SSD1306(
    display_bus,
    width=128,
    height=64
)
``` 

### Schritt 3: Display Layout erstellen

In diesem Schritt legst du fest, welche Informationen später auf dem Display angezeigt werden. Dazu erstellst du zunächst eine gemeinsame Display-Gruppe und anschließend für jeden Messwert ein eigenes Textfeld.

Die Position der einzelnen Textfelder wird über die `x`- und `y`-Werte bestimmt. Anschließend werden alle Textfelder der Gruppe hinzugefügt und diese Gruppe als sichtbarer Inhalt des Displays gesetzt.

```python
# Display-Gruppe erstellen
screen = displayio.Group()

temp_label = label.Label(terminalio.FONT, text="", x=0, y=8)
hum_label = label.Label(terminalio.FONT, text="", x=0, y=24)
press_label = label.Label(terminalio.FONT, text="", x=0, y=40)
uv_label = label.Label(terminalio.FONT, text="", x=0, y=56)

screen.append(temp_label)
screen.append(hum_label)
screen.append(press_label)
screen.append(uv_label)

display.root_group = screen
```

### Schritt 4: WLAN-Verbindung herstellen

Im nächsten Schritt stellst du die WLAN-Verbindung her. Dazu werden die in `settings.toml` hinterlegten Zugangsdaten ausgelesen und die senseBox mit dem angegebenen Netzwerk verbunden.

```python
# Verbindung zum WiFi herstellen
print(f"Connecting to {CIRCUITPY_WIFI_SSID}")
wifi.radio.connect(
    CIRCUITPY_WIFI_SSID, 
    CIRCUITPY_WIFI_PASSWORD
)
print(f"Connected!")
```

### Schritt 5: openSenseMap konfigurieren

Nun wird festgelegt, wohin die Messdaten gesendet werden, und eine Requests-Session für die HTTP-Kommunikation vorbereitet.

```python
# API Endpunkt
OSENSEMAP_HOST = "ingress.opensensemap.org"
OSENSEMAP_PATH = f"/boxes/{SENSEBOX_ID}/data"

# HTTP-Anfragesitzung initialisieren
pool = adafruit_connection_manager.get_radio_socketpool(wifi.radio)
requests = adafruit_requests.Session(pool)
```

### Schritt 6: Messschleife programmieren

In der Messschleife werden die Sensorwerte regelmäßig ausgelesen, zur Kontrolle über die serielle Konsole ausgegeben und auf dem OLED-Display aktualisiert.

```python
# Messschleife
while True:
    try:
        # Sensorwerte auslesen
        temperature = hdc1080.temperature
        humidity = hdc1080.humidity
        pressure = dps310.pressure
        uv_raw = veml6070.uv_raw
        uv_level = veml6070.get_index(uv_raw)

        # Serielle Ausgabe
        print(f"Temperature: {temperature:.2f} °C")
        print(f"Humidity: {humidity:.2f} %")
        print(f"Pressure: {pressure:.2f} hPa")
        print(f"UV Raw: {uv_raw}")
        print(f"UV Risk Level: {uv_level}")
        
        # Display aktualisieren
        temp_label.text = f"Temperature: {temperature:.2f} C"
        hum_label.text = f"Humidity: {humidity:.2f} %"
        press_label.text = f"Pressure: {pressure:.2f} hPa"
        uv_label.text = f"UV Raw: {uv_raw:.2f}"
```

### Schritt 7: Daten auf die openSenseMap übertragen

Anschließend erstellst du im selben `try`-Block das `data`-Objekt mit den aktuellen Messwerten und überträgst diese an die openSenseMap. Nach jeder Messung wartet das Programm 60 Sekunden, bevor der Vorgang erneut beginnt.

```python
        # Daten vorbereiten
        data = {
            TEMP_SENSOR_ID: f"{temperature:.2f}",
            HUMIDITY_SENSOR_ID: f"{humidity:.2f}",
            PRESSURE_SENSOR_ID: f"{pressure:.2f}",
            UV_RAW_SENSOR_ID: f"{uv_raw:.2f}"
        }
        
        # Daten an die openSenseMap senden
        url = f"http://{OSENSEMAP_HOST}{OSENSEMAP_PATH}"
        headers = {
            "Content-Type": "application/json",
            "Authorization": AUTH_TOKEN
        }
        
        print("Sending data to openSenseMap...")
        response = requests.post(url, json=data, headers=headers)
        print(f"Response: {response.text}")
        response.close()
        
    except Exception as e:
        print(f"Error: {e}")
    
    # 60 Sekunden bis zur nächsten Messung warten
    time.sleep(60)
  ``` 
## Gesamter Code

Den fertigen CircuitPython-Code findest du [hier](https://gist.github.com/COSKUNATOR/144eb345021ae4a00889febca8459380).
