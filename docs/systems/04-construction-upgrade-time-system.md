# Construction & Upgrade Time System

## Ziel

Das Construction & Upgrade Time System beschreibt, dass Käufe, Umbauten, Renovierungen und Erweiterungen nicht sofort passieren, sondern Zeit brauchen.

Wenn der Spieler ein Gebäude kauft, umbauen lässt oder ein Business erweitert, soll daraus ein erwartbarer Prozess entstehen: Planung, Baustelle, Wartezeit, sichtbarer Fortschritt und schließlich Eröffnung.

Dieses System bringt Animal-Crossing-/Cozy-Life-Sim-Elemente in Night Shift City: Dinge brauchen Zeit, und genau dadurch bekommen sie Bedeutung.

Wichtig: Diese Zeit ist ausschließlich Ingame-Zeit. Es gibt keine Real-Life-Timer, keine echte Uhrzeitbindung und keine Erwartung, dass der Spieler an einem bestimmten realen Tag oder zu einer bestimmten realen Uhrzeit online ist.

## Design-Kernsatz

> Fortschritt darf dauern, damit er sich nach Fortschritt anfühlt – aber nur innerhalb der Spielzeit.

## Inspiration und Gefühl

Die Idee orientiert sich an cozy Aufbau- und Lebenssimulationsspielen wie Animal Crossing oder ähnlichen Life-Sim-/Town-Sim-Ansätzen:

- Heute wird etwas beschlossen.
- Morgen oder später ist es fertig.
- Währenddessen verändert sich der Ort sichtbar.
- Der Spieler freut sich auf die Fertigstellung.

Für Night Shift City bedeutet das:

- Ein gekaufter Shop wird nicht sofort zur Bar.
- Ein Umbau erzeugt eine Baustelle.
- Erweiterungen brauchen Zeit.
- Mitarbeiter oder Lieferanten können vorbereitet werden.
- Eröffnung wird zu einem kleinen Moment.

Der wichtige Unterschied zu Real-Time-Cozy-Spielen:

> Der Spieler wartet nicht im echten Leben. Er erlebt Zeit im Spiel.

## Warum das wichtig ist

Sofortige Upgrades können sich bedeutungslos anfühlen.

Zeitbasierter Ausbau erzeugt:

- Vorfreude
- Planung
- Rhythmus
- Wiederkommen
- Stadtgefühl
- sichtbare Veränderung
- sanfte Progression

Der Spieler soll denken:

> „Morgen im Spiel ist mein neuer Laden fertig. Ich fahr später nochmal vorbei.“

Nicht:

> „Ich muss morgen in echt wiederkommen.“

## Verbindung zur Gesamtvision

Night Shift City soll kein hektischer Tycoon sein. Der Spieler soll wachsen, aber nicht durch permanente Klick-Optimierung.

Construction Time unterstützt dieses Ziel:

- Wachstum wird entschleunigt.
- Fortschritt fühlt sich organisch an.
- Der Spieler hat zwischen Bauphasen Zeit zum Erkunden, Arbeiten oder Beobachten.
- Die Welt wirkt weniger wie ein Menü und mehr wie ein Ort.

## Generische Engine-Sicht

Dieses System sollte generisch als zeitbasierte Veränderung von Locations, Businesses oder World Objects gedacht werden.

Die Engine kennt Konzepte wie:

- Project
- Construction Job
- Start Time
- Duration
- Required Cost
- Required Conditions
- Target Location
- Resulting State
- Progress State
- Completion Event

Sie muss nicht wissen, ob aus einem Cyberpunk-Klamottenladen eine Bar wird oder aus einer Tankstelle ein größerer Shop.

## Game-Layer-Sicht für Night Shift City

Night Shift City nutzt dieses System für:

- Gebäudeumbauten
- Business-Eröffnungen
- Renovierungen
- Erweiterungen
- Deko-/Atmosphäre-Upgrades
- neue Räume
- neue Services
- neue Ausstattung

