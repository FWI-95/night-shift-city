# Engine vs Game Layer Strategy

## Ausgangspunkt

Night Shift City ist aktuell das konkrete Spielprojekt: ein cozy Cyberpunk-Erkundungsspiel mit NPC-Routinen, kleinen Businesses, Stadtteilen, Metro, Atmosphäre und datengetriebener Simulation.

Gleichzeitig steckt im Konzept eine zweite Ebene: Viele Systeme sind nicht ausschließlich Cyberpunk-spezifisch. NPC-Routinen, Tagesabläufe, kleine Businesses, Orte, Nachfrage, Exploration und Gesprächsfetzen könnten auch andere Settings tragen.

Beispiele:

- Cyberpunk-Bar in Night Shift City
- Dieselpunk-Stadt mit Werkstätten und Hafenkneipen
- geerbte Tankstelle mit Zapfsäulen, Stammkunden und Ausbau
- kleines Café in einer Universitätsstadt
- Dorfkneipe mit lokalen Routinen
- Spaceport-Kiosk mit Reisenden und Schichtarbeitern

## Design-Kernsatz

> Night Shift City ist das erste Spiel. Die darunterliegende Engine soll aber nicht in Cyberpunk gefangen sein.

## Zwei-Schichten-Modell

```text
Game Layer: Night Shift City
 ├─ Setting: cozy Cyberpunk
 ├─ konkrete Stadtteile
 ├─ konkrete NPCs
 ├─ konkrete Businesses
 ├─ Ton, Atmosphäre, Lore
 └─ konkrete Assets

Simulation / Engine Layer
 ├─ Zeitmodell
 ├─ Orte / Locations
 ├─ NPC-Routinen
 ├─ Activity Pools
 ├─ Bedürfnisse / Zustände
 ├─ Business-Logik
 ├─ Nachfrage / Awareness
 ├─ Micro Actions
 ├─ Dialogue Snippets
 └─ datengetriebener Content Loader
```

## Was generisch bleiben sollte

Diese Systeme sollten möglichst setting-agnostisch entworfen werden:

### Time / Calendar

- Tageszeit
- Wochentage
- Zeitfenster
- Öffnungszeiten
- Ereignisfenster

### Actor / NPC Routines

- Wohnort
- Arbeitsplatz / Rolle
- Traits
- Needs
- Schedule
- Activity Pools
- Abweichungen

### Locations

- Orte mit Tags
- Kapazität
- Öffnungszeiten
- Funktionen
- Nachfrageprofil
- soziale Rolle

### Businesses

- Besitz / Betreiber
- Standort
- Angebot
- Bekanntheit
- Kundentypen
- Einnahmen / Kosten
- lokale Nachfrage
- Verbesserungen

### Micro Actions

- Werbung machen
- Angebot anpassen
- Öffnungszeiten ändern
- Standort scouten
- Ausstattung verbessern
- mit Stammkunden interagieren

### Discovery / Knowledge

- Spieler erkennt Muster
- Orte werden verstanden
- Nachfrage wird sichtbar
- NPC-Routinen werden vertrauter

## Was game-spezifisch bleiben darf

Diese Dinge dürfen bewusst im Night-Shift-City-Layer liegen:

- Cyberpunk-Ästhetik
- Neon, Regen, Metro, Nachtleben
- konkrete NPC-Namen
- konkrete Stadtteile
- Lore
- Dialogton
- spezifische Business-Typen wie Nudelstand, Bar, Lieferdienst
- UI-Stil
- konkrete Assets
- Soundscape

## Beispiel: Gleiches System, anderes Spiel

### Night Shift City

```yaml
businessType: bar
settingTags: [cyberpunk, nightlife, lower_district]
customers: [night_worker, drifter, courier]
actions:
  - advertise_in_district
  - adjust_opening_hours
  - change_drink_menu
```

### Tankstellen-Sim

```yaml
businessType: gas_station
settingTags: [rural, roadside, late_shift]
customers: [commuter, truck_driver, local_regular]
actions:
  - advertise_on_road
  - adjust_fuel_prices
  - expand_pump_capacity
```

