# AGENTS.md – Night Shift City

Dieses Repository darf ausdrücklich durch KI-gestützte Agents wie Codex, GPT-basierte Planungsassistenten oder vergleichbare Coding-/Planning-Agents bearbeitet werden.

## Grundsatz

Agents haben in diesem Repository vollen operativen Zugriff auf:

- Code
- Dokumentation
- Issues
- Tasks
- Subtasks
- Pull Requests
- Backlog-Struktur
- technische Architekturvorschläge
- Refactorings
- Tests
- Debug-/Prototyp-Code

Der Zweck dieses Repositories ist explizit, als gemeinsamer Arbeitsraum zwischen Mensch, GPT und Codex zu funktionieren.

## Agent Permission Model

Agents dürfen eigenständig:

- Issues analysieren, ergänzen und strukturieren.
- Tasks und Subtasks aus größeren Issues ableiten.
- neue Issues für klar abgegrenzte Arbeitspakete vorschlagen oder anlegen.
- Code ändern, ergänzen oder refactoren.
- Dokumentation aktualisieren.
- Akzeptanzkriterien ergänzen.
- technische Spikes vorschlagen.
- Tests hinzufügen oder verbessern.
- kleine Prototypen implementieren.
- Pull Requests vorbereiten.

Agents sollen dabei bevorzugt kleine, nachvollziehbare Änderungen erzeugen.

## Arbeitsmodus

Night Shift City soll nicht als großes, unkontrolliertes Spielprojekt umgesetzt werden, sondern als modularer Engine- und Gameplay-Prototyp.

Bevorzugte Reihenfolge:

1. Konzept sauber dokumentieren.
2. Systeme klein schneiden.
3. Issues/Tasks/Subtasks definieren.
4. Headless-/Debug-Prototypen bauen.
5. Tests und Debug-Ausgaben ergänzen.
6. Erst danach Visualisierung und Polishing.

## Projektvision

Night Shift City ist ein cozy Cyberpunk-Erkundungsspiel, getragen von einem leichten Business-System.

Der Spieler lebt in einer Stadt, die größer wirkt als er selbst. Der Fokus liegt auf Atmosphäre, Erkundung, wiederkehrenden NPCs, Routinen, kleinen Businesses und einer Stadt, die scheinbar auch ohne den Spieler existiert.

Wichtige Leitidee:

> Der Spieler entdeckt keine Inhalte – er entdeckt Zusammenhänge.

## Design Pillars

Agents müssen bei Änderungen diese Design Pillars berücksichtigen:

1. Cozy statt Stress.
2. Beobachtung ist Gameplay.
3. NPCs wirken wie Bewohner, nicht wie Kulisse.
4. Business ist Motor, nicht Zwang.
5. Exploration speist das Business.
6. Datengetrieben vor hardcoded.
7. Kleine Aktionen, spürbare Wirkung.
8. Die Stadt ist nicht für den Spieler gebaut – der Spieler lebt nur darin.

## Technische Leitplanken

Agents sollen bevorzugt:

- Engine-Logik und Content trennen.
- Datengetriebene Modelle für NPCs, Locations, Businesses und Schedules nutzen.
- kleine, testbare Module bauen.
- Debug-/Headless-Simulationen ermöglichen.
- Entscheidungen dokumentieren, wenn sie Architektur betreffen.
- existierende Docs aktualisieren, wenn sich Konzepte ändern.

Agents sollen vermeiden:

- große unbesprochene Framework-Wechsel.
- Scope-Explosion durch Combat, Storykampagne oder Mega-Corp-Endgame.
- harte Verdrahtung von Content, wenn Datenmodelle sinnvoller sind.
- komplexe KI-Systeme, bevor einfache Routinen stabil laufen.
- Grafik/Polishing vor Simulationskern.

## Issue- und Task-Regeln

Gute Issues enthalten:

- Kontext
- Ziel
- Akzeptanzkriterien
- Out of Scope
- betroffene Systeme
- erwartete Tests oder Debug-Ausgaben

Große Issues sollen in kleinere Subtasks zerlegt werden.

Empfohlene Labels:

- `type:concept`
- `type:feature`
- `type:task`
- `type:spike`
- `type:docs`
- `system:npc`
- `system:business`
- `system:world`
- `system:simulation`
- `system:content`
- `system:codex`
- `status:needs-refinement`
- `status:ready`
- `status:blocked`

## MVP-Reihenfolge

Aktuelle MVP-Reihenfolge:

1. MVP 0 – Living Schedule Prototype
2. MVP 1 – First District
3. MVP 2 – First Business Loop
4. MVP 3 – Micro Actions
5. MVP 4 – Minimal Visual Prototype
5. MVP 5 – Exploration Hook

Details siehe:

- `docs/00-vision.md`
- `docs/01-design-pillars.md`
- `docs/02-systems-map.md`
- `docs/03-mvp-roadmap.md`
- `docs/04-codex-working-rules.md`

## Codex Task Template

```md
## Context
This task belongs to Night Shift City.
Relevant design pillars:
- Cozy statt Stress
- Beobachtung ist Gameplay
- Datengetrieben vor hardcoded

## Goal
Describe the smallest useful outcome.

## Acceptance Criteria
- [ ] Clear, testable criterion
- [ ] Clear, testable criterion

## Out of Scope
- Explicitly list what must not be implemented yet.

## Notes
Mention affected docs, systems or follow-up issues.
```

## Wichtigste Projektregel

> Erst Herzschlag, dann Grafik.

Der erste große technische Beweis ist eine Stadt, die als Debug-/Textsimulation lebt.
