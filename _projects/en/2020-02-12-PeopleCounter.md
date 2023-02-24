---
layout: project_page
name: "People Counter"
date: 2020-02-19
author: Lia
abstract: "With the ultrasonic distance sensor and the display a people counter can be built"
thumbnail: /images/projects/traffic_counter_en.png
image1: /images/projects/personenzaehler/01_personenzaehler_schaltung.jpg
image2: /images/projects/personenzaehler/en/02_sensor_displayEn.PNG
image3: /images/projects/personenzaehler/en/03_wenn_bedingungEn.PNG
image4: /images/projects/personenzaehler/en/04_wenn_bedingung_2En.PNG
material:
    - senseBox MCU
    - Ultrasonic sensor
    - OLED display
    - 1x JST adapter cable
    - 1x JST cable
ide: blockly 
version: ["edu"]   
lang: en
tags: ["geography", "computer science"]
difficult: easy
---
# People counter

The aim is to develop a people counter. The ultrasonic distance sensor is used for this purpose. The values recorded in this way are to be output on the <b>Display</b>.

## Basics
The ultrasonic distance sensor uses sound to determine the distance of objects. The sensor sends out a pulse and measures the time until it receives the echo of the pulse again. From this time the distance of the object can then be calculated using the speed of sound.

## Structure

The ultrasonic distance sensor is connected to the senseBox MCU via the JST adapter cable. Connect the JST adapter cable to the digital/analog port A. The black cable is connected to pin GND, the red cable to pin VCC, the green cable to pin Trig and the yellow cable to pin Echo of the sensor. The display is connected to one of the I2C/Wire ports via the JST-JST cable. 

{% include image.html image=page.image1 %}

***Note:*** *The sensor should point in the direction where no cables are in the way as this will not obstruct the sound.*

## Programming

### Step 1

In the first step the measured value of the ultrasonic distance sensor is read out, assigned to a variable and shown on the display.

{% include image.html image=page.image2 %}

To show the value of the sensor on the display, the display must first be initialized in Setup(). Then the display can be used in the 'endless loop'.
Drag the block 'Show on display' into the endless loop. To display text or numbers, drag the block 'Show Text/Number' into the open block section. In this block you can set in which font size and where on the display texts or numbers should be shown. After the block 'Show on display' the display must be cleared with the block 'Clear display'. Under Variables you will find the block to create a variable.

Transfer the program code to the senseBox MCU and check what happens with the distance when a person passes the sensor. 

***Note*** *Effectively the ultrasonic distance sensor measures reliably in a range between 5cm and 200cm.*

### Step 2

The distance is important to detect whether a person is passing the sensor. An if-then condition is used for this: If a person walks past the sensor, the distance decreases. 
In an if-then condition, for example, operators can be used to compare two values. If the condition is met, the code that is placed in the open block section is executed. In this case the variable *persons* is always increased by one.   

{% include image.html image=page.image3 %}

Transfer the program code to your senseBox MCU and check if the program works. 

### Step 3: Double counts?

If you have transferred and tested the program, you will have noticed that the counter counts people multiple times if they stop in front of the sensor. To solve this problem you can add a second condition to check if the maximum distance has been reached again after the distance has been interrupted. The counter will be locked if the distance is interrupted and will only be unlocked when the distance has reached the maximum value. With the logical AND you can link two conditions and the code in the block section "make" will only be executed if both conditions are met. 

{% include image.html image=page.image4 %}

The variable *locked* is set to "false" at the beginning of the program. Whenever the distance is less than 40cm and at the same time *locked* "false", the counter is increased and the variable *locked* is set to "true". This interrupts the counter for the time being. Counting is only started again when the lock is removed. 

## Entire Code

You can find the finished Blockly Code [here](https://blockly.sensebox.de/gallery/63bc4556d2853f0013b1e01a).
