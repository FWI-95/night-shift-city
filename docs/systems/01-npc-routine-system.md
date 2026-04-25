# NPC Routine System

## Ziel

Das NPC Routine System ist der emotionale Kern von Night Shift City. Es soll dafür sorgen, dass wiederkehrende NPCs nicht wie statische Dekoration wirken, sondern wie Bewohner mit eigenen Gewohnheiten, Tagesabläufen, Bedürfnissen und kleinen Abweichungen.

Der Spieler soll nicht das Gefühl haben, dass NPCs nur für ihn existieren. Stattdessen soll er Menschen wiedererkennen, Muster beobachten und langsam ein Gefühl für ihre Leben entwickeln.

## Design-Kernsatz

> Routine ist Erwartbarkeit mit Störungen.

NPCs sollen wiedererkennbare Muster haben, aber nicht jeden Tag exakt identisch funktionieren.

Ein NPC darf regelmäßig freitags in eine Bar gehen. Er soll aber nicht jeden Freitag exakt um 22:00 Uhr am selben Tisch stehen und exakt um 23:30 Uhr verschwinden.

## Spielerlebnis

Der Spieler soll Dinge denken wie:

- „Den Typen sehe ich immer nach der Spätschicht am Nudelstand.“
- „Die Frau verpasst ständig die Metro.“
- „Der Barbesucher bleibt freitags oft zu lange.“
- „Wenn es regnet, sind hier weniger Leute unterwegs.“
- „In diesem Stadtteil kaufen viele Arbeiter nach Feierabend Essen.“

Das System soll keine perfekte Realität simulieren, sondern glaubwürdige Stadtgewohnheiten erzeugen.

## NPC-Typen

### Named NPCs

Named NPCs sind kuratierte, wiederkehrende Bewohner.

Sie besitzen mindestens:

- eine eindeutige ID
- einen Namen oder Anzeigenamen
- Wohnort
- optionale Arbeit / Rolle
- Traits
- wochentagsabhängige Routinen
- Activity Pools
- aktuelle Simulationszustände

Named NPCs sollen wiedererkennbar sein und langfristig optional Gesprächsfetzen, Familiarity oder kleine persönliche Geschichten erhalten.

### Ambient NPCs

Ambient NPCs füllen die Stadt.

Sie sind leichter simuliert und müssen nicht dauerhaft vollständig existieren. Sie folgen vereinfachten Bewegungs- und Aktivitätsmustern, damit die Stadt bevölkert wirkt.

Ambient NPCs können später optional zu Named NPCs promoted werden, wenn sie dem Spieler wiederholt auffallen.

## Datenmodell – Konzept

Beispielhafte NPC-Definition:

```yaml
id: riko_malden
displayName: Riko Malden
home: district_lower_market.block_c.apartment_412
job: harbor_loader

traits:
  - social
  - impulsive
  - tired
  - likes_noodles
  - drinks_too_much

needs:
  hunger: 35
  energy: 60
  stress: 55
  money: 42

weeklySchedule:
  monday-friday:
    - window: "07:00-08:30"
      activity: breakfast
      target: nearest:cheap_food
      duration: "10m-30m"
      probability: 0.85

    - window: "10:30-11:00"
      activity: travel_to_work
      target: job.location
      duration: auto

    - window: "11:00-19:00"
      activity: work
      target: job.location
      visibility: hidden

    - window: "19:00-21:00"
      activityPool: after_work

  friday:
    - window: "21:30-23:00"
      activityPool: friday_night

activityPools:
  after_work:
    - weight: 55
      activity: go_home
    - weight: 30
      activity: eat
      target: nearest:cheap_food
      condition: hunger > 45
    - weight: 15
      activity: drink
      target: bar_01
      condition: stress > 60

  friday_night:
    - weight: 75
      activity: drink
      target: bar_01
      duration: "1h-4h"
      modifiers:
        - condition: stress > 70
          durationBonus: "1h"
        - condition: money < 15
          weightBonus: -40
        - condition: friend_present
          durationBonus: "30m-2h"
```

## Zeitfenster statt fixer Uhrzeiten

Ein Kernprinzip ist, dass Aktivitäten mit Zeitfenstern arbeiten.

Statt:

```text
22:00 Bar
23:30 Zuhause
```

Besser:

```yaml
window: "21:30-23:00"
duration: "1h-4h"
probability: 0.75
```

Dadurch entstehen Abweichungen, ohne dass der NPC beliebig wirkt.

## Activity Pools

Activity Pools sind wiederverwendbare Entscheidungsgruppen.

Beispiel:

