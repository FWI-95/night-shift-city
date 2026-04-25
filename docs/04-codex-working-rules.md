# Night Shift City – Codex Working Rules

Dieses Dokument beschreibt, wie Codex oder andere KI-gestützte Coding-Agenten am Projekt arbeiten sollen.

## Grundprinzip

Codex soll nicht frei „ein Cyberpunk-Spiel bauen“, sondern kleine, klar abgegrenzte Engine- und Content-Bausteine umsetzen.

## Arbeitsweise

Jede Aufgabe soll enthalten:

- Kontext
- Ziel
- Akzeptanzkriterien
- Out of Scope
- betroffene Systeme
- erwartete Tests oder Debug-Ausgaben

## Design-Kontext für jede Aufgabe

Wenn eine Aufgabe erstellt wird, soll sie mindestens auf diese Prinzipien verweisen:

- Cozy statt Stress.
- Beobachtung ist Gameplay.
- Business ist Motor, nicht Zwang.
- NPCs sollen wie Bewohner wirken.
- Datengetrieben vor hardcoded.

## Codex soll bevorzugt

- kleine, testbare Schritte umsetzen.
- Engine-Logik und Content trennen.
- Datenmodelle klar dokumentieren.
- Debug-/Headless-Simulationen zuerst ermöglichen.
- Architekturentscheidungen in Docs ergänzen.
- bei Unsicherheit minimal und erweiterbar implementieren.

## Codex soll vermeiden

- große Framework-Wechsel ohne explizite Aufgabe.
- Grafiksysteme vor Simulationskern zu priorisieren.
- Spielmechaniken hart zu verdrahten, wenn sie datengetrieben sein können.
- komplexe KI-Systeme einzubauen, bevor einfache Routinen funktionieren.
- unnötige Scope-Erweiterungen wie Storykampagnen, Combat oder Mega-Corp-Endgame.

## Beispiel für eine gute Aufgabe

```md
## Context
This belongs to the NPC Routine System of Night Shift City.
NPCs should feel like recurring inhabitants, not static props.

## Goal
Implement a headless schedule simulation for named NPCs.

## Acceptance Criteria
- NPC definitions can be loaded from JSON/YAML.
- NPCs can have weekday-specific schedules.
- Activities use time windows, not only fixed timestamps.
- The simulation logs state changes for at least three NPCs.

## Out of Scope
- Rendering.
- Dialogue.
- Business logic.
- Pathfinding.
```

## Projektregel

> Erst Herzschlag, dann Grafik.

Der erste große technische Beweis ist eine Stadt, die als Debug-/Textsimulation lebt.
