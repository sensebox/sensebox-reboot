---
layout: project_page
title: "Brick Breaker"
date: 2025-10-09
author: Kieran Galbraith
abstract: "Programmiere das klassische Spiel 'Brick Breaker' mit CircuitPython und dem OLED Display."
thumbnail: /images/projects/brick-breaker_thumbnail.jpg
material:
  - senseBox MCU-S2 (Version 2.1)
  - 1x OLED Display
  - 1x QWIIC-Kabel
  - Integrierter MPU6050 Beschleunigungssensor (auf dem Board)
ide: circuitpython
lang: de
version: ["edu-S2"]
tags: ["CircuitPython", "edu-S2", "Spiele", "Spiel", "Informatik"]
difficult: schwer
---

# Brick Breaker mit CircuitPython

> **Hinweis zur Zielgruppe und Voraussetzungen**  
> Dieses Projekt richtet sich an Lernende **ab etwa 13 Jahren** mit **grundlegenden Python-Kenntnissen** (z. B. Variablen, Schleifen, Funktionen). Es wird empfohlen, bereits erste Erfahrungen mit der **senseBox:edu S2** und **CircuitPython** gesammelt zu haben – beispielsweise durch einfachere Projekte wie „Blinkende LED“ oder „Temperatur messen“.
>
> **Was ist der MPU6050?**  
> Der MPU6050 ist ein kombinierter Sensor, der sowohl **Beschleunigung** (Neigung der Box) als auch **Drehbewegungen** (Gyroskop) misst. In diesem Projekt nutzen wir **nur die Neigungsdaten des Beschleunigungssensors**, um das Paddle zu steuern – du musst das Gyroskop also nicht verstehen, um mitzumachen!

In diesem Projekt programmierst du das klassische Arcade-Spiel Brick Breaker mit CircuitPython. Du steuerst ein Paddle durch Neigen der senseBox, um einen Ball zu lenken und alle Blöcke zu zerstören. Das Spiel nutzt den integrierten Beschleunigungssensor zur Steuerung und das OLED Display zur Anzeige.

## Lernziele

- Grundlagen der Spieleprogrammierung mit CircuitPython
- Verwendung des Beschleunigungssensors zur Bewegungserkennung
- Grafische Darstellung auf dem OLED Display
- Kollisionserkennung und Spiellogik

## Aufbau

Schließe das OLED Display mit einem QWIIC-Kabel an einen der I2C-Anschlüsse der senseBox MCU-S2 an. Der MPU6050 Beschleunigungssensor ist bereits auf dem Board integriert und muss nicht zusätzlich angeschlossen werden.

> **⚠️ Wichtiger Hinweis zur Hardware (senseBox MCU-S2, Version 2.1)**  
> Diese Anleitung setzt spezifische Hardwareeinstellungen voraus:
>
> - Der **`IO_POWER`-Pin** muss auf **`False`** gesetzt werden (nicht `True` wie bei anderen Boards).
> - Das **OLED-Display** verwendet die I²C-Adresse **`0x3D`**.
> - Der **integrierte MPU6050** nutzt die GPIO-Pins **42 (SCL)** und **45 (SDA)** für I²C.
>
> Diese Einstellungen sind im Beispielcode bereits korrekt implementiert.

<p align="center">
  <img src="/images/projects/brick-breaker/brick-breaker_setup.jpg" alt="Setup für das Brick Breaker Spiel" width="400">
</p>

<p align="center"><em>Abbildung: Aufbau des Brick Breaker Setups</em></p>

## Programmierung

### Schritt 0: Vorbereitung

Lade die benötigten Bibliotheken <a href="https://github.com/adafruit/Adafruit_CircuitPython_DisplayIO_SSD1306/releases/download/3.0.3/adafruit-circuitpython-displayio-ssd1306-10.x-mpy-3.0.3.zip">SSD1306</a>, <a href="https://github.com/adafruit/Adafruit_CircuitPython_Display_Text/releases/download/3.3.3/adafruit-circuitpython-display-text-10.x-mpy-3.3.3.zip ">adafruit_display_text</a> <b>und</b> <a href="https://github.com/adafruit/Adafruit_CircuitPython_MPU6050/releases/download/1.3.4/adafruit-circuitpython-mpu6050-10.x-mpy-1.3.4.zip">MPU6050</a> herunter und kopiere die Bibliotheken auf deine senseBox MCU S2. Dazu muss CircuitPython auf deine senseBox MCU S2 installiert werden. Folge dazu diesem <a href="https://docs.sensebox.de/docs/editors/circuitpython/circuitpython_esp32">Tutorial</a>

