# Minimal Custom Engine Philosophy

## Ausgangspunkt

Night Shift City soll nicht auf einer großen bestehenden Engine aufgebaut werden, nur weil diese theoretisch alles kann.

Der Wunsch nach einer eigenen Engine entsteht nicht aus dem Ziel, Unreal, Unity oder Godot nachzubauen. Es geht darum, eine kleine, verständliche und gezielt passende Grundlage zu schaffen, die zu den Systemen, Denkmodellen und Arbeitsweisen dieses Projekts passt.

## Design-Kernsatz

> Keine Universal-Engine. Eine kleine Engine, die wir verstehen.

## Warum eine eigene Minimal-Engine?

Eine eigene Engine kann sinnvoll sein, wenn sie bewusst klein bleibt und direkt aus den Anforderungen von Night Shift City entsteht.

Motivation:

- Die Engine soll verständlich bleiben.
- Die Begriffe sollen zum Spiel passen: Actor, Routine, Location, Business, Activity, District.
- Codex und andere Agents sollen leichter im Code navigieren können.
- Systeme sollen datengetrieben und testbar sein.
- Die Simulationslogik soll wichtiger sein als Grafik-Features.
- Das Projekt soll nicht durch das Lernen oder Anpassen einer großen Fremd-Engine ausgebremst werden.

## Was diese Engine sein soll

Die Engine soll ein kleiner, modularer Simulations- und Spielrahmen sein.

Sie soll unterstützen:

- Zeitmodell
- Datengetriebene Content-Definitionen
- Actor-/NPC-Routinen
- Locations und Districts
- Business-Systeme
- Activity-Auswahl
- Micro Actions
- Debug-/Headless-Simulation
- später einfache Darstellung / Rendering-Anbindung

## Was diese Engine nicht sein soll

Sie soll nicht versuchen, eine große Game Engine zu ersetzen.

Nicht kurzfristig enthalten:

- allgemeiner 3D-Renderer
- Physik-Engine
- komplexes Animationssystem
- Editor wie Unity/Godot
- vollständiger RPG Maker
- Netzwerk-/Multiplayer-System
- generischer Visual-Scripting-Editor
- universelles Asset-Pipeline-Monster

## Grundprinzip: Simulation First

Die wichtigste Ebene ist nicht Rendering, sondern Simulation.

Die erste Frage lautet nicht:

> Wie sieht das aus?

Sondern:

> Lebt das System auch als Debug-/Textsimulation?

Wenn NPCs, Orte, Businesses und Tagesabläufe ohne Grafik sinnvoll funktionieren, kann später eine visuelle Ebene darauf aufgebaut werden.

## Engine-Schichten

```text
Content Layer
 ├─ NPC definitions
 ├─ District definitions
 ├─ Business definitions
 ├─ Activity pools
 └─ Dialogue snippets

Simulation Layer
 ├─ Time / Calendar
 ├─ Actors / NPCs
 ├─ Locations
 ├─ Activities
 ├─ Business logic
 ├─ Demand / Awareness
 └─ Events / State changes

Presentation Layer
 ├─ Debug logs
 ├─ Debug UI
 ├─ 2D / isometric rendering
 ├─ audio playback
 └─ player input
```

## Codex-Freundlichkeit

Die Engine soll so gebaut werden, dass Codex gut damit arbeiten kann.

Dafür wichtig:

- klare Ordnerstruktur
- kleine Module
- sprechende Namen
- viele Tests oder Debug-Beispiele
- dokumentierte Datenformate
- keine versteckte Magie
- keine riesigen Klassen mit zu vielen Verantwortlichkeiten

## Generisch, aber nicht abstrakt

Die Engine darf generische Konzepte verwenden, aber nur soweit sie für Night Shift City nützlich sind.

Gut:

- `Actor`
- `Location`
- `Business`
- `Activity`
- `Schedule`
- `District`

Riskant:

- abstrakte Universal-Entity-Systeme ohne konkreten Use Case
- Plugin-Architekturen vor dem ersten Prototyp
- generische RPG-Maker-Funktionen, bevor das Spielgefühl klar ist

## Praktische Regel

> Jede Engine-Abstraktion braucht einen konkreten Night-Shift-City-Anwendungsfall.

Wenn es keinen aktuellen Use Case gibt, bleibt es Backlog oder Idee.

## Beispiel

Nicht bauen:

```text
UniversalGameObjectWithComponentGraphFactory
```

Besser:

```text
Actor
  has Schedule
  has CurrentActivity
  has HomeLocation
  has Traits
```

Das ist generisch genug für spätere Wiederverwendung, aber konkret genug für den ersten Prototyp.

## Verhältnis zu bestehenden Engines

Bestehende Engines sind nicht grundsätzlich ausgeschlossen.

Mögliche spätere Nutzung:

- MonoGame für Rendering und Input
- kleinere Libraries für Audio, Datenformate oder UI
- bestehende Tools für Asset-Metadaten

Aber die Kernlogik von Night Shift City soll unabhängig und verständlich bleiben.

## Zielbild

Die eigene Engine soll nicht beeindrucken, sondern Arbeit erleichtern.

Sie ist erfolgreich, wenn:

- neue NPCs einfach hinzugefügt werden können
- neue Businesses über Daten definiert werden können
- Stadtteile modular wachsen
- Codex Aufgaben nachvollziehbar umsetzen kann
- Debug-Simulationen schnell Feedback geben
- der Entwickler versteht, warum etwas passiert

## Wichtigste Regel

> Die Engine wächst aus dem Spiel heraus. Nicht das Spiel aus der Engine.
