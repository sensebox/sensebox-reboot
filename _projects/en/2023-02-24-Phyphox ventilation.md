---
layout: project_page
title: "Optimising ventilation strategies"
date: 2021-12-28
author: Verena
abstract: "Measure the CO2 concentration in your room using the Phyphox app."
thumbnail:  /images/projects/Titelbild_Lueftungsstrategien_en.png
image0: /images/projects/Lüftungsstrategien/0.png
image1: /images/projects/Lüftungsstrategien/1_en.png
image2: /images/projects/Lüftungsstrategien/2_en.png
image3: /images/projects/Lüftungsstrategien/3_en.png

material:
    - senseBox MCU
    - 1x CO2-Sensor
    - 1x Bluetooth-Bee
    - 1x JST-JST-Kabel 
    - if necessary, Powerbank
    
ide: blockly
version: ["edu"]   
addons: ["Bluetooth-Bee"]  
lang: en
tags: ["Computer Science", "Physics", "Phyphox"]
difficult: easy
---
<head><title>Optimisation of ventilation strategies with the help of Phyphox</title></head>

# Measure the CO2 concentration in your room
In this project you find out how high the CO2 concentration is in your room. For the measurement, you use the senseBox, which sends the data to Phyphox via Bluetooth. In the app you can follow your data collection and use the graph visible there as a starting point for interpreting the CO2 concentration and consequently the ventilation strategies.  

## Set-up
First connect the CO2 sensor with the JST-JST cable. Connect it to one of the five I2C/Wire connections of your senseBox MCU. The Bluetooth-Bee is plugged into the XBee1 slot of the microcontroller.

{% include image.html image=page.image0 %}

## Programming

The aim of the programming is to establish a connection to the Phyphox app. This is to display the measured values of the CO2 concentration and the temperature in a suitable graph.

### Step 1: Set up Phyphox device
Programming your meter is done with Blockly for senseBox. First initialise a Phyphox device in Setup() and name it individually. If several measuring devices are used in one room, you can find your measuring device by its name. With the block 'Create Experiment' you can configure the display of your measured values. Since the CO2 sensor can measure both the CO2 concentration and the temperature, two graphs are recommended. With the first channel you can transmit the CO2 concentration and display the time in seconds on the x-axis and the measured values in parts per million (ppm) on the y-axis. Using the second channel, you can transmit the collected data on temperature and map it on the y-axis in degrees Celsius, while on the x-axis the time in seconds again serves as a guide. 

{% include image.html image=page.image1 %}

### Step 2: Sending the measured values
In the endless loop, you connect the CO2 sensor and select the temperature and the CO2 concentration as measured values. Use the 'Measuring interval' block to set how often the measured values are to be sent from the senseBox to the Phyphox app.

{% include image.html image=page.image2 %}

## Entire Code

The programme code is now ready! You can now compile the sketch and transfer it to the senseBox MCU.
[Here](https://blockly.sensebox.de/gallery/63b5a057d2853f0013b1d900) you can call up the finished programme code in Blockly. 

## Connecting with the Phyphox app
Open the Phyphox app, click on the + and select 'New experiment for Bluetooth device'. A list of available measuring devices will now be displayed. Click on your measuring device to connect. To set the measurement period for the experiment, click on the three dots and open the item 'Timer'. Since the experiment is to run for 10 minutes, enter 600 seconds for the duration.

{% include image.html image=page.image3 %}

Start the experiment by clicking on the 'Start' button. The measured values of the senseBox are now recorded by the app. 
Now proceed step by step and open or close the window completely or partially after a few minutes. After the experiment is finished, you can select 'Save state' via the three dots and name it. The saved graph now gives you the opportunity to analyse your ventilation behaviour based on the CO2 concentration and to derive suitable strategies. 