### Schritt 1: Bibliotheken importieren

Beim Programmieren mit CircuitPython beginnst du damit, die Bibliotheken von deiner senseBox MCU S2 in den Code zu importieren.

```python
import time
import board
import displayio
import digitalio
import busio
import microcontroller
from i2cdisplaybus import I2CDisplayBus
import adafruit_displayio_ssd1306
import adafruit_mpu6050
import math
```

### Schritt 2: Hardware initialisieren

Als Nächstes initialisierst du die angeschlossenen Komponenten: Den Bildschirm und den eingebauten Beschleunigungssensor. Damit legst du fest, wie deine senseBox mit diesen Komponenten kommuniziert.

```python
# Enable IO power
io_enable_pin = digitalio.DigitalInOut(board.IO_POWER)
io_enable_pin.direction = digitalio.Direction.OUTPUT
io_enable_pin.value = False

time.sleep(0.5)

# Initialize display
displayio.release_displays()
i2c_display = board.I2C()
display_bus = I2CDisplayBus(i2c_display, device_address=0x3D)
display = adafruit_displayio_ssd1306.SSD1306(display_bus, width=128, height=64)

# Initialize MPU6050
scl = microcontroller.pin.GPIO42
sda = microcontroller.pin.GPIO45
i2c_mpu = busio.I2C(scl, sda)
mpu = adafruit_mpu6050.MPU6050(i2c_mpu)
```

### Schritt 3: Spielkonstanten definieren

In diesem Schritt wollen wir die Spielkonstanten definieren: Den Ball, den steuerbaren Paddle und die Bricks, die mit dem Ball getroffen werden sollen. Die verschiedenen Komponenten des Spiels werden nur definiert und noch nicht auf dem Bildschirm eingezeichnet.

```python
# Game constants
PADDLE_WIDTH = 20
PADDLE_HEIGHT = 3
PADDLE_Y = 58
PADDLE_SPEED = 2.0

BALL_SIZE = 2
BALL_SPEED = 1.5

BRICK_WIDTH = 12
BRICK_HEIGHT = 4
BRICK_ROWS = 3
BRICK_COLS = 10
BRICK_SPACING = 1

# Game state
paddle_x = 54  # Center position
ball_x = 64.0
ball_y = 50.0
ball_dx = 0.0
ball_dy = 0.0
game_started = False
game_over = False
game_won = False

# Bricks array (True = exists, False = destroyed)
bricks = [[True for _ in range(BRICK_COLS)] for _ in range(BRICK_ROWS)]
```

### Schritt 4: Display Funktionen erstellen

Nachfolgend wollen wir Funktionen erstellen, um das Spiel auf dem Display darzustellen. Wir zeigen an dieser Stelle noch nichts auf dem Display an, sondern erstellen Funktionen, auf die wir später zugreifen. Dafür legen wir die möglichen Positionen der Spielelemente fest. Der Ball soll sich beispielsweise über das gesamte Display bewegen können, er benötigt also variable X- und Y-Koordinaten. Das Paddle dagegen soll sich nur auf der X-Achse am unteren Rand bewegen können und braucht daher nur eine Koordinate. Die Bricks sollen sich nicht bewegen. Sie sollen sich aber schwarz verfärben, wenn sie getroffen werden, sodass es so aussieht, als wären sie nicht mehr vorhanden.