```yaml
after_work:
  - weight: 50
    activity: go_home
  - weight: 30
    activity: eat
    target: nearest:cheap_food
  - weight: 20
    activity: socialize
    target: nearest:bar
```

Sie ermöglichen, dass viele NPCs ähnliche Bausteine verwenden, aber durch Traits und Zustände anders gewichten.

## Traits

Traits beeinflussen Entscheidungen, Dialog, Verhalten und Routinen.

Beispiele:

- `social`
- `introvert`
- `cheap_food`
- `hates_rain`
- `workaholic`
- `drinks_too_much`
- `night_owl`
- `early_bird`
- `impulsive`
- `reliable`
- `broke`

Traits sollen nicht zu komplex werden. Sie sind zunächst einfache Tags, die Gewichtungen und Bedingungen beeinflussen.

## Needs / Zustände

NPCs können einfache Zustände besitzen:

- Hunger
- Energie
- Stress
- Geld
- Stimmung
- soziale Energie

Für MVP 0 reicht eine stark vereinfachte Variante. Zustände müssen nicht perfekt simuliert werden. Sie dienen zunächst dazu, Aktivitätsauswahl plausibler zu machen.

## Sichtbarkeit und Simulationstiefe

Um solo-dev-tauglich zu bleiben, wird nicht jeder NPC dauerhaft voll simuliert.

```text
Dormant  = weit weg, nur abstrakter Zeitstatus
Abstract = im Stadtteil, aber nicht sichtbar
Active   = nahe beim Spieler, echte Bewegung und Interaktion möglich
```

### Dormant

Der NPC wird nicht physisch bewegt. Das System kann aus Uhrzeit, Schedule und Zustand ableiten, wo er ungefähr sein müsste.

### Abstract

Der NPC existiert im aktuellen Stadtteil, aber nicht direkt sichtbar. Aktivitäten können abstrakt verarbeitet werden.

### Active

Der NPC ist im Sicht-/Interaktionsbereich des Spielers. Bewegung, Animation, Dialog und sichtbare Interaktion können stattfinden.

## Offscreen-Logik

Wenn ein NPC nicht sichtbar ist, soll nicht jeder Schritt simuliert werden.

Beispiel:

```text
07:30 home
08:00 traveling_to_food
08:20 eating
10:45 traveling_to_work
11:00 working
19:15 traveling_home
```

Beim Betreten eines Bereichs kann die Engine den aktuellen plausiblen Zustand rekonstruieren.

## Abweichungen

Abweichungen erzeugen Leben.

Mögliche Ursachen:

- Wetter
- Stress
- Hunger
- Geldmangel
- Überstunden
- zufällige Verspätung
- Freund getroffen
- zu lange geblieben
- Event im Stadtteil
- Werbung des Spielers
- geänderte Öffnungszeiten eines Geschäfts

Abweichungen sollen nachvollziehbar bleiben. Sie sind keine beliebige Zufallsmaschine.

## Spielerinteraktion

Der Spieler soll NPCs primär beobachten und leicht mit ihnen interagieren können.

Mögliche spätere Interaktionen:

- kurzen Smalltalk führen
- Stammkunden wiedererkennen
- Gesprächsfetzen hören
- auf Beschwerden reagieren
- Angebot oder Öffnungszeiten an Gewohnheiten anpassen

Der Spieler soll nicht das Leben jedes NPCs kontrollieren. Er beeinflusst eher den Kontext, in dem NPCs handeln.

## MVP 0 Scope

Für MVP 0 wird benötigt:

- einfache NPC-Datenstruktur
- einfache Location-Datenstruktur
- GameClock
- Schedule-Auswertung
- Zeitfenster
- Activity-Auswahl
- Debug-Log
- mindestens 3 Beispiel-NPCs

Nicht benötigt:

- Rendering
- Pathfinding
- Dialoge
- Beziehungen
- komplexe Bedürfnisse
- Business-Integration

## Akzeptanzkriterien für MVP 0

- Drei NPCs werden aus Daten geladen.
- Jeder NPC besitzt einen Wochentagsablauf.
- Aktivitäten starten innerhalb von Zeitfenstern.
- Mindestens eine Aktivität variiert zwischen Simulationsläufen.
- Die Debug-Ausgabe ist lesbar und zeigt Zustandswechsel.

## Offene Fragen

- JSON oder YAML als erstes Content-Format?
- Wie deterministisch soll die Simulation sein?
- Brauchen wir Seeds pro Tag, damit Routinen reproduzierbar bleiben?
- Wie stark sollen Needs bereits in MVP 0 einfließen?
- Wann wird ein Ambient NPC zu einem Named NPC promoted?
