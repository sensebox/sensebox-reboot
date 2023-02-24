---
layout: project_page
title: "IAQ Traffic Light"
date: 2022-12-19
author: Verena
abstract: "A traffic light to check indoor air quality."
thumbnail:  /images/projects/IAQ-ampel_en.png
image0: /images/projects/IAQ-ampel/0.png
image1: /images/projects/IAQ-ampel/1_en.png
image2: /images/projects/IAQ-ampel/2.png
image3: /images/projects/IAQ-ampel/3_en.png
image4: /images/projects/IAQ-ampel/4_en.png
material:
    - senseBox MCU mini
    - OLED display
    - Environmental sensor BME680
    - 2x JST-Qwicc cable
ide: blockly
version: ["mini v2"]   
lang: en
tags: ["Computer science", "Chemistry"]
difficult: medium
---
<head><title>Traffic light to check the indoor air quality</title></head>

In this project, the senseBox:mini is used to build a traffic light to check the indoor air quality (IAQ). With the help of the environmental sensor, the measured value is shown on the display in the first step. In the second step, the RGB LED integrated on the board is used to visually support and classify the measured values.

## Structure
The OLED display and the environmental sensor are each connected with a cable to one of the two I2C connections. 

{% include block.html image=page.image0 %}

## Programming

The programming of the measuring station is carried out in [Blockly](https://blockly.sensebox.de). In the first step, the measured values are read out and shown on the display. In the second step, the corresponding traffic light is programmed.

### Step 1: The indoor running quality indicator on the display 

Initialise the display in __Setup()__ and insert the block __Show on the display__ into the endless loop. With the block __Write Text/Number__ you can show the respective measured values on the display. For this purpose, insert the block __Create text from__ from the category 'Text' in 'Value'. With the help of a text field you can then add the label to the respective sensor value. The latter is displayed by inserting the __Environmental Sensor (BME680)__ as a block and selecting the corresponding environmental phenomenon, the indoor air quality. For the further course it makes sense to define a variable for this measured value. Create a variable of the type __int__ and name it 'IAQ'. You can then insert the block of the variable at all places where you would otherwise insert the block of the environmental sensor. To ensure that the measured value is permanently updated, insert the block __Display Clear__ at the end of your programme. 

#### Note: Calibration of the sensor
To provide reliable readings, the BME680 sensor calibrates itself based on the ambient air. The status is indicated by the calibration value. It is therefore useful to have this also shown on the display so that you can see whether the calibration is complete and the readings can be used. If the sensor is not calibrated or is in the process of calibrating, measured values are output but should not be used. The following values are available for the calibration value:

0: The sensor has just been started and is in the warm-up phase.
1: The measured values so far show too little difference and cannot be used for calibration.
2: The sensor is being calibrated
3: The calibration of the sensor is completed.
The calibration process may take a long time (>12h) and then shows the value 1. If the calibration does not start or is not completed after this time, it may be helpful to change the environmental parameters, e.g. by shocking ventilation in the room or holding the sensor in your hand for a certain time.

{% include block.html image=page.image1 %}


### Step 2: The traffic light 

At this point, you will see a number on the display. This is the index for the indoor air quality. The following table helps you to classify the measured value in the context of the application (source: Bosch 2022):

 {% include block.html image=page.image2 %}

To make this value directly interpretable for other people, we now want to add a traffic light to the display, so that a green light stands for good air quality and a red light for poor air quality. To do this, you need three __if-then conditions__ from the category 'Logic'. Here you add limit values in relation to the measured air quality (category 'Mathematics'), which can be exceeded or fallen short of, in accordance with the table. Depending on the value, the RGB LED then lights up green, yellow or red. You can choose these colours yourself by setting a value between 0 and 255 for the colours red, green and blue. Depending on the ratio of the assigned values, different colours are created. 

{% include block.html image=page.image3 %}


## Entire code

 {% include block.html image=page.image4 %}

Look at the programme code in Blockly: [IAQ traffic light](https://blockly.sensebox.de/gallery/63b59cf4d2853f0013b1d8b7)

 Now compile the program code and transfer it to the senseBox MCU mini. 