```python
def create_display():
    """Create initial display with bricks and paddle"""
    group = displayio.Group()

    # Background
    bg_bitmap = displayio.Bitmap(128, 64, 1)
    bg_palette = displayio.Palette(1)
    bg_palette[0] = 0x000000 # Black color
    bg_sprite = displayio.TileGrid(bg_bitmap, pixel_shader=bg_palette)
    group.append(bg_sprite)

    # Draw bricks
    brick_palette = displayio.Palette(1)
    brick_palette[0] = 0xFFFFFF # White color

    for row in range(BRICK_ROWS):
        for col in range(BRICK_COLS):
            if bricks[row][col]:
                x = col * (BRICK_WIDTH + BRICK_SPACING) + 4
                y = row * (BRICK_HEIGHT + BRICK_SPACING) + 4
                brick_bitmap = displayio.Bitmap(BRICK_WIDTH, BRICK_HEIGHT, 1)
                brick_sprite = displayio.TileGrid(
                    brick_bitmap,
                    pixel_shader=brick_palette,
                    x=x,
                    y=y
                )
                group.append(brick_sprite)

    return group

def draw_paddle(group, x):
    """Draw paddle at position"""
    paddle_palette = displayio.Palette(1)
    paddle_palette[0] = 0xFFFFFF
    paddle_bitmap = displayio.Bitmap(PADDLE_WIDTH, PADDLE_HEIGHT, 1)
    paddle_sprite = displayio.TileGrid(
        paddle_bitmap,
        pixel_shader=paddle_palette,
        x=int(x),
        y=PADDLE_Y
    )
    group.append(paddle_sprite)
    return paddle_sprite

def draw_ball(group, x, y):
    """Draw ball at position"""
    ball_palette = displayio.Palette(1)
    ball_palette[0] = 0xFFFFFF # White color
    ball_bitmap = displayio.Bitmap(BALL_SIZE, BALL_SIZE, 1)
    ball_sprite = displayio.TileGrid(
        ball_bitmap,
        pixel_shader=ball_palette,
        x=int(x),
        y=int(y)
    )
    group.append(ball_sprite)
    return ball_sprite
```

### Schritt 5: Kollisionserkennung

Die Kollisionserkennung gehört zu den wichtigsten Bausteinen des Spiels. Wenn der Ball einen Brick berührt, soll dieser aus dem Spiel entfernt werden. Berührt der Ball das Paddle, soll er in die entgegengesetzte Richtung zurückgespielt werden. Das klingt komplizierter, als es ist: Wir müssen lediglich mit einigen if-Abfragen die Position des Balls überprüfen. Außerdem wollen wir in diesem Schritt festlegen, wann der Spieler das Spiel gewonnen hat. Nämlich dann, wenn keine Bricks mehr übrig sind. Was genau passiert, wenn eine Kollision erkannt wird, legen wir im nächsten Schritt fest.

```python
def check_brick_collision(x, y):
    """Check if ball hits a brick and remove it"""
    global bricks

    for row in range(BRICK_ROWS):
        for col in range(BRICK_COLS):
            if bricks[row][col]:
                brick_x = col * (BRICK_WIDTH + BRICK_SPACING) + 4
                brick_y = row * (BRICK_HEIGHT + BRICK_SPACING) + 4

                if (x < brick_x + BRICK_WIDTH and
                    x + BALL_SIZE > brick_x and
                    y < brick_y + BRICK_HEIGHT and
                    y + BALL_SIZE > brick_y):
                    bricks[row][col] = False
                    return True
    return False

def check_paddle_collision(ball_x, ball_y, paddle_x):
    """Check if ball hits paddle"""
    if (ball_y + BALL_SIZE >= PADDLE_Y and
        ball_y <= PADDLE_Y + PADDLE_HEIGHT and
        ball_x + BALL_SIZE >= paddle_x and
        ball_x <= paddle_x + PADDLE_WIDTH):
        return True
    return False

def check_win():
    """Check if all bricks are destroyed"""
    for row in bricks:
        if any(row):
            return False
    return True
```

### Schritt 6: Gameplay-Loop

Zum Schluss wollen wir den sogenannten "Gameplay-Loop" definieren. Wir legen also fest, wann das Spiel startet und endet, wie es gesteuert wird und was genau dazwischen passiert. Im Grunde erstellen wir hier das Herz des Spiels. Erst jetzt wird das Programm wirklich zu einem Spiel.

Zunächst nutzen wir die Funktionen aus Schritt 4, um die Spielelemente auf dem Display anzuzeigen und geben in der Python-Konsole am Rechner Informationen über das Spiel aus.

```python
# Initialize display
display_group = create_display()
paddle_sprite = draw_paddle(display_group, paddle_x)
ball_sprite = draw_ball(display_group, ball_x, ball_y)
display.root_group = display_group

print("Brick Breaker Started!")
print("Tilt to move paddle")
print("Shake to start the game")
```

Danach legen wir den Spielstart mithilfe des Beschleunigungssensors fest. Dazu müssen wir die Werte des Sensors auslesen und bestimmen, ab welchen Werten das Schütteln der senseBox als Spielstart erkannt wird.

