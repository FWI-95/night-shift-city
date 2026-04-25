# Night Shift City – MVP Roadmap

Diese Roadmap beschreibt eine bewusst kleine, sprintfähige Reihenfolge. Ziel ist nicht sofort ein fertiges Spiel, sondern ein belastbarer Engine-Kern.

## MVP 0 – Living Schedule Prototype

### Ziel

Drei NPCs leben einen Tag in einer Text-/Debugsimulation.

### Enthält

- GameClock mit Tageszeit und Wochentag.
- Datenmodell für NPCs.
- Datenmodell für Locations.
- Wochentagsabhängige Schedules.
- Zeitfenster und Aktivitätsdauer.
- Einfache Activity-Auswahl.
- Log-Ausgabe der NPC-Zustände.

### Nicht enthalten

- Grafik.
- Business-System.
- Dialogsystem.
- Beziehungen.
- komplexe Pfadfindung.

### Erfolgskriterium

Eine Debug-Ausgabe zeigt nachvollziehbar, dass NPCs ihren Tagesablauf verfolgen und dabei leichte Variationen entstehen.

## MVP 1 – First District

### Ziel

Ein kleiner Stadtteil existiert als Datenmodell.

### Enthält

- 1 Apartment-Komplex.
- 1 Arbeitsplatz.
- 1 Essensstand oder Bar.
- 1 Metrostation.
- 5–10 Locations insgesamt.
- einfache Distanz-/Reisezeitlogik.

### Erfolgskriterium

NPCs wechseln plausibel zwischen Orten. Offscreen-Aktivitäten werden abstrakt verarbeitet.

## MVP 2 – First Business Loop

### Ziel

Der Spieler besitzt ein kleines Business, das NPCs anzieht und Geld erzeugt.

### Enthält

- 1 Business-Typ, z. B. Bar oder Essensstand.
- Öffnungszeiten.
- einfaches Angebot.
- lokale Bekanntheit.
- Kundenzufluss durch NPCs.
- Einnahmen und einfache Betriebskosten.

### Erfolgskriterium

NPCs besuchen das Business abhängig von Routine, Nähe, Bedürfnissen und Bekanntheit.

## MVP 3 – Micro Actions

### Ziel

Der Spieler kann kleine Aktionen ausführen, die die Simulation beeinflussen.

### Erste Micro Action

Werbung in einem Stadtteil machen.

### Effekt

- Erhöht temporär die lokale Bekanntheit.
- Kann neue Kunden aus dem beworbenen Stadtteil bringen.
- Klingt nach Spielhandlung, bleibt aber technisch klein.

### Erfolgskriterium

Nach Werbung verändert sich der Kundenzufluss messbar, aber nicht übertrieben.

## MVP 4 – Minimal Visual Prototype

### Ziel

Die Simulation bekommt eine einfache visuelle Darstellung.

### Enthält

- Top-down oder isometrische Testansicht.
- sichtbare Locations.
- simple NPC-Bewegung im aktiven Bereich.
- Debug-Overlay für Zeit, NPC-Zustand und Business-Werte.

### Erfolgskriterium

Der Spieler kann sich in einem kleinen Stadtteil bewegen und erste NPC-Routinen beobachten.

## MVP 5 – Exploration Hook

### Ziel

Erkundung soll einen spürbaren Nutzen bekommen.

### Enthält

- 2. kleiner Stadtteil oder Testbereich.
- Metro-/Travel-Aktion.
- Scouten von Nachfrage.
- erste Hinweise durch Beobachtung oder Gesprächsfetzen.

### Erfolgskriterium

Der Spieler kann durch Erkundung eine Business-Entscheidung besser treffen.

## Backlog-Parkplatz

Diese Themen sind spannend, aber nicht MVP-kritisch:

- Dialogsystem mit Gesprächsfetzen.
- Ambient NPC Promotion.
- mehrere Business-Typen.
- Mitarbeiter einstellen.
- Apartment-System.
- Hunger/Müdigkeit für den Spieler.
- Wetter.
- Reputation/Familiarity.
- komplexere Beziehungen zwischen NPCs.
