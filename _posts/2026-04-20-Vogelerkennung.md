---
layout: post
title: "Vogelerkennung mit der senseBox:eye"
date: 2026-04-20
author: Paula
abstract: "Im Blogbeitrag stellen wir verschiedene Citizen-Science- und Forschungsprojekte zur Vogelerfassung vor und geben Einblicke in die neuesten Entwicklungen rund um die senseBox:eye als Board mit integrierter Kamera zur Beobachtung und Identifikation von Vögeln und anderen Tieren."
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

## Birdiary - smarte Vogelerkennung im eigenen Garten

<div style="text-align: center;">
    {% include image.html image=page.image-birdiary-combined %}
    <div class="caption">Bild links: © Simon Jöcker (2022) - Universität Münster</div>
</div>

/images/blog/2026-04-20-Vogelerkennung/birdiary-combined.jpg - Logo


Durch anthropogenes Handeln sind derzeit mehr Arten vom Aussterben bedroht als jemals zuvor. Um diese Entwicklung stärker ins gesellschaftliche Bewusstsein zu rücken, setzt das 2021 am Institut für Geoinformatik der Universität Münster entwickelte Projekt „[Birdiary](https://www.uni-muenster.de/studium/orga/foerderung_forschungsprojekte/multi-sensor-feeder.html)“ auf eine aktive Einbindung von Bürger in die Forschung. Im Mittelpunkt steht eine selbst entwickelte, smarte Futterstation für Vögel, die mit verschiedenen Sensoren, unter anderem Kamera, Waage und Mikrofon, sowie zusätzlichen Umweltsensoren ausgestattet ist. Die Station besteht aus einem Gehäuse mit zwei unterschiedlichen Kammern, wobei eine als Futtersilo dient und die andere die technische Ausstattung beherbergt. Ergänzt wird das Gehäuse durch ein abnehmbares Dach, das das Nachfüllen von Futter ermöglicht. Die integrierte Kamera zeichnet Videos der besuchenden Vögel auf, während die Waage erkennt, wenn ein Vogel die Station besucht, und dabei das entsprechende Gewicht misst. Zusätzlich nimmt ein Mikrofon Umgebungsgeräusche auf, sobald sich ein Vogel an der Station befindet. Ein weiterer Sensor für Lufttemperatur und Luftfeuchtigkeit erfasst zudem in regelmäßigen Abständen, auch unabhängig von Vogelbesuchen, verschiedene Umweltdaten.

Die Station ermöglicht eine automatisierte Erfassung von Vogelbesuchen: Tiere werden gezählt, ihre Aktivitäten dokumentiert und mithilfe der Kameradaten sogar bestimmten Arten zugeordnet. Damit wird der eigene Garten zum Forschungsstandort. Gerade in Deutschland ist dieses Konzept besonders wirkungsvoll, da es über 13 Millionen Privatgärten gibt, deren Gesamtfläche in etwa derjenigen aller Naturschutzgebiete entspricht. Dadurch entsteht ein enormes Potenzial für dezentrale Biodiversitätsforschung direkt vor der Haustür.

Im Rahmen des Projekts werden Bürger:innen selbst zu Forscherinnen. Sie installieren die Open-Source-Station in ihrem Garten, beobachten die heimische Vogelwelt und tragen aktiv zur Datenerhebung bei. Die in Echtzeit gesammelten Daten können anschließend auf einer offenen Datenplattform eingesehen, ausgewertet, validiert und mit anderen Standorten verglichen werden. So entsteht ein kollaboratives Forschungsnetzwerk, das Wissenschaft und Gesellschaft enger miteinander verbindet. Dafür hat das Projekt 2022 den [Citizen-Science-Preis](https://www.uni-muenster.de/news/view.php?cmdid=12481) der Stiftung der Universität Münster erhalten.

Die auf Open-Source-Hardware basierende Station wurde bereits an zahlreichen Standorten eingesetzt und hat eine große Menge an Vogelbildern gesammelt, die anschließend durch Citizen Scientists validiert wurden. Durch den offenen Aufbau des Projekts konnten zudem verschiedene Weiterentwicklungen entstehen. So wurde beispielsweise „[DuisBird](https://gitlab.com/iot-developer/DuisBird)“ entwickelt, eine Variante, die statt eines Raspberry Pi einen ESP32-basierten Mikrocontroller verwendet.

Weitere Informationen und Mitmachmöglichkeiten: [https://wiediversistmeingarten.org/](https://wiediversistmeingarten.org/)

## TinyAIoT und Annis Masterarbeit

Forschungsprojekt TinyAIoT: KI auf Microcontrollern wie der senseBox

deshalb Vogelerkennung AUF DER SENSEBOX nicht in der Cloud

In dem Kontext: Annis Masterarbeit: Mit den validierten Vogelbildern aus Birdiary ein Modell zur Vogelklassifikation trainieren, das auf die senseBox Eye passt

Vorschlag Gina:

## TinyAIoT: KI meets senseBox – von Smart Cities bis zur Vogelerkennung

Das Forschungsprojekt [TinyAIoT](https://sensebox.de/de/research-tinyaiot) beschäftigt sich mit der Frage, wie Künstliche Intelligenz direkt auf kleinen IoT-Geräten wie der senseBox eingesetzt werden kann. Ziel ist es, KI-Modelle so effizient und ressourcenschonend zu gestalten, dass sie nicht mehr in der Cloud laufen müssen, sondern unmittelbar auf Mikrocontrollern ausgeführt werden können. Dadurch werden Daten nicht dauerhaft übertragen, sondern direkt vor Ort verarbeitet, was Energie spart, den Datenverkehr reduziert und neue Anwendungen im Bereich Umwelt- und Smart-City-Monitoring ermöglicht.

Ein besonders anschauliches Beispiel dafür ist die Vogelerkennung auf der senseBox Eye. Im Rahmen des Projekts wurde ein KI-fähiges senseBox-Board entwickelt, das speziell für solche Anwendungen ausgelegt ist. Grundlage dafür ist unter anderem die Masterarbeit von Anni Henriikka Kurkela, in der mit validierten Vogelbildern aus dem Projekt Birdiary ein Modell zur Vogelklassifikation trainiert wurde, das direkt auf der Hardware der senseBox Eye lauffähig ist. Erste Tests zeigen bereits die erfolgreiche Erkennung typischer heimischer Vogelarten wie Kohlmeise, Blaumeise, Rotkehlchen und Amsel.

Die Klassifikation erfolgt dabei in etwa drei Viertel einer Sekunde pro Bild. Besonders leistungsfähig wird das System durch die Architektur der senseBox Eye selbst: Sie verfügt über einen Prozessor mit zwei Kernen, sodass parallel gearbeitet werden kann. Während ein Kern kontinuierlich Videodaten aufnimmt, analysiert der zweite gleichzeitig einzelne Frames, um zu prüfen, ob ein Vogel im Bild zu erkennen ist. So wird eine nahezu Echtzeit-Verarbeitung direkt auf dem Gerät möglich – ohne Umweg über die Cloud.

Ergänzend zu den Bilddaten lassen sich auch weitere Ansätze aus Birdiary integrieren, etwa durch die Kombination mit der ***Biodiversitäts-Waage*** (TODO: Was ist damit gemeint?). Insgesamt zeigt TinyAIoT damit sehr konkret, wie KI-basierte Umweltbeobachtung lokal auf Sensoren funktioniert: effizient, energiearm und unabhängig von Cloud-Infrastrukturen – und gleichzeitig leistungsfähig genug, um komplexe Aufgaben wie die automatische Vogelerkennung direkt vor Ort umzusetzen.

## Coming soon: senseBox:eye als neues Board mit integrierter Kamera

Im Rahmen von TinyAIoT wurde mit der senseBox:eye ein neues KI-fähiges senseBox-Board entwickelt, das speziell für Anwendungen im Bereich Computer Vision und Tiny Machine Learning ausgelegt ist. Durch die integrierte Kamera sowie die Möglichkeit, KI-Modelle direkt auf dem Mikrocontroller auszuführen, können Bilddaten lokal verarbeitet werden, ohne dass eine dauerhafte Verbindung zur Cloud notwendig ist. Das spart Strom und schützt die Privatsphäre.

<div style="text-align: center;">
    {% include image.html image=page.image-eye %}
</div>

Erste Tests mit dem im Rahmen einer Masterarbeit entwickelten Modell zur Vogelklassifikation zeigten bereits vielversprechende Ergebnisse. Dabei können typische heimische Vogelarten wie Kohlmeise, Blaumeise, Rotkehlchen und Amsel direkt auf der senseBox:eye erkannt werden.

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

Jede Klassifikation dauert circa eine 3/4tel Sekunde. Die sensebox:eye hat einen Prozessor mit zwei Kernen: Während ein Prozessorkern kontinuierlich Videodaten aufnimmt, analysiert der zweite gleichzeitig einzelne Frames und prüft, ob sich ein Vogel im Bild befindet. Dadurch wird eine nahezu Echtzeit-fähige Vogelerkennung direkt auf dem Gerät möglich.

Perspektivisch soll die Bilderkennung zudem mit weiteren Sensordaten kombiniert werden. Denkbar ist beispielsweise die Verbindung mit der im Birdiary-Projekt eingesetzten Waage, um Bilddaten mit Gewichtsveränderungen oder Aktivitätsmustern zu verknüpfen. Dadurch könnten Vogelbesuche robuster erkannt und zusätzliche Informationen über Verhalten oder Artenzugehörigkeit gewonnen werden.

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
    <div class="caption">Ein altes Birdiary Vogelhaus mit senseBox:eye ausgestattet</div>
</div>

Die ersten Prototypen zeigen bereits, wie bestehende Birdiary-Stationen mit der neuen Hardware erweitert werden können. Langfristig soll die senseBox:eye nicht nur für die Vogelerkennung eingesetzt werden, sondern auch für weitere Anwendungen im Bereich Umweltmonitoring, Smart City und KI-gestützter Sensorik.

Mehr dazu: LINK ZU UNTERSEITE

## Vogeldashboard für Heilbronn - ein Citizen-Science-Projekt zur urbanen Biodiversität

Wie können Umwelt- und Klimadaten gemeinsam erhoben, verstanden und für gesellschaftliche Fragestellungen der Stadt Heilbronn nutzbar gemacht werden? Und wie können Bildung, Zivilgesellschaft und Institutionen dabei zusammenwirken? Gemeinsam mit Arkadia Heilbronn möchten wir zusammen mit Bürger:innen und der senseBox diesen Fragen datenbasiert auf den Grund gehen. Ein Anwendungsfall soll auch hier die Vogelerkennung an verschiedenen Orten im Stadtgebiet werden, um Rückschlüsse auf die Biodiversität der Stadt Heilbronn zu ziehen. Dazu werden in Workshops im Juni 2026 Vogelhäuser mit den Teilnehmenden zusammengebaut sowie mit der Birdiary Sensorik (noch ohne senseBox:eye) ausgestattet. Auf einem Dashboard werden die erhobenen Daten zur Anzahl der Sichtungen sowie die häufigsten Arten visualisiert werden: [https://greencity.hn/sammlung/biodiversitt](https://greencity.hn/sammlung/biodiversitt)

Es wurden bereits versuchsweise zwei Vogelhäuser mit der Hard- und Software aus dem Birdiary-Projekt aufgestellt, um erste Testdaten für die Dashboard-Entwicklung zu erhalten. Hier zeigt sich jedoch, dass die KI-basierte Auswertung noch fehleranfällig ist und beispielsweise Vogelarten erkannt werden, die es gar nicht in Europa gibt. Das stellt uns vor die Herausforderung: wie gehen wir mit Fehleranfälligkeit, Fehlmessungen etc. um? 

## Next Steps

Die bisherigen Ergebnisse zeigen bereits, welches Potenzial in der Kombination aus Citizen Science, Open-Source-Hardware und KI-gestützter Umweltbeobachtung steckt. Gleichzeitig stehen noch einige spannende Entwicklungsschritte bevor.

Ein zentraler nächster Schritt ist die Veröffentlichung der senseBox:eye als eigenständiges Board mit integrierter Kamera. Damit soll die Hardware künftig nicht nur für die Vogelerkennung, sondern auch für weitere TinyML- und Computer-Vision-Anwendungen nutzbar werden. Denkbar sind beispielsweise Projekte aus den Bereichen Umweltmonitoring, Smart City oder kreative Maker-Anwendungen (sogar zaubern wird möglich!). Darüber hinaus eröffnet die senseBox:eye auch Anwendungen jenseits der Vogelerkennung. Im Rahmen eines Studienprojekts am Institut für Geoinformatik der Universität Münster setzten Studierende die Hardware beispielsweise zur Zählung der Ein- und Ausflüge von Hummeln an einem Brutkasten ein. Durch die senseBox:eye konnte die Beobachtung minimalinvasiv erfolgen, ohne die Tiere in ihrem natürlichen Verhalten zu stören. Perspektivisch könnten so auch weitere Tierarten automatisiert beobachtet und ökologische Fragestellungen datenbasiert untersucht werden.

Auch die Weiterentwicklung der KI-Modelle bleibt ein wichtiger Entwicklungsbereich. Erste Tests zeigen bereits vielversprechende Ergebnisse bei der Erkennung heimischer Vogelarten, gleichzeitig wird aber deutlich, dass KI-gestützte Klassifikation weiterhin fehleranfällig sein kann. Künftig soll daher untersucht werden, wie sich Fehlklassifikationen reduzieren und Unsicherheiten transparenter darstellen lassen, z.B. durch bessere Trainingsdaten, zusätzliche Sensorinformationen oder Mechanismen zur Validierung durch Citizen Scientists.

Darüber hinaus eröffnet die Kombination verschiedener Sensordaten neue Möglichkeiten für die Biodiversitätsforschung. Neben Bilddaten könnten künftig beispielsweise Gewichtsverläufe, Geräuschaufnahmen oder Umweltdaten stärker in die Auswertung einbezogen werden, um Vogelbesuche robuster und genauer zu analysieren.

Langfristig entsteht so eine offene Plattform für lokale KI-Anwendungen auf ressourcensparender Hardware. Projekte wie Birdiary, TinyAIoT und das Vogeldashboard Heilbronn zeigen bereits heute, wie Umweltbeobachtung, Forschung und Bildung durch offene Technologien miteinander verbunden werden können.
