---
layout: project_page
name: "First steps: Your first sketch"
date: 2020-02-12
author: Björn
abstract: "Let the LED on the senseBox MCU flash with your first sketch"
thumbnail: /images/projects/ErsterSketch_Titel.png
image1: /images/projects/FirstSketch/FirstSketch_Image00.PNG
image2: /images/projects/FirstSketch/FirstSketch_Image01.PNG
image3: /images/projects/FirstSketch/FirstSketch_Image02.PNG

material:
    - senseBox MCU
ide: blockly  
lang: en
version: ["edu", "mini"]   
tags: ["first steps", "computer science"]
difficult: easy
---

# First setps: Your first Sketch
The goal of this project is to get to know Blockly and to make the LED on the senseBox MCU flash with a first sketch.

## Programming

###Step 1: Setup und Loop

This block is loaded directly when you start the interface and should always be used. The two basic functions `Setup()` and `Loop()` are always needed to write a working program.
All blocks within the `Setup()` function are only executed once at the beginning of the program. In this function the display is initialized or the WLAN connection is established for example. All blocks within the `Endless Loop()` function are executed continuously. The microcontroller executes all blocks again and again from the top to the bottom. In the 'endless loop', for example, the sensors are read out or the measured values are stored or transferred to the SD card.


{% include image.html image=page.image1 %}

### Step 2: Switch on the built-in LED

To turn on the built-in LED, you have to pull the 'LED on digital' block into the endless loop. Then select "BUILTIN_1" in the PIN and "On" in the Status.
{% include image.html image=page.image2 %}

<div class="panel panel-info">
  <div class="panel-heading">
    The built-in LED can be found above the red reset button on the senseBox MCU
  </div>
  <div class="panel-body">
  </div>
</div>

### Step 3: Let the built-in LED flash

To make the built-in LED flash, it is necessary to switch it off again with another 'LED on digital' block. In addition, a pause must be inserted after switching on and off so that the flashing is visible at all. You can find the 'Waiting' block in the category 'Time'.
{% include image.html image=page.image3 %}

<div class="panel panel-info">
  <div class="panel-heading">
 1000 milliseconds are 1 second
  </div>
  <div class="panel-body">
  </div>
</div>
