# Night Shift City – Systems Map

Dieses Dokument beschreibt die wichtigsten Systeme und ihre Beziehung zueinander. Es ist bewusst als Arbeitsstand gedacht und soll mit dem Projekt wachsen.

## Übersicht

```text
World / District System
 ├─ Locations
 ├─ Metro / Travel
 ├─ Ambient Population
 └─ Discovery Hints

NPC System
 ├─ Named NPCs
 ├─ Ambient NPCs
 ├─ Traits
 ├─ Needs
 ├─ Weekly Schedules
 ├─ Activity Pools
 └─ Promotion from Ambient to Named NPC

Business System
 ├─ Business Types
 ├─ Locations / Stands / Shops
 ├─ Customer Attraction
 ├─ Opening Hours
 ├─ Offer / Menu
 ├─ Local Awareness / Advertising
 └─ Passive Stability

Interaction System
 ├─ Observation
 ├─ Dialogue Snippets
 ├─ Small Talk
 ├─ Micro Actions
 └─ Reputation / Familiarity
```

## World / District System

Stadtteile sind modulare Bereiche mit eigenen Orten, NPC-Gruppen, Routinen und wirtschaftlichen Mustern.

### Ziel

Neue Stadtteile sollen später relativ leicht hinzugefügt werden können, ohne die Engine umzubauen.

### Enthält

- Locations wie Wohnung, Bar, Essensstand, Metrostation, Arbeitsplatz.
- Pfade / Routen zwischen Orten.
- Stadtteil-Tags wie `industrial`, `nightlife`, `residential`, `market`.
- lokale Nachfrage und typische NPC-Gruppen.

## NPC System

NPCs sind der emotionale und immersive Kern der Stadt.

### Named NPCs

Wiederkehrende NPCs mit:

- Name
- Wohnort
- optionalem Job
- Traits
- Routinen
- Activity Pools
- Erinnerungs- oder Familiarity-Zustand

### Ambient NPCs

Leichte Statisten, die Stadtfülle erzeugen.

- Nicht dauerhaft vollständig simuliert.
- Können generisch auftreten.
- Verhalten soll zu denselben Stadtregeln passen.
- Können später optional zu Named NPCs promoted werden.

### Promotion System

Ambient NPCs können zu echten wiederkehrenden NPCs werden, wenn sie häufig relevant werden oder der Spieler sie mehrfach bemerkt.

Beispiel:

```text
Ambient NPC wird mehrmals im selben Viertel gesehen
→ bekommt wiedererkennbare Merkmale
→ bekommt Namen
→ bekommt einfache Routine
→ wird Named NPC
```

## Routine / Schedule System

NPCs sollen Gewohnheiten haben, aber nicht mechanisch exakt wiederholen.

### Prinzip

> Routine ist Erwartbarkeit mit Störungen.

### Bausteine

- Wochentagsabhängige Zeitpläne.
- Zeitfenster statt fixe Uhrzeiten.
- Aktivitätsdauer als Bereich.
- Bedingungen und Wahrscheinlichkeiten.
- Abweichungen durch Stress, Wetter, Geld, Müdigkeit, Laune oder Events.

Beispiel:

```yaml
friday_evening:
  preferredActivity: bar_01
  timeWindow: "21:30-23:00"
  duration: "1h-4h"
  probability: 0.75
  modifiers:
    - if: stress > 70
      durationBonus: "+1h"
    - if: money < 15
      probability: -0.40
```

## Business System

Das Business-System ist der sanfte Motor der Gameloop.

### Ziel

Der Spieler kann ein kleines Business aufbauen, das Einnahmen erzeugt, Stammkunden anzieht und neue Erkundung motiviert.

### Mögliche Business-Typen

- Bar
- Essensstand
- kleines Restaurant
- Taxi-Service
- Lieferdienst
- Mini-Shop

### Wichtige Parameter

- Standort
- Öffnungszeiten
- Angebot
- Bekanntheit im Stadtteil
- Stammkunden
- Betriebskosten
- lokale Nachfrage

## Micro Action System

Kleine Aktionen halten den Loop lebendig.

Beispiele:

- Werbung in anderem Stadtteil machen.
- Flyer verteilen.
- Standort scouten.
- Öffnungszeiten ändern.
- Menü anpassen.
- Ausstattung/Deko verbessern.
- Mit Stammkunden kurz reden.

Diese Aktionen sollen geringe Komplexität haben, aber spürbare Auswirkungen erzeugen.

## Exploration / Discovery System

Exploration soll neue Zusammenhänge sichtbar machen.

Beispiele:

- Ein Stadtteil hat viele Arbeiter nach 19 Uhr.
- Eine Metrostation erzeugt viel Laufkundschaft.
- Ein Nachtviertel braucht späte Öffnungszeiten.
- Ein bestimmter NPC bringt Freunde mit, wenn er zufrieden ist.

## Simulationszustände

Um solo-dev-tauglich zu bleiben, sollen NPCs nicht immer voll simuliert werden.

```text
Dormant  = weit weg, nur abstrakter Zeitstatus
Abstract = im Stadtteil, aber nicht sichtbar
Active   = nahe beim Spieler, echte Bewegung/Interaktion möglich
```

## Priorität für den ersten Prototyp

1. Zeit- und Tagesmodell.
2. Orte laden.
3. 3–5 Named NPCs mit Routinen.
4. Ein Business mit Kundenzufluss.
5. Eine Micro Action: Werbung machen.
6. Debug-/Textausgabe vor Grafik.