Beispiele:

- Kleidungsladen → kleine Bar
- alter Imbiss → Nacht-Imbiss
- leerer Laden → Metro-Kiosk
- Bar → Bar mit Dancefloor
- Essensstand → kleiner Indoor-Shop

## Bauprojekt als Datenmodell

Beispiel:

```yaml
id: project_convert_old_threads_to_bar
projectType: conversion
location: lower_market.old_thread_outfitters
fromUsage: clothing_store
toBusinessType: bar

cost:
  money: 18000

duration:
  gameDays: 5

requirements:
  - owns_location
  - permits_available

progressStates:
  - gameDayOffset: 0
    state: planning
  - gameDayOffset: 1
    state: demolition
  - gameDayOffset: 3
    state: construction
  - gameDayOffset: 5
    state: final_setup

onComplete:
  setUsage: bar
  unlockBusiness: neon_kettle
  addAwareness:
    lower_market: 5
```

## Zustände eines Bauprojekts

Ein Projekt kann verschiedene Zustände haben:

- planned
- waiting_for_resources
- in_progress
- paused
- blocked
- completed
- cancelled

Für den Anfang reichen:

- planned
- in_progress
- completed

## Sichtbarer Fortschritt

Bauzeit soll, wenn möglich, in der Welt sichtbar sein.

Beispiele:

- Schild: „Under Renovation“
- Baugerüst
- verschlossene Tür
- NPC-Kommentare
- Lieferwagen vor dem Laden
- Licht im Innenraum
- Baustellen-Sound

Für frühe Versionen reicht Debug-Ausgabe:

```text
Day 3, 09:00: Renovation at Old Thread Outfitters is now in construction phase.
Day 5, 18:00: Neon Kettle is ready to open.
```

## Zeitmodell

Bauzeit wird in Spieltagen, Spielstunden oder abstrakten Ingame-Ticks gemessen.

Wichtig ist nicht Realzeit, sondern Spielrhythmus.

Mögliche Skalierung:

- kleine Deko: einige Spielstunden
- kleines Upgrade: 1 Spieltag
- Umbau: mehrere Spieltage
- großer Standortwechsel: 1 Ingame-Woche oder mehr

Dieses System muss mit `docs/systems/05-game-time-calendar-system.md` konsistent bleiben.

## Spieleraktivität während Bauzeit

Während ein Projekt läuft, soll der Spieler andere Dinge tun können:

- einfache Jobs erledigen
- Werbung vorbereiten
- Stadtteile erkunden
- Lieferungen machen
- andere Businesses betreiben
- NPCs beobachten
- Kapital aufbauen
- schlafen oder Ingame-Zeit vergehen lassen

Dadurch wird Wartezeit nicht Leerlauf, sondern Teil des Loops.

## Keine Mobile-Game-Falle

Wichtig: Bauzeiten sollen nicht wie künstliche Wartebarrieren wirken.

Nicht gewünscht:

- Echtgeld-Beschleunigung
- Real-Life-Timer
- echte 24h-Wartezeiten
- harte Wartepflicht ohne Alternative
- unnötig lange Timer
- tägliche Login-Pflicht
- Bestrafung, wenn man nicht pünktlich zurückkommt
- Inhalte, die nur an echten Wochentagen verfügbar sind

Gewünscht:

- organischer Ingame-Rhythmus
- Vorfreude
- sichtbare Veränderung
- freie Nebenaktivitäten
- cozy Progression
- vollständige Unabhängigkeit von echter Uhrzeit

## Beschleunigung und Einfluss

Später könnte der Spieler Bauzeiten innerhalb des Spiels beeinflussen:

- mehr Ingame-Geld investieren
- bessere Crew beauftragen
- selbst helfen
- Materialien besorgen
- Genehmigungen schneller klären

Aber diese Optionen sollten nicht zu Optimierungsstress führen.

