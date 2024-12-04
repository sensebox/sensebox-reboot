---
layout: post
title: "Bluetooth Bee"
date: 2022-01-25
author: Mario
abstract: "Das neue Bluetooth Bee für die senseBox ist da!"
thumbnail: /images/blog/2022-01-25-Bluetooth-Bee/DSCF9880.jpg
image1: /images/blog/2022-01-25-Bluetooth-Bee/DSCF9809.jpg
image2: /images/blog/2022-01-25-Bluetooth-Bee/blockly.png
blocks: /images/blog/2022-01-25-Bluetooth-Bee/phyphox-blocks.jpg
lang: de
tag: News
---

# Das neue Bluetooth Bee für die senseBox ist da

Mit Unterstützung der Deutschen Telekom Stiftung konnten wir ein Bluetooth Bee für die senseBox entwickeln, das ein Übertragen von Messwerten über Bluetooth an dein Smartphone oder Tablet ermöglicht und die senseBox zu einem mobilen Umweltlabor macht. Zur Visualisierung und Analyse der Daten wird die [Phyphox App](https://phyphox.org/) der RWTH Aachen verwendet. Dank der tollen [Arduino Bibliothek](https://phyphox.org/arduino/), die von Phyphox bereitgestellt wird, können so eigene Messgeräte auf Arduino und eben auch auf senseBox Basis gebaut werden. Durch die Integration des neuen Bluetooth Bees in das senseBox System kannst du alle Sensoren, die du direkt an die senseBox anschließen kannst, verwenden und die Programmierung läuft wie gewohnt über die grafische Programmierumgebung [Blockly](https://blockly.sensebox.de/).

{% include image.html image=page.image1 %}

## Technisches

Das Bluetooth Bee verwendet den [uBlox B312](https://www.u-blox.com/en/product/nina-b31-series-u-connect?lang=de), dessen Basis ein nRF52840 von Nordic Semiconductors ist. Das Bluetooth Bee ist kompatibel zu Bluetooth 5.0 und unterstützt Bluetooth Low Energy. Das Bee kann direkt auf die senseBox MCU gesteckt werden und benötigt keine weitere Verkabelung.

## Programmierung

Die Programmierung des Messgerätes kann in unserer grafischen [Programmier- und Lernumgebung](https://blockly.sensebox.de/) durchgeführt werden. Neue Blöcke ermöglichen dir dein Experiment genau für deinen Anwendungsfall zu erstellen. Alle Sensoren, die du an die senseBox anschließen kannst, kannst du verwenden und die Messwerte einfach übertragen.

{% include image.html image=page.blocks %}

Ein Beispielcode kannst du direkt [hier](https://blockly.sensebox.de/gallery) öffnen. Zusätzlich zum Beispielcode gibt es auch ein Tutorial, welches dir die einzelnen Blöcke der Programmierung erläutert. Zum Tutorial kommst du [hier](https://blockly.sensebox.de/tutorial).

## Materialien

Durch die Anbindung der senseBox an Phyphox ergeben sich viele spannende Möglichkeiten für den Einsatz im naturwissenschaftlichen Unterricht. Für den leichten Einstieg haben wir verschiedene Unterrichtsmaterialien und das folgende Video vorbereitet.

{% include youtube.html id = "rs1DoW6p2Hs" %}

---

Neben der Einführung im Video findest du drei weitere Projekte auf unserer Website oder zum Download

<div class="row">
     <div class="col-lg-3 col-sm-12">
            <div class="card" style="cursor: pointer; border: none">
                <canvas class="header-bg" width="250" id="header-blur"
                    style="background-image: url({{ site.baseurl | append: '/images/material/ble_handreichung.jpg' }});"></canvas>
                <div class="content">
                    <h4 style="clear:both">Digitales Mobiles Umweltlabor für die MINT-Fächer</h4>
                    <div id="desc_{{ teaching.position }}">
                        <a class="stretched-link" href="/docs/senseBox_BluetoothBee_ver1.0.pdf"></a>
                    </div>
                </div>
            </div>
        </div>
        <div class="col-lg-3 col-sm-12">
            <div class="card" style="cursor: pointer; border: none">
                <canvas class="header-bg" width="250" id="header-blur"
                    style="background-image: url({{ site.baseurl | append: '/images/projects/Titelbild_Wurfbewegungen.png' }});"></canvas>
                <div class="content">
                    <h4 style="clear:both">Analyse von Wurfbewegungen</h4>
                    <div id="desc_{{ teaching.position }}">
                        <a class="stretched-link" href="/projects/de/2021-12-28-Wurfbewegung-Phyphox.html"></a>
                    </div>
                </div>
            </div>
        </div>
        <div class="col-lg-3 col-sm-12">
            <div class="card" style="cursor: pointer; border: none">
                <canvas class="header-bg" width="250" id="header-blur"
                    style="background-image: url({{ site.baseurl | append: '/images/projects/Titelbild_Lueftungsstrategien.png' }});"></canvas>
                <div class="content">
                    <h4 style="clear:both">Optimierung von Lüftungsstrategien</h4>
                    <div id="desc_{{ teaching.position }}">
                        <a class="stretched-link" href="/projects/de/2021-12-28-Lüftungsstrategien-Phyphox.html"></a>
                    </div>
                </div>
            </div>
        </div>
              <div class="col-lg-3 col-sm-12">
            <div class="card" style="cursor: pointer; border: none">
                <canvas class="header-bg" width="250" id="header-blur"
                    style="background-image: url({{ site.baseurl | append: '/images/projects/Titelbild_Phyphox.png' }});"></canvas>
                <div class="content">
                    <h4 style="clear:both">Verbindung der senseBox mit Phyphox</h4>
                    <div id="desc_{{ teaching.position }}">
                        <a class="stretched-link" href="/projects/de/2021-12-21-Verbindung%20mit%20der%20Phyphox%20App.html"></a>
                    </div>
                </div>
            </div>
        </div>
</div>

---

## Shop

Das Bluetooth Bee wurde mit Unterstüzung der Deutschen Telekom Stiftung entwickelt und ist ab sofort bei uns im Shop erhältlich [https://sensebox.kaufen/product/bluetooth-bee](https://sensebox.kaufen/product/bluetooth-bee)
