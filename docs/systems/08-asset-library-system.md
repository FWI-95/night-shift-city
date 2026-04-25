# Asset Library / Asset Indexing System

## Ausgangslage

Für Night Shift City existiert potenziell eine große Sammlung gekaufter, frei nutzbarer Assets aus Humble Bundles oder ähnlichen Quellen. Diese Sammlung kann Sprites, Tilesets, UI-Grafiken, Audiofiles, Musik, Soundeffekte und andere Ressourcen enthalten.

Das Problem ist nicht der Mangel an Assets, sondern die Masse und Unübersichtlichkeit.

Wenn tausende Dateien unstrukturiert vorliegen, werden sie im Projektalltag schwer nutzbar. Gute Assets bleiben unentdeckt, Dopplungen entstehen, und Codex oder andere Agents können nicht sinnvoll darauf zugreifen.

## Ziel

Es soll ein Asset-Library-System entstehen, das vorhandene Assets auffindbar, bewertbar und später projektbezogen nutzbar macht.

Der Fokus liegt nicht darauf, Assets sofort perfekt automatisch zu verstehen, sondern darauf, sie schrittweise indexierbar und kuratierbar zu machen.

## Design-Kernsatz

> Die Asset-Sammlung soll nicht sortiert werden müssen, bevor sie nutzbar wird. Sie soll durch Nutzung und Analyse langsam verständlicher werden.

## Grundidee

Statt alle Assets manuell in Ordner zu sortieren, wird ein Index aufgebaut.

Der Index enthält Metadaten zu jeder Datei:

- Pfad
- Dateiname
- Dateityp
- Größe
- Dimensionen bei Bildern
- Dauer bei Audio
- grobe Kategorie
- Tags
- Lizenz-/Quellenhinweis
- Projektverwendung
- manuelle Notizen
- Qualitätseinschätzung
- Status

Die Originaldateien können dabei in ihrer bestehenden Struktur bleiben. Der Index bildet die eigentliche Arbeitsgrundlage.

## Mögliche Index-Formate

Für den Anfang reicht ein einfaches maschinenlesbares Format:

- JSON
- SQLite
- CSV für erste Experimente

Langfristig ist SQLite besonders interessant, weil viele Dateien effizient durchsucht werden können und einfache Tools darauf aufbauen können.

## Beispiel-Metadaten

```json
{
  "id": "asset_000123",
  "source": "humble_bundle_unknown_pack",
  "path": "assets/raw/sprites/cyberpunk/characters/worker_01.png",
  "fileName": "worker_01.png",
  "type": "image",
  "extension": ".png",
  "width": 64,
  "height": 64,
  "tags": ["character", "worker", "npc", "pixelart"],
  "mood": ["urban", "neutral"],
  "usableFor": ["npc", "prototype"],
  "license": "purchased_bundle_check_details",
  "status": "candidate",
  "notes": "Could fit early worker NPC prototype."
}
```

## Grobe Asset-Kategorien

### Images

- sprites
- tilesets
- UI
- portraits
- icons
- backgrounds
- effects
- placeholders

### Audio

- music
- ambient loops
- UI sounds
- footsteps
- vehicle sounds
- door sounds
- bar/restaurant ambience
- metro ambience
- notification sounds

### Project Usage

- prototype
- final_candidate
- rejected
- needs_review
- used_in_game

## Automatische Analyse – realistische Einschätzung

### Bilder

Automatisch gut erfassbar:

- Dateityp
- Auflösung
- Transparenz
- Sprite-Sheet-Verdacht
- Farbdurchschnitt / Palette
- Seitenverhältnis
- Dateiname-basierte Tags
- Ordner-basierte Tags

Automatisch schwieriger:

- tatsächlicher Inhalt
- Stilqualität
- ob es zum Projektgefühl passt
- ob Sprite-Frames korrekt geschnitten sind

Mögliche spätere Ansätze:

- Thumbnail-Generator
- einfache Farbanalyse
- manuelles Tagging-UI
- KI-basierte Bildbeschreibung, falls lokal oder per Tool verfügbar

### Audio

Automatisch gut erfassbar:

- Dateityp
- Dauer
- Samplerate
- Kanäle
- Lautheit / Peak
- Loop-Verdacht durch Dateiname
- Ordner-/Dateiname-basierte Tags

Automatisch schwieriger:

- Stimmung
- Instrumentierung
- ob Loop wirklich sauber ist
- ob Soundeffekt zur Situation passt

Mögliche spätere Ansätze:

- Waveform-/Preview-Tool
- Batch-Normalisierung nur nach Review
- manuelles Rating
- grobe Audiofeatures wie Dauer, Lautheit, Spektrum

## Empfohlener Workflow

### Phase 1: Datei-Inventar

Ein Tool scannt die Asset-Ordner und erzeugt einen Rohindex.

Erfasst werden:

- Pfad
- Name
- Extension
- Größe
- Änderungsdatum
- Hash

Ziel:

> Welche Dateien existieren überhaupt?

### Phase 2: Metadaten extrahieren

Für unterstützte Typen werden technische Metadaten ergänzt.

Bilder:

- Breite
- Höhe
- Transparenz
- ggf. Sprite-Sheet-Verdacht

Audio:

- Dauer
- Sample Rate
- Kanäle

### Phase 3: Heuristische Tags

Aus Pfaden und Dateinamen werden erste Tags abgeleitet.

Beispiel:

```text
bar_ambience_loop.wav
→ tags: audio, ambience, bar, loop

cyberpunk_worker_idle.png
→ tags: image, sprite, cyberpunk, worker, idle
```

### Phase 4: Kuratierung

Der Nutzer oder ein Agent bewertet Assets schrittweise.

Mögliche Statuswerte:

- `raw`
- `candidate`
- `needs_review`
- `approved`
- `rejected`
- `used`

### Phase 5: Projektintegration

Aus approved Assets werden projektnahe Packs gebaut.

Beispiele:

- `night_shift_city_prototype_pack`
- `district_lower_market_pack`
- `npc_worker_pack`
- `bar_ambience_pack`

## Wichtiges Prinzip

Originalassets sollten möglichst nicht direkt verändert oder manuell wild verschoben werden.

Stattdessen:

```text
assets/raw/...
assets/index/assets.sqlite
assets/curated/...
assets/game/...
```

Der Index weiß, welches Originalasset zu welchem kuratierten oder exportierten Asset gehört.

## Mögliche Tooling-Idee

Ein internes CLI-Tool könnte später Befehle anbieten:

```bash
asset-index scan assets/raw
asset-index analyze
asset-index search --tag bar --type audio
asset-index approve asset_000123
asset-index export-pack lower-market-prototype
```

## Rolle für Codex

Codex kann später helfen, dieses Tool aufzubauen.

Gute erste Aufgaben:

- CLI-Projektstruktur anlegen
- Ordner rekursiv scannen
- Dateiindex als JSON/SQLite speichern
- Bildmetadaten extrahieren
- Audio-Metadaten extrahieren
- einfache Suchfunktion bauen
- Thumbnail-Export für Bilder
- HTML- oder Markdown-Katalog generieren

## Datenschutz / Lizenzhinweis

Auch wenn Assets gekauft und frei nutzbar sind, muss die genaue Lizenz pro Bundle oder Pack nachvollziehbar bleiben.

Jeder Asset-Eintrag sollte langfristig eine Quelle oder Lizenzreferenz besitzen.

## MVP Scope

Für einen ersten Prototyp reicht:

- rekursiver Scan eines Asset-Ordners
- Hash pro Datei
- technische Basis-Metadaten
- JSON- oder SQLite-Ausgabe
- einfache Suche nach Dateiname/Extension/Tags
- manuelle Notiz-/Status-Ergänzung

Nicht nötig im ersten Schritt:

- perfekte automatische Inhaltserkennung
- KI-Bildanalyse
- KI-Audioanalyse
- eigenes großes UI
- automatische Sprite-Sheet-Zerlegung

## Akzeptanzkriterien für einen ersten Asset-Index-Prototyp

- Asset-Ordner kann rekursiv gescannt werden.
- Jede Datei bekommt eine stabile ID oder einen Hash.
- Der Index speichert Pfad, Typ, Größe und Extension.
- Bilder erhalten Breite/Höhe.
- Audiofiles erhalten Dauer, wenn technisch machbar.
- Dateiname und Pfad erzeugen erste heuristische Tags.
- Ergebnisse können durchsucht oder als Bericht ausgegeben werden.

## Offene Fragen

- Soll der Asset-Index im Night-Shift-City-Repo liegen oder in einem eigenen Tool-Repo?
- Wie groß ist die Asset-Sammlung ungefähr?
- Welche Dateiformate kommen hauptsächlich vor?
- Sind Lizenztexte/Quellenordner noch vorhanden?
- Soll das Tool projektagnostisch für andere Spiele nutzbar sein?
- Reicht ein CLI oder wäre später ein kleines Browser-UI sinnvoll?
