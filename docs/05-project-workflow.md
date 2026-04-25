# Night Shift City – Project Workflow

Dieses Projekt wird bewusst in zwei großen Modi entwickelt:

1. **Meta-Design / Konzeption**
2. **Umsetzung / Codex-Ausführung**

Der Zweck dieser Trennung ist, Gedanken, Visionen und Systemideen zuerst sauber zu verstehen und ausführlich zu dokumentieren, bevor daraus konkrete Implementierungsaufgaben entstehen.

## 1. Meta-Design / Konzeption

In diesem Modus werden Ideen besprochen, geschärft und dokumentiert.

Ziele:

- Vision klären
- Spielgefühl beschreiben
- Systeme entwerfen
- Design Pillars festlegen
- Scope bewusst begrenzen
- offene Fragen sammeln
- technische Grundlogik definieren
- spätere Codex-Aufgaben vorbereiten

In dieser Phase ist es erlaubt, frei zu denken. Ideen müssen noch nicht sofort implementierbar sein. Wichtig ist aber, am Ende die relevanten Gedanken in strukturierte Dokumente zu überführen.

Typische Ergebnisse:

- Vision-Dokumente
- System-Design-Dokumente
- Content-Konzepte
- MVP-Roadmaps
- offene Fragen
- technische Leitplanken

## 2. Umsetzung / Codex-Ausführung

In diesem Modus wird aus der Dokumentation konkrete Arbeit abgeleitet.

Ziele:

- Issues erstellen
- Tasks/Subtasks schneiden
- Akzeptanzkriterien definieren
- kleine Implementierungsschritte planen
- Prototypen bauen
- Tests und Debug-Ausgaben ergänzen
- PRs erzeugen und reviewen

Codex soll nicht aus vagen Ideen heraus direkt große Features bauen, sondern anhand der dokumentierten Konzepte kleine, klare Aufgaben umsetzen.

## Source of Truth

Die Dokumentation im Repository ist der primäre Kontext für Codex und andere Agents.

Wichtige Quellen:

- `AGENTS.md`
- `docs/00-vision.md`
- `docs/01-design-pillars.md`
- `docs/02-systems-map.md`
- `docs/03-mvp-roadmap.md`
- `docs/04-codex-working-rules.md`
- `docs/systems/*`

Wenn sich ein Konzept im Gespräch ändert, soll die relevante Dokumentation aktualisiert werden, bevor daraus größere Implementierungen entstehen.

## Workflow von Idee zu Code

```text
Geistesblitz / Gespräch
        ↓
Konzept schärfen
        ↓
Dokumentation erweitern
        ↓
Systemgrenzen und MVP-Scope klären
        ↓
Issue / Task / Subtask erstellen
        ↓
Codex implementiert kleinsten sinnvollen Schritt
        ↓
Review / Tests / Debug-Ausgabe
        ↓
Dokumentation ggf. aktualisieren
```

## Warum diese Trennung wichtig ist

Night Shift City ist bewusst kein Projekt, bei dem ein Agent einfach „ein Spiel bauen“ soll.

Das Projekt lebt von:

- Atmosphäre
- kleinen Designentscheidungen
- Simulationstiefe durch Illusion
- Scope-Kontrolle
- datengetriebenen Systemen
- iterativer Erweiterbarkeit

Diese Dinge müssen vor der Implementierung klar genug beschrieben sein, damit Codex nicht aus Versehen falsche Annahmen trifft oder das Projekt in eine andere Richtung zieht.

## Rolle von GPT

GPT dient primär als Sparringspartner und Strukturgeber.

Typische Aufgaben:

- Ideen spiegeln und schärfen
- Scope-Probleme erkennen
- Systemdesign ausformulieren
- Doku erstellen und erweitern
- Backlog-Struktur vorbereiten
- Codex-taugliche Aufgaben formulieren

## Rolle von Codex

Codex dient primär als Ausführungs- und Implementierungsagent.

Typische Aufgaben:

- bestehende Doku lesen
- Issues analysieren
- kleine technische Schritte umsetzen
- Tests ergänzen
- Prototypen bauen
- PRs vorbereiten
- Dokumentation bei technischen Änderungen aktualisieren

## Projektregel

> Erst verstehen. Dann dokumentieren. Dann schneiden. Dann bauen.

## Anti-Pattern

Diese Arbeitsweisen sollen vermieden werden:

- direkt große Features aus vagen Ideen bauen
- neue Systeme ohne Doku-Kontext implementieren
- Grafik/Polishing vor Simulationskern priorisieren
- Designentscheidungen nur im Code verstecken
- Scope-Erweiterungen ohne Rückbindung an die Design Pillars
- Codex ohne klare Akzeptanzkriterien losschicken

## Zielbild

Das Repository soll langfristig ein sauberer gemeinsamer Arbeitsraum sein:

- Mensch bringt Vision, Priorität und Geschmack ein.
- GPT hilft beim Denken, Strukturieren und Dokumentieren.
- Codex hilft beim Umsetzen, Testen und Refactoren.

Dadurch kann aus einer losen Ideensammlung schrittweise ein baubares, nachvollziehbares und erweiterbares Spiel-/Engine-Projekt entstehen.