## Verbindung zum Location Ownership & Conversion System

Dieses System erweitert das Location Ownership & Conversion System.

Ownership entscheidet:

> Darf der Spieler diesen Ort verändern?

Conversion entscheidet:

> Was soll aus dem Ort werden und wie teuer ist es?

Construction Time entscheidet:

> Wie lange dauert die Veränderung in Ingame-Zeit und wie wird sie sichtbar?

## Verbindung zum Business System

Business-Erweiterungen können ebenfalls Bauprojekte sein:

- mehr Sitzplätze
- bessere Küche
- Barbereich
- Dancefloor
- bessere Beleuchtung
- Lagerraum
- zweite Etage

Diese Upgrades beeinflussen später:

- Kapazität
- Kundentypen
- Aufenthaltsdauer
- Reputation
- Betriebskosten
- Angebot

## Verbindung zur NPC-Simulation

Bauprojekte können NPCs beeinflussen:

- Stammkunden kommentieren den Umbau.
- Arbeiter meiden vorübergehend den Ort.
- Neugierige NPCs schauen vorbei.
- Bauarbeiter erscheinen als temporäre NPCs.
- Nach Eröffnung steigt Awareness lokal.

Das muss nicht sofort tief simuliert werden, aber es ist langfristig ein starker Immersionshebel.

## Verbindung zur Progression

Bauzeiten unterstützen Progression ohne harte Missionsstruktur.

Der Spieler setzt sich Ziele selbst:

- „Ich spare auf diesen Umbau.“
- „Während gebaut wird, erkunde ich den nächsten District.“
- „Zur Eröffnung will ich Werbung gemacht haben.“

Das Spiel zieht den Spieler durch Vorfreude, nicht durch Druck.

## Generische Wiederverwendbarkeit

Dieses System kann auch andere spätere Settings tragen:

### Tankstellen-Sim

- neue Zapfsäule bauen
- Shop erweitern
- Waschanlage installieren
- Lagerraum ausbauen

### Dorfkneipen-Sim

- Terrasse bauen
- Küche renovieren
- Vereinszimmer einrichten

### Spaceport-Kiosk

- zusätzlicher Service-Schalter
- Frachtausgabe erweitern
- Sicherheitsmodul installieren

Die Engine braucht dafür nur zeitbasierte Ingame-Projekte und Resultate.

## MVP-Relevanz

Dieses System ist für die Endvision wichtig, aber muss nicht vollständig im ersten Prototyp umgesetzt werden.

Für eine frühe Version reicht:

- ein Bauprojekt kann gestartet werden
- es hat Kosten und Ingame-Dauer
- es wechselt nach Spielzeitablauf den Status
- es erzeugt Debug-Ausgaben
- am Ende wird die Location/Business-Konfiguration geändert

## Beispiel-Debug-Loop

```text
Day 1, 10:00: Player starts conversion project: Old Thread Outfitters -> Bar.
Day 1, 10:01: Project status: in_progress, phase: planning, remaining: 5 game days.
Day 2, 09:00: Construction phase changed to demolition.
Day 4, 09:00: Construction phase changed to interior_setup.
Day 6, 18:00: Project completed. Neon Kettle can now open.
```

## Offene Fragen

- Wie lang sollen typische Bauzeiten im Verhältnis zur Spielzeit sein?
- Können Projekte pausieren oder scheitern?
- Gibt es Bauunternehmen / Crews als eigene Actors oder Services?
- Kann der Spieler mehrere Bauprojekte gleichzeitig laufen lassen?
- Wie sichtbar sind Baustellen in frühen Versionen?
- Soll es Eröffnungsevents geben?
- Wie stark beeinflusst ein Umbau den District während der Bauzeit?

## Wichtigste Regeln

> Umbau ist kein Menü-Klick. Umbau ist ein Ereignis in der Stadt.

> Bauzeit ist immer Ingame-Zeit, niemals Real-Life-Zeit.
