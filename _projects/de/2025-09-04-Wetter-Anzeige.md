---
layout: project_page
title: "Weather Indication"
date: 2025-08-03
author: Lavinia
abstract: "Das Display zeigt das Wetter an. Das Wetter wird mit Symbolen dargestellt."
thumbnail: /images/projects/Titelbild_Wetter_Anzeige.png
image0: /images/projects/Wetter-Anzeige/blocklySunnImage.png
image1: /images/projects/Wetter-Anzeige/Hardware_weather_indication.jpeg
image2: /images/projects/Wetter-Anzeige/sonnyScreen.svg

material: 
  - 1x SenseBox MCU S2
  - 1x Luftdruck- und Temperatursensor (DPS310)
  - 1x OLED-Display
  - 1x RGB-LED-Matrix
ide: arduino
version: ["edu-S2"]
lang: de
tags: ["Informatik"]
difficult: leicht
---


# Wetter Anzeige

Ziel dieses Projektes ist es, auf dem Display das Wetter darzustellen und gleichzeitig das passende Symbol auf der LED-Matrix leuchten zu lassen.  
Mit dem Sensor werden Temperatur und Luftdruck gemessen. Diese Werte können auf dem Display abgelesen werden. Auf der LED-Matrix erscheint dann ein passendes Symbol, zum Beispiel eine Sonne bei warmem Wetter oder Wolken bei niedrigem Luftdruck.


## Aufbau

1. Schließe das **Display** mit einem QWIIC-Kabel an einen **I2C-Port** an.  
2. An das Display wird der **Sensor** ebenfalls mit einem QWIIC-Kabel angeschlossen.  
3. Verbinde die **LED-Matrix** mit einem QWIIC-Kabel und schließe sie an **Port A** der GPIO-Schnittstelle an.  

{% include image.html image=page.image1 %}

Damit ist der Aufbau schon abgeschlossen.


## Programmierung