```python
while True:
    # Read accelerometer
    accel_x, accel_y, accel_z = mpu.acceleration

    # Check for shake (start/reset)
    if abs(accel_x) > 15 or abs(accel_y) > 15 or abs(accel_z) > 15:
        if game_over or game_won:
            # Reset game
            ball_x = 64.0
            ball_y = 50.0
            ball_dx = 0.0
            ball_dy = 0.0
            paddle_x = 54
            game_started = False
            game_over = False
            game_won = False
            bricks = [[True for _ in range(BRICK_COLS)] for _ in range(BRICK_ROWS)]

            # Redraw everything
            display_group = create_display()
            paddle_sprite = draw_paddle(display_group, paddle_x)
            ball_sprite = draw_ball(display_group, ball_x, ball_y)
            display.root_group = display_group
            print("Game reset!")
        elif not game_started:
            game_started = True
            ball_dx = BALL_SPEED
            ball_dy = -BALL_SPEED
            print("Game started!")
        time.sleep(1)
        continue
```

Während diese while-Schleife läuft, wollen wir außerdem die Steuerung des Paddles über die senseBox definieren, festlegen, was bei einer Kollision passiert, und bestimmen, wann der Spieler das Spiel gewonnen oder verloren hat.
Diese Abfragen sollen sehr häufig ausgeführt werden, damit sich das Spiel flüssig anfühlt. Deshalb wird die Schleife alle 0,03 Sekunden wiederholt. Das entspricht etwa 30 Wiederholungen pro Sekunde, auch bekannt als "FPS" (Frames per Second).

```python
    # Move paddle based on tilt
    if not game_over and not game_won:
        paddle_x += accel_y * PADDLE_SPEED
        paddle_x = max(0, min(128 - PADDLE_WIDTH, paddle_x))
        paddle_sprite.x = int(paddle_x)

    # Update ball if game is running
    if game_started and not game_over and not game_won:
        # Move ball
        ball_x += ball_dx
        ball_y += ball_dy

        # Ball collision with walls
        if ball_x <= 0 or ball_x >= 128 - BALL_SIZE:
            ball_dx = -ball_dx
            ball_x = max(0, min(128 - BALL_SIZE, ball_x))

        if ball_y <= 0:
            ball_dy = -ball_dy
            ball_y = 0

        # Ball collision with paddle
        if check_paddle_collision(ball_x, ball_y, paddle_x):
            ball_dy = -abs(ball_dy)
            # Add spin based on where ball hits paddle
            hit_pos = (ball_x + BALL_SIZE/2 - paddle_x) / PADDLE_WIDTH
            ball_dx = (hit_pos - 0.5) * 3

        # Ball collision with bricks
        if check_brick_collision(ball_x, ball_y):
            ball_dy = -ball_dy
            # Redraw display
            display_group = create_display()
            paddle_sprite = draw_paddle(display_group, paddle_x)
            ball_sprite = draw_ball(display_group, ball_x, ball_y)
            display.root_group = display_group

            # Check win
            if check_win():
                game_won = True
                print("YOU WIN!")

        # Check game over
        if ball_y > 64:
            game_over = True
            print("GAME OVER!")

        # Update ball position
        ball_sprite.x = int(ball_x)
        ball_sprite.y = int(ball_y)

    time.sleep(0.03)
```

## Spielanleitung

1. Spiel starten: Schüttle die senseBox kräftig um das Spiel zu starten
2. Paddle steuern: Neige die senseBox nach links oder rechts um das Paddle zu bewegen
3. Ziel: Zerstöre alle Blöcke mit dem Ball
4. Game Over: Der Ball darf nicht am Paddle vorbei nach unten fallen
5. Neustart: Nach Game Over oder Gewinn kannst du durch Schütteln neu starten

<p align="center">
  <img src="/images/projects/brick-breaker/brick-breaker_gif.gif" alt="Beschleunigungssensor Steuerung" width="400">
</p>
<p align="center"><em>Abbildung: Steuerung des Brick Breaker Spiels mit dem eingebauten Beschleunigungssensor</em></p>

## Erweiterungen

Du kannst das Spiel beliebig erweitern, falls du etwas hinzufügen möchtest. Du könntest zusätzliche Komponenten an deine MCU anschließen oder folgendes verändern:

- Schwierigkeitsgrade: Ändere BALL_SPEED für verschiedene Schwierigkeiten
- Mehr Blöcke: Erhöhe BRICK_ROWS für mehr Herausforderung
- Power-Ups: Füge spezielle Blöcke hinzu, die das Paddle vergrößern
- Punktezähler: Implementiere einen Score-Counter

## Sonstiges

Den gesamten Code zum Kopieren findest du [hier](https://docs.sensebox.de/docs/editors/circuitpython/circpy_example). Weitere Tutorials und Informationen zu CircuiPython findest du bei den [senseBox Docs](https://docs.sensebox.de/).
