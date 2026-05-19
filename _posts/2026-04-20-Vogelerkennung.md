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

/images/blog/2026-04-20-Vogelerkennung/birdiary-combined.jpg - Logo
Das Bild ist von Birdiary! Wir müssen fragen ob wir nutzen dürfen!

2021 erfolgreiches Projekt am Ifgi: Birdiary

https://wiediversistmeingarten.org/

[https://wiediversistmeingarten.org/](https://wiediversistmeingarten.org/)

- Raspberry Pi
- seit 2021 an vielen Orten aufgestellt und viele Vögel aufgenommen
- Vogelbilder von Citizen Scientists validiert
- open source: es haben sich Abwandlungen entwickelt. zB [DuisBird](https://gitlab.com/iot-developer/DuisBird) hat Birdiary mit esp32-basiertem Mikrocontroller umgesetzt, statt Raspberry Pi

### Birdiary - smarte Vogelerkennung im eigenen Garten

Vorschlag Gina:

Durch anthropogenes Handeln sind derzeit mehr Arten vom Aussterben bedroht als jemals zuvor. Um diese Entwicklung stärker ins gesellschaftliche Bewusstsein zu rücken, setzt das Projekt auf eine aktive Einbindung von Bürger*innen in die Forschung. Im Mittelpunkt steht eine selbst entwickelte, smarte Futterstation für Vögel, die mit verschiedenen Sensoren ausgestattet ist – darunter Kamera, Waage und Mikrofon sowie zusätzliche Umweltsensoren wie ein Thermometer.

Die Station ermöglicht eine automatisierte Erfassung von Vogelbesuchen: Tiere werden gezählt, ihre Aktivitäten dokumentiert und mithilfe der Kameradaten sogar bestimmten Arten zugeordnet. Damit wird der eigene Garten zum Forschungsstandort. Gerade in Deutschland ist dieses Konzept besonders wirkungsvoll, da es über 13 Millionen Privatgärten gibt, deren Gesamtfläche in etwa derjenigen aller Naturschutzgebiete entspricht. Dadurch entsteht ein enormes Potenzial für dezentrale Biodiversitätsforschung direkt vor der Haustür.

Im Rahmen des Projekts werden Bürgerinnen selbst zu Forscherinnen. Sie installieren die Open-Source-Station in ihrem Garten, beobachten die heimische Vogelwelt und tragen aktiv zur Datenerhebung bei. Die in Echtzeit gesammelten Daten können anschließend auf einer offenen Datenplattform eingesehen, ausgewertet, validiert und mit anderen Standorten verglichen werden. So entsteht ein kollaboratives Forschungsnetzwerk, das Wissenschaft und Gesellschaft enger miteinander verbindet.

Ein erfolgreiches Beispiel für diesen Ansatz ist das 2021 am Ifgi entwickelte Projekt „Birdiary“. Basierend auf einem Raspberry Pi wurde die Station an zahlreichen Orten eingesetzt und hat bereits eine große Menge an Vogelbildern gesammelt, die durch Citizen Scientists validiert wurden. Das Projekt ist vollständig Open Source, wodurch sich verschiedene Weiterentwicklungen etabliert haben. So wurde etwa „DuisBird“ entwickelt, eine Variante, die statt eines Raspberry Pi einen ESP32-basierten Mikrocontroller nutzt.

Weitere Informationen und Mitmachmöglichkeiten finden sich unter: [https://wiediversistmeingarten.org/](https://wiediversistmeingarten.org/)



# TinyAIoT und Annis Masterarbeit

Forschungsprojekt TinyAIoT: KI auf Microcontrollern wie der senseBox

deshalb Vogelerkennung AUF DER SENSEBOX nicht in der Cloud

In dem Kontext: Annis Masterarbeit: Mit den validierten Vogelbildern aus Birdiary ein Modell zur Vogelklassifikation trainieren, das auf die senseBox Eye passt

Vorschlag Gina:

### TinyAIoT: KI meets senseBox – von Smart Cities bis zur Vogelerkennung

Das Forschungsprojekt [TinyAIoT](https://sensebox.de/de/research-tinyaiot) beschäftigt sich mit der Frage, wie Künstliche Intelligenz direkt auf kleinen IoT-Geräten wie der senseBox eingesetzt werden kann. Ziel ist es, KI-Modelle so effizient und ressourcenschonend zu gestalten, dass sie nicht mehr in der Cloud laufen müssen, sondern unmittelbar auf Mikrocontrollern ausgeführt werden können. Dadurch werden Daten nicht dauerhaft übertragen, sondern direkt vor Ort verarbeitet, was Energie spart, den Datenverkehr reduziert und neue Anwendungen im Bereich Umwelt- und Smart-City-Monitoring ermöglicht.

Ein besonders anschauliches Beispiel dafür ist die Vogelerkennung auf der senseBox Eye. Im Rahmen des Projekts wurde ein KI-fähiges senseBox-Board entwickelt, das speziell für solche Anwendungen ausgelegt ist. Grundlage dafür ist unter anderem die Masterarbeit von Anni Henriikka Kurkela, in der mit validierten Vogelbildern aus dem Projekt Birdiary ein Modell zur Vogelklassifikation trainiert wurde, das direkt auf der Hardware der senseBox Eye lauffähig ist. Erste Tests zeigen bereits die erfolgreiche Erkennung typischer heimischer Vogelarten wie Kohlmeise, Blaumeise, Rotkehlchen und Amsel.

Die Klassifikation erfolgt dabei in etwa drei Viertel einer Sekunde pro Bild. Besonders leistungsfähig wird das System durch die Architektur der senseBox Eye selbst: Sie verfügt über einen Prozessor mit zwei Kernen, sodass parallel gearbeitet werden kann. Während ein Kern kontinuierlich Videodaten aufnimmt, analysiert der zweite gleichzeitig einzelne Frames, um zu prüfen, ob ein Vogel im Bild zu erkennen ist. So wird eine nahezu Echtzeit-Verarbeitung direkt auf dem Gerät möglich – ohne Umweg über die Cloud.

Ergänzend zu den Bilddaten lassen sich auch weitere Ansätze aus Birdiary integrieren, etwa durch die Kombination mit der ***Biodiversitäts-Waage*** (TODO: Was ist damit gemeint?). Insgesamt zeigt TinyAIoT damit sehr konkret, wie KI-basierte Umweltbeobachtung lokal auf Sensoren funktioniert: effizient, energiearm und unabhängig von Cloud-Infrastrukturen – und gleichzeitig leistungsfähig genug, um komplexe Aufgaben wie die automatische Vogelerkennung direkt vor Ort umzusetzen.

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

### Vogeldashboard für Heilbronn - ein Citizen-Science-Projekt zur urbanen Biodiversität

Wie können Umwelt- und Klimadaten gemeinsam erhoben, verstanden und für gesellschaftliche Fragestellungen der Stadt Heilbronn nutzbar gemacht werden? Und wie können Bildung, Zivilgesellschaft und Institutionen dabei zusammenwirken? Gemeinsam mit Arkadia Heilbronn möchten wir zusammen mit Bürger:innen und der senseBox diesen Fragen datenbasiert auf den Grund gehen. Ein Anwendungsfall soll auch hier die Vogelerkennung an verschiedenen Orten im Stadtgebiet werden, um Rückschlüsse auf die Biodiversität der Stadt Heilbronn zu ziehen. Dazu werden in Workshops im Juni 2026 Vogelhäuser mit den Teilnehmenden zusammengebaut sowie mit der Birdiary Sensorik (noch ohne senseBox Eye) ausgestattet. Auf einem Dashboard werden die erhobenen Daten zur Anzahl der Sichtungen sowie die häufigsten Arten visualisiert werden: https://greencity.hn/sammlung/biodiversitt

Aktuell wurden versuchsweise zwei Vogelhäuser mit der Hard- und Software aus dem Birdiary-Projekt  aufgestellt, um erste Testdaten für die Dashboard-Entwicklung zu erhalten. Hier zeigt sich jedoch, dass die KI-basierte Auswertung noch fehleranfällig ist und beispielsweise Vogelarten erkannt werden, die es gar nicht in Europa gibt. Das stellt uns vor die Herausforderung: wie gehen wir mit Fehleranfälligkeit, Fehlmessungen etc. um? 

# Next Steps

Muss noch ausformuliert werden:

Coming Soon senseBox Eye als Hardware (auch für andere Anwendungsfälle als Vogelerkennung, Zauberstab?)
Umgang mit Fehlklassifikationen?
Weiteres?
