---
layout: post
title: "Vogelerkennung mit der senseBox Eye"
date: 2026-04-20
author: Paula
abstract: "sesenBox Eye, Vogelerkennung, Citizen Science, Forschungsprojekt"
thumbnail: /images/blog/2026-04-20-Vogelerkennung/kohlmeise.gif
image-birdiary-combined: /images/blog/2026-04-20-Vogelerkennung/birdiary-combined.jpg
image-eye: /images/blog/2026-04-20-Vogelerkennung/eye.jpg
image-kohlmeise: /images/blog/2026-04-20-Vogelerkennung/kohlmeise.gif
image-blaumeise: /images/blog/2026-04-20-Vogelerkennung/blaumeise.gif
image-rotkehlchen: /images/blog/2026-04-20-Vogelerkennung/rotkehlchen.gif
image-amsel: /images/blog/2026-04-20-Vogelerkennung/amsel.gif
image-house-inside: /images/blog/2026-04-20-Vogelerkennung/house-with-inside.jpg
lang: de
---

# Birdiary

<div style="text-align: center;">
    {% include image.html image=page.image-birdiary-combined %}
    <div class="caption">Das Bild ist von Birdiary! Wir müssen fragen ob wir nutzen dürfen!</div>
</div>

2021 erfolgreiches Projekt am Ifgi: Birdiary

[https://wiediversistmeingarten.org/](https://wiediversistmeingarten.org/)

- Raspberry Pi
- seit 2021 an vielen Orten aufgestellt und viele Vögel aufgenommen
- Vogelbilder von Citizen Scientists validiert
- open source: es haben sich Abwandlungen entwickelt. zB [DuisBird](https://gitlab.com/iot-developer/DuisBird) hat Birdiary mit esp32-basiertem Mikrocontroller umgesetzt, statt Raspberry Pi


# TinyAIoT und Annis Masterarbeit

Forschungsprojekt TinyAIoT: KI auf Microcontrollern wie der senseBox

deshalb Vogelerkennung AUF DER SENSEBOX nicht in der Cloud

In dem Kontext: Annis Masterarbeit: Mit den validierten Vogelbildern aus Birdiary ein Modell zur Vogelklassifikation trainieren, das auf die senseBox Eye passt

# senseBox Eye

<div style="text-align: center;">
    {% include image.html image=page.image-eye %}
</div>

Im Rahmen von TinyAIoT KI-fähiges senseBox board entwickelt.

Erste Tests mit dem Modell aus Annis Masterarbeit.

<div class="bird-gallery">
  <div class="bird-item">
    {% include image.html image=page.image-kohlmeise %}
    <div class="caption">Kohlmeise</div>
  </div>
  <div class="bird-item">
    {% include image.html image=page.image-blaumeise %}
    <div class="caption">Blaumeise</div>
  </div>
  <div class="bird-item">
    {% include image.html image=page.image-rotkehlchen %}
    <div class="caption">Rotkehlchen</div>
  </div>
  <div class="bird-item">
    {% include image.html image=page.image-amsel %}
    <div class="caption">Amsel</div>
  </div>
</div>

Jede Klassifikation dauert circa eine 3/4tel Sekunde. Da wir in der sensebox Eye einen Prozessor mit zwei Kernen haben können wir auf einem Kern Videos aufnehmen und mit dem anderen Kern gleichzeitig einzelne Bilder daraus klassifizieren um zu prüfen, ob ein Vogel im Video zu sehen ist.

Auch mit der Waage aus Birdiary möglich...

<style>
.bird-gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 1em;
  justify-content: center;
  margin-bottom: 1.5em;
}
.bird-item {
  flex: 1 1 150px;
  max-width: 200px;
  text-align: center;
}
.bird-item img {
  width: 100%;
  height: auto;
  display: block;
}
.caption {
  font-size: 0.95em;
  color: #555;
  margin-top: 0.3em;
}
</style>

...


<div style="text-align: center;">
    {% include image.html image=page.image-house-inside %}
    <div class="caption">Ein altes Birdiary Vogelhaus mit senseBox Eye ausgestattet</div>
</div>

...

# Heilbronn?

Wir haben dort zwei Vogelhäuser mit der Hard- und Software von Birdiary aufgestellt (ohne senseBox Eye, ohne Tiny, einfach nur Birdiary...)

# Zukunft?

Umgang mit Fehlklassifikationen?