Für die Programmierung nutzen wir die [Arduino IDE](https://www.arduino.cc/en/software).  
Zuerst benötigen wir die passenden **Libraries** (= Software-Bibliotheken). Danach programmieren wir:

1. Die **Wettersymbole** für die LED-Matrix.  
2. Das **Initialisieren** des Sensors.  
3. Die **Ausgabe auf dem Display**, wo Temperatur und Luftdruck angezeigt werden.  


### Schritt 1: Libraries importieren

Für das Projekt brauchen wir folgende Libraries, die du über den **Library Manager** der Arduino IDE installieren kannst:

- `Adafruit_DPS310` (für den Sensor)  
- `Adafruit_SSD1306` (für das Display)  
- `Adafruit_GFX` (für die LED-Matrix)  
- `Adafruit_NeoMatrix` und `Adafruit_NeoPixel` (für die LED-Matrix)

Der Code für die Einbindung sieht so aus:

```arduino
#include <Adafruit_NeoPixel.h>
#include <Adafruit_NeoMatrix.h>
#include <Adafruit_GFX.h> 
#include <Adafruit_DPS310.h> 
#include <SPI.h>
#include <Wire.h>
#include <Adafruit_SSD1306.h>
```
*(Du weißt noch nicht, was Libraries sind und wie du sie importieren kannst? Kein Problem! Hier findest du weitere Informationen: [Hinzufügen einer Arduino Software Bibliothek](https://docs.sensebox.de/docs/editors/arduino/libraries-hinzufuegen/))* 

Anschließend richten wir Sensor, Display und LED-Matrix ein:

```arduino
// LED-Matrix:
#define WIDTH 12
#define HEIGHT 8
Adafruit_NeoMatrix matrix_2 = Adafruit_NeoMatrix(
    WIDTH, HEIGHT, 2,
    NEO_MATRIX_TOP + NEO_MATRIX_LEFT + NEO_MATRIX_ROWS + NEO_MATRIX_ZIGZAG,
    NEO_GRB + NEO_KHZ800
);

// Display:
#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET -1
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

// Sensor:
Adafruit_DPS310 dps;
```

### Schritt 2: Wettersymbole

In der LED-Matrix wollen wir zuerst Symbole definieren. Nutze dafür den [Code Editor von senseBox-Blockly](https://blockly.sensebox.de/).  

1. Wähle links die LED-Matrix.  
2. Nutze den Block **„Zeichne Bitmap“**.  
3. Lege mit Klicks fest, welche LEDs leuchten sollen (schwarz = aus).  
4. Gib dem Motiv einen Namen (z. B. `Sonne`).  
5. Kopiere den generierten Code-Abschnitt in deinen Arduino-Code.  

{% include image.html image=page.image0 %}

Beispielsymbole: Sonne ☀️, Wolken ☁️, Sonne mit Wolken 🌤️, Schneeflocke ❄️.  
(Weiter unten findest du fertige Symbole)

### Schritt 3: Anzeige auf dem Display

Das Display soll Temperatur und Luftdruck anzeigen. Dafür schreiben wir eine Methode, die Textgröße, Farbe und Position definiert:

```arduino
void printOnDisplay(String title, String measurement, String unit,
                    String title2, String measurement2, String unit2) {

  display.setCursor(0, 0);
  display.setTextSize(1);
  display.setTextColor(WHITE, BLACK);
  display.println(title);
  display.setCursor(0, 10);
  display.setTextSize(2);
  display.print(measurement);
  display.print(" ");
  display.setTextSize(1);
  display.println(unit);

  display.setCursor(0, 30);
  display.setTextSize(1);
  display.setTextColor(WHITE, BLACK);
  display.println(title2);
  display.setCursor(0, 40);
  display.setTextSize(2);
  display.print(measurement2);
  display.print(" ");
  display.setTextSize(1);
  display.println(unit2);
  display.display();
}
```

### Schritt 4: Setup

In der `setup()`-Funktion starten wir Sensor, Display und LED-Matrix:

```arduino
void setup() {
  // LED-Matrix
  matrix_2.setBrightness(20);
  matrix_2.setTextWrap(false);
  matrix_2.begin();

  // Display
  display.begin(SSD1306_SWITCHCAPVCC, 0x3D);
  display.display();
  delay(100);
  display.clearDisplay();

  // Sensor
  dps.begin_I2C(0x76);
  dps.configurePressure(DPS310_64HZ, DPS310_64SAMPLES);
  dps.configureTemperature(DPS310_64HZ, DPS310_64SAMPLES);
}
```
*(Da diese Funktionen nicht spezifisch für dieses Projekt sind, gehen wir hier nicht ins Detail. Wenn du mehr Informationen dazu möchtest, 
hilft zum Beispiel die [Arduino Dokumentation](https://docs.arduino.cc/) weiter.)*

### Schritt 5: loop() – Anzeige und Bedingungen

Im letzten Schritt befinden wir uns in der loop()-Methode. Alles, was in dieser Methode steht, wiederholt sich ständig in einer Schleife.
Mit `delay(5000);` legen wir fest, dass der Ablauf jeweils 5 Sekunden pausiert. Dadurch passiert alles in einem 5-Sekunden-Takt.

Zuerst setzen wir die LED-Matrix zurück, damit sie ein neues Bild anzeigen kann:
```arduino
  matrix_2.fillScreen(0);
  matrix_2.show();
```

Danach fragen wir die Werte unseres Sensors ab:
```arduino
  sensors_event_t temp_event, pressure_event;
  dps.getEvents(&temp_event, &pressure_event);
```

Anschließend rufen wir die Display-Methode auf, die wir in Schritt 3 erstellt haben, und übergeben die Messwerte, damit Temperatur und Luftdruck auf dem Display angezeigt werden:
```arduino
  printOnDisplay("Temperatur", String(temp_event.temperature), "Grad","Luftdruck", String(pressure_event.pressure), "hPa");
```
Nun haben wir unsere Messwerte auf dem Display. Jetzt fehlt noch die Bedingung, die entscheidet, welches Symbol auf der LED-Matrix erscheinen soll.
Wir orientieren uns dabei an diesen Werten (du kannst sie bei Bedarf anpassen): 

- **Sonne**: ab 20 °C und Luftdruck > 1020 hPa  
- **Sonne mit Wolken**: unter 20 °C und Luftdruck < 1020 hPa  
- **Wolken**: unter 15 °C und Luftdruck < 1000 hPa  
- **Schnee**: unter 5 °C  

Dafür nutzen wir eine if-else-Abfrage. Damit prüfen wir die Bedingungen und lassen das richtige Symbol erscheinen.
*(Infos zu "wenn-dann"-Bedingungen findest du auf der [Lernkarte](https://sensebox.de/de/lernkarten-s2) GI02)*.

```arduino
  if ((temp_event.temperature > 20 || pressure_event.pressure > 1020)) {
    matrix_2.drawRGBBitmap(0, 0, bitmap_sonny, WIDTH, HEIGHT);
    matrix_2.show();
  }
```
Hier prüfen wir zuerst, ob die Temperatur über 20 °C liegt oder der Luftdruck größer als 1020 hPa ist.
Wenn das stimmt, wird auf der LED-Matrix das Symbol `bitmap_sonny` (also die Sonne) angezeigt.

Das machen wir anschließend genauso für die anderen Symbole. Du kannst auch eigene Symbole hinzufügen.

So sieht die fertige `loop()`-Methode aus:
```arduino
void loop() {
  delay(5000);
  matrix_2.fillScreen(0);
  matrix_2.show();

  sensors_event_t temp_event, pressure_event;
  dps.getEvents(&temp_event, &pressure_event);

  printOnDisplay("Temperatur", String(temp_event.temperature), "Grad",
                 "Luftdruck", String(pressure_event.pressure), "hPa");

  if ((temp_event.temperature > 20 || pressure_event.pressure > 1020)) {
    matrix_2.drawRGBBitmap(0, 0, bitmap_sonny, WIDTH, HEIGHT);
    matrix_2.show();
  } else if ((temp_event.temperature < 20 || pressure_event.pressure < 1020)) {
    matrix_2.drawRGBBitmap(0, 0, bitmap_cloudAndSunny, WIDTH, HEIGHT);
    matrix_2.show();
  } else if ((temp_event.temperature < 15 || pressure_event.pressure < 1000)) {
    matrix_2.drawRGBBitmap(0, 0, bitmap_cloud, WIDTH, HEIGHT);
    matrix_2.show();
  } else if (temp_event.temperature < 5) {
    matrix_2.drawRGBBitmap(0, 0, bitmap_snow, WIDTH, HEIGHT);
    matrix_2.show();
  }
}
```

### Extra: fertige Symbole

#### ☀️ Sonne: 
```arduino
 const uint16_t bitmap_sonny[] =  {0x0, 0x0, 0x0, 0x0, 0x0, 0xffe0,
  0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0xffe0, 0x0, 0x0, 0x0, 0xffe0, 
  0x0, 0x0, 0xffe0, 0x0, 0x0, 0x0, 0x0, 0x0, 0xffe0, 0x0, 0x0, 0xffe0,
  0x0, 0xffe0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0xffe0, 0xffe0, 
  0xffe0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0xffe0, 0xffe0, 0xffe0, 0xffe0, 
  0xffe0, 0xffe0, 0xffe0, 0xffe0, 0xffe0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0,
  0xffe0, 0xffe0, 0xffe0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0xffe0,
  0x0, 0x0, 0x0, 0xffe0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0xffe0, 0x0, 0x0, 
  0x0, 0x0, 0x0, 0xffe0, 0x0, 0x0, 0x0,
};
```
#### 🌤️ Sonne mit Wolken: 
```arduino
const uint16_t bitmap_cloudAndSunny[] = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0,
0x0, 0x0, 0x0, 0x0, 0x9fff, 0x0, 0x0, 0x0, 0xffe0, 0xffe0, 0xffe0, 0x0,
0x0, 0x0, 0x0, 0x9fff, 0x9fff, 0x9fff, 0x0, 0xffe0, 0xffe0, 0xffe0, 0xffe0, 0xffe0,
0x0, 0x0, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0xffe0, 0xffe0, 0xffe0, 0xffe0, 0xffe0,
0x0, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0xffe0, 0x9fff, 0x9fff, 0xffe0, 0xffe0,
0x0, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0xffe0,
0x0, 0x0, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x0,
0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0,
};
```

#### ☁️ Wolken: 
```arduino
const uint16_t bitmap_cloud[] =  {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0,
0x0, 0x0, 0x0, 0x0, 0x9fff, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0,
0x0, 0x0, 0x0, 0x9fff, 0x9fff, 0x9fff, 0x0, 0x0, 0x9fff, 0x9fff, 0x0, 0x0,
0x0, 0x0, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x0,
0x0, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff,
0x0, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff,
0x0, 0x0, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x9fff, 0x0,
0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0,
};
```

#### ❄️ Schneeflocke: 
```arduino
const uint16_t bitmap_snow[] = {0x0, 0x0, 0x0, 0x0, 0xcfff, 0x0, 0xcfff, 0x0, 0x0, 0x0, 0x0, 0x0,
0x0, 0x0, 0xcfff, 0x0, 0x0, 0xcfff, 0x0, 0x0, 0xcfff, 0x0, 0x0, 0x0,
0x0, 0x0, 0x0, 0xcfff, 0x0, 0xcfff, 0x0, 0xcfff, 0x0, 0x0, 0x0, 0x0,
0x0, 0x0, 0x0, 0x0, 0xcfff, 0xcfff, 0xcfff, 0x0, 0x0, 0x0, 0x0, 0x0,
0x0, 0x0, 0x0, 0x0, 0xcfff, 0xcfff, 0xcfff, 0x0, 0x0, 0x0, 0x0, 0x0,
0x0, 0x0, 0x0, 0xcfff, 0x0, 0xcfff, 0x0, 0xcfff, 0x0, 0x0, 0x0, 0x0,
0x0, 0x0, 0xcfff, 0x0, 0x0, 0xcfff, 0x0, 0x0, 0xcfff, 0x0, 0x0, 0x0,
0x0, 0x0, 0x0, 0x0, 0xcfff, 0x0, 0xcfff, 0x0, 0x0, 0x0, 0x0, 0x0,
};
```

## Gesamter Code

Den gesamten Code findest du hier: [Projekt-Code auf Github](https://github.com/sensebox/sensebox-examples/blob/main/Weather-Indication/weather-indication.ino)