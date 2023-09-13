---
layout: project_page
date: 2020-08-19
author: Verena
title: "Metronome"
abstract: "Let the senseBox set the pace for you!"
thumbnail: /images/projects/Titelbild_Metronom_en.jpg
image0: /images/projects/Metronom/Aufbau.png
image1: /images/projects/Metronom/Bild0_en.png
image2: /images/projects/Metronom/Bild1_en.png
image3: /images/projects/Metronom/Bild2_en.png

material:
  - senseBox MCU
  - 1x piezo
  - 1x JST adapter cable
  - if necessary, power bank

ide: blockly
version: ["edu"]
lang: en
tags: ["Music", "Mathematics"]
difficult: easy
---

# Metronome {#head}

The aim of this project is for the senseBox to support you in making music and to give you the beat, as you know it from a classical metronome.

## Structure

For the construction you only need the piezo, which has to be connected to the breadboard of the senseBox. To do this, use the JST adapter cable, which you connect to one of the digital ports. Now connect the shorter pin of the piezo (negative pole) to the black cable (ground GND) and the positive pole to the green or yellow cable (input/output). The number on the senseBox for the cable used should be kept in mind as a pin for subsequent programming.

{% include image.html image=page.image0 %}

## Programming

### Step 1: Output tones

Under the category 'Audio' you will find the block 'Play Sound'. You need this several times in the endless loop. As with a classical metronome, the first note in the bar should be louder or higher than the other notes. Therefore, you can use 528 Hz (c'') for the first note and 264 Hz (c') for the other notes in the bar. Depending on which bar you want to set, you need different numbers of 'play tone' blocks. Apart from the first note in the bar, you can loop the other notes and specify the number of repetitions. For example, if you want to produce a 4/4 bar, you need 3 repetitions, for a 3/4 bar only 2 repetitions, and so on.

{% include image.html image=page.image1 %}

### Step 2: Calculate distance between the tones

A metronome is known to maintain a set speed. This is usually given at the beginning of a piece in beats per minute (bpm). With this, you can calculate how long the interval between each new beat in the bar must be and integrate this into your programming with the help of the 'Wait' block from the 'Time' category. This block works with the unit milliseconds. You should therefore know that 1000 milliseconds are converted to one second. You should also note that 60 seconds correspond to one minute. For example, if 80 bpm is given, you calculate 60/80 = 0.75. You then multiply this by 1000 to get the correct unit (ms).

> The waiting time x is calculated with the following formula: (bpm/60)\*1000 = x

{% include image.html image=page.image2 %}

### Step 3: Separate tones from one another

Since the sounds do not merge into one another, but should be separated by a short pause the length of the previously calculated waiting time, the sound must be switched off again. You do this with the appropriate block from the category 'Audio'. However, if you were to insert the block directly after the 'Play Sound' block without a waiting period, no sound would be produced. So first the sound has to be played for a certain time interval, then it has to be stopped and then you have to wait until the new beat is played in the form of a sound. However, the time for this process should not exceed the previously calculated waiting time x, otherwise the metronome would be too slow. So you divide the time x by using, for example, one third of the time to play the sound and two thirds of the time to wait for the next beat.

{% include image.html image=page.image3 %}

## Entire Code

The entire Blockly sketch can be found [here](https://blockly.sensebox.de/gallery/63b6b0e4d2853f0013b1da25).

This solution now represents a metronome for a 4/4 beat with 80 beats per minute. However, you can vary the speed as you wish by recalculating the waiting time. You can set a different beat by changing the repetitions in the loop.


