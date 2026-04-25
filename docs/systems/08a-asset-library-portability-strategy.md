# Asset Library – Portability Strategy

## Entscheidung

Das Asset-Library-/Asset-Indexing-System wird zunächst als internes Tool für Night Shift City behandelt, aber bewusst so konzipiert, dass es später aus dem Projekt herausgelöst und als eigenständige Tool-Bibliothek wiederverwendet werden kann.

## Design-Kernsatz

> Internal tool first. Extraction-ready by design.

Das Tool soll zuerst ein echtes Problem im aktuellen Projekt lösen: eine sehr große gekaufte Asset-Sammlung auffindbar und nutzbar machen.

Gleichzeitig soll die Architektur vermeiden, dass das Tool so stark mit Night Shift City verdrahtet wird, dass es später nicht mehr für andere Projekte verwendbar ist.

## Warum nicht sofort ein eigenes Projekt?

Ein eigenes Tool-Projekt wäre zum aktuellen Zeitpunkt riskant, weil es schnell zu einem eigenen Nebenprojekt werden könnte, bevor klar ist, welche Funktionen wirklich gebraucht werden.

Aktuell ist der beste Weg:

1. im Kontext von Night Shift City starten
2. echten Nutzungsdruck erzeugen
3. nur die nötigen Funktionen bauen
4. Schnittstellen sauber halten
5. später bei Bedarf auslagern

## Warum trotzdem portabel denken?

Die Asset-Sammlung ist nicht nur für Night Shift City relevant. Sie kann langfristig für mehrere Spielideen, Prototypen oder Tools genutzt werden.

Daher sollte das Asset-System nicht so gebaut werden, als wäre es ausschließlich Night-Shift-City-spezifisch.

## Empfohlene Projektstruktur

Kurzfristig innerhalb dieses Repositories:

```text
tools/
  asset-indexer/
    src/
    tests/
    README.md
    asset-indexer.config.example.json
```

Night-Shift-City-spezifische Konfiguration getrennt davon:

```text
assets/
  index/
  curated/
  game/

docs/systems/08-asset-library-system.md
```

Wichtig: Das Tool selbst sollte keine Night-Shift-City-spezifischen Annahmen hart enthalten.

## Trennung zwischen Tool und Projektkontext

### Tool darf wissen

- wie man Ordner scannt
- wie man Dateien klassifiziert
- wie man Metadaten extrahiert
- wie man Hashes erzeugt
- wie man einen Index schreibt
- wie man sucht und filtert
- wie man Reports erzeugt

### Tool soll nicht fest wissen

- was Night Shift City ist
- welche Stadtteile existieren
- welche NPCs existieren
- welche Assets final im Spiel landen
- welche Ästhetik endgültig gilt

Diese Dinge gehören in Projektkonfiguration, Tags oder Kuratierungsdaten.

## Datenmodell mit Wiederverwendung im Blick

Asset-Einträge sollten allgemeine und projektbezogene Felder trennen.

Beispiel:

```json
{
  "id": "asset_000123",
  "hash": "...",
  "path": "assets/raw/example/worker_01.png",
  "type": "image",
  "extension": ".png",
  "width": 64,
  "height": 64,
  "technicalTags": ["png", "transparent", "small_sprite"],
  "sourceTags": ["humble_bundle", "cyberpunk_pack"],
  "manualTags": ["worker", "npc", "pixelart"],
  "projectUsage": {
    "night-shift-city": {
      "status": "candidate",
      "usableFor": ["npc", "prototype"],
      "notes": "Could fit early worker NPC prototype."
    }
  }
}
```

Dadurch kann dasselbe Asset später in mehreren Projekten unterschiedlich bewertet werden.

## SQLite als bevorzugte Richtung

Für erste Experimente kann JSON reichen. Langfristig ist SQLite attraktiv, weil:

- große Asset-Mengen effizienter durchsucht werden können
- ein einzelner Index leicht transportierbar ist
- CLI, UI und Reports auf derselben Datenbasis arbeiten können
- spätere Migrationen möglich bleiben

Empfehlung:

- MVP: JSON oder SQLite, je nach Implementierungsaufwand
- Zielbild: SQLite mit klarer Schema-Version

## Schema-Versionierung

Wenn das Tool wiederverwendbar werden soll, braucht der Index langfristig eine Schema-Version.

Beispiel:

```json
{
  "schemaVersion": 1,
  "generatedAt": "2026-04-25T00:00:00Z",
  "assets": []
}
```

Oder in SQLite:

```text
metadata
  key: schema_version
  value: 1
```

## Konfiguration statt Hardcoding

Projektbezogene Regeln sollten in Konfigurationsdateien liegen.

Beispiel:

```json
{
  "projectId": "night-shift-city",
  "rawAssetRoots": ["D:/Assets/Humble"],
  "tagRules": [
    {
      "matchPathContains": "bar",
      "addTags": ["bar", "ambience"]
    },
    {
      "matchExtension": ".wav",
      "addTags": ["audio"]
    }
  ]
}
```

## Möglicher Extraktionspunkt

Das Tool sollte erst dann in ein eigenes Repository ausgelagert werden, wenn mindestens zwei Bedingungen erfüllt sind:

- Es wird regelmäßig für Night Shift City genutzt.
- Es gibt einen konkreten zweiten Anwendungsfall außerhalb von Night Shift City.

Weitere Auslöser:

- eigenes UI
- mehrere Projekte nutzen denselben Indexer
- Tool bekommt eigene Release-Versionen
- andere Repos sollen es als Dependency nutzen

## Anti-Pattern

Vermeiden:

- perfektes Asset-Management-System bauen, bevor Assets wirklich gebraucht werden
- manuelle Komplettsortierung vor dem ersten Nutzen
- Night-Shift-City-spezifische Begriffe im Tool-Code hardcoden
- Asset-Dateien wild verschieben und Herkunft verlieren
- Lizenzinformationen ignorieren
- KI-Analyse als Voraussetzung für MVP behandeln

## MVP für diese Strategie

Der erste Tool-Prototyp soll nur beweisen:

- große Ordner können gescannt werden
- Dateien werden stabil identifiziert
- technische Metadaten werden extrahiert
- erste Tags entstehen aus Pfad und Dateiname
- Projektstatus kann ergänzt werden
- das Tool ist nicht hart an Night Shift City gekoppelt

## Wichtigste Regel

> Das Tool darf aus Night Shift City entstehen, aber es soll nicht in Night Shift City gefangen sein.