Beide könnten dieselben Engine-Konzepte nutzen:

- Location
- Business
- Customer Archetypes
- Awareness
- Demand
- Opening Hours
- Micro Actions

## Architektur-Prinzip

Die Engine soll Begriffe wie `Business`, `Location`, `Actor`, `Routine`, `Activity`, `Demand`, `Awareness` und `Interaction` kennen.

Sie soll möglichst nicht fest Begriffe wie `CyberpunkBar`, `MetroStationLowerNeon`, `NoodleVendor` oder `NightCityWorker` kennen.

Solche Begriffe gehören in Content-Dateien oder Game-spezifische Module.

## Content Packs

Langfristig könnte jedes Spiel oder Setting als Content Pack verstanden werden.

```text
content-packs/
  night-shift-city/
    districts/
    npcs/
    businesses/
    activities/
    dialogue/

  roadside-station/
    locations/
    customers/
    businesses/
    activities/
```

Night Shift City wäre dann das erste und wichtigste Content Pack.

## RPG-/Story-Generator-Gedanke

Die Systeme könnten langfristig nicht nur ein Spiel antreiben, sondern auch Geschichten erzeugen.

Wenn NPCs Routinen, Orte, Bedürfnisse und Business-Interaktionen haben, entstehen automatisch kleine Erzählungen:

- Ein Stammkunde bleibt länger als sonst.
- Ein Arbeiter kommt nicht mehr, weil seine Schicht geändert wurde.
- Ein Stadtteil verändert sich durch neue Öffnungszeiten.
- Ein Laden wird bekannt und zieht neue Gruppen an.
- Ein Ambient NPC taucht mehrfach auf und wird zur wiedererkennbaren Figur.

Das kann später als Grundlage für:

- emergente Geschichten
- Simulationslogs
- Dialoghinweise
- Quest-Ideen
- Story Seeds
- Content-Generatoren

genutzt werden.

## Gefahr: Zu generisch werden

Eine generische Engine ist verführerisch, aber gefährlich.

Wenn zu früh alles für alle Settings funktionieren soll, entsteht schnell ein abstraktes Framework ohne spielbaren Kern.

## Gegenregel

> Generisch denken, konkret beweisen.

Night Shift City bleibt der konkrete Beweisfall. Jede generische Abstraktion muss zunächst einem echten Night-Shift-City-Use-Case dienen.

## Praktische Regel

Ein System darf generisch designt werden, aber nur implementiert werden, wenn es für den aktuellen MVP gebraucht wird.

Beispiel:

- Gut: Business-System heißt intern generisch `Business`, nicht `CyberpunkBar`.
- Gut: Night Shift City liefert eine konkrete `bar`-Definition als Content.
- Schlecht: Vor MVP 0 ein komplettes RPG-Maker-Framework bauen.

## MVP-Auswirkung

Für MVP 0 bedeutet das:

- Die Schedule Engine sollte keine Cyberpunk-Begriffe hardcoden.
- NPCs sollten als `actors` oder `characters` modelliert werden können.
- Locations sollten generische Tags und Funktionen haben.
- Night Shift City liefert konkrete Testdaten.

## Mögliche spätere Extraktion

Wenn die Engine stabil genug ist, könnte sie später in ein eigenes Paket oder Repository ausgelagert werden.

Mögliche Namen / Konzepte:

- RoutineSim
- Living District Engine
- Small Life Engine
- Urban Routine Engine
- Cozy Sim Toolkit

Aber diese Auslagerung ist kein kurzfristiges Ziel.

## Entscheidung

Night Shift City wird als erstes Spiel und erster Proof of Concept entwickelt.

Die darunterliegenden Systeme werden bewusst so gestaltet, dass sie später auch andere Settings und Spiele tragen könnten, ohne jetzt schon als vollständiger RPG Maker gebaut zu werden.

## Wichtigste Regel

> Night Shift City ist der Anker. Die Engine ist die Möglichkeit dahinter.
