# Location Ownership & Conversion System

## Ziel

Dieses System beschreibt, wie die Stadt als bestehendes, organisches Netzwerk von Locations aufgebaut ist, die vom Spieler entdeckt, bewertet, gekauft und in eigene Businesses umgewandelt werden können.

Das Ziel ist es, eine Welt zu erschaffen, die bereits existiert und nicht für den Spieler generiert wird – und in der der Spieler sich Schritt für Schritt seinen Platz erarbeitet.

## Design-Kernsatz

> Die Stadt gehört nicht dir. Du eignest sie dir langsam an.

## Grundidee

Jede Location in der Stadt existiert unabhängig vom Spieler.

Sie hat:

- eine aktuelle Nutzung
- eine Geschichte
- eine Lage
- eine Nachfrage
- eine Struktur

Der Spieler kann:

- Locations entdecken
- ihren Wert einschätzen
- sie kaufen oder übernehmen
- sie umbauen
- sie in eigene Businesses transformieren

## Spielerfantasie

- „Dieser Laden läuft schlecht… vielleicht kann ich da was draus machen.“
- „Die Lage ist perfekt, aber der Umbau wird teuer.“
- „Das war mal eine Bäckerei – eigentlich perfekt für meinen Imbiss.“
- „Wenn ich den Laden übernehme, verändert sich das Viertel.“

## Location als Kernobjekt

Eine Location ist ein generisches Objekt der Engine.

### Eigenschaften

```yaml
id: location_042
name: Old Thread Outfitters

district: lower_market

currentUsage: clothing_store

structure:
  size: medium
  hasKitchen: false
  hasBar: false
  hasStorage: true
  hasStage: false

locationTags:
  - street_level
  - commercial
  - medium_traffic

baseValue: 12000

conversionAffinity:
  food: medium
  bar: low
  retail: high
  service: medium
```

## Location-Zustände

Eine Location kann verschiedene Zustände haben:

- active_business (NPC betrieben)
- struggling_business
- closed
- abandoned
- for_sale
- owned_by_player

Diese Zustände können sich dynamisch ändern.

## Ownership System

Der Spieler kann Locations erwerben.

### Erwerbsarten

- Kauf (direkt)
- Übernahme (günstiger, wenn Business schlecht läuft)
- langfristig: Beteiligung, Miete, Kooperation

### Faktoren für Preis

- Lage
- Nachfrage
- Zustand des aktuellen Businesses
- Größe
- vorhandene Infrastruktur
- Ruf des Standorts

## Conversion System

Nach dem Erwerb kann der Spieler eine Location umwandeln.

## Design-Kernsatz Conversion

> Die Vergangenheit eines Ortes bestimmt, wie teuer seine Zukunft ist.

### Conversion-Logik

Kosten setzen sich zusammen aus:

```text
conversionCost = baseCost + structuralMismatch + missingFeatures - existingAdvantages
```

### Beispiele

#### Kleidungsladen → Bar

- keine Küche
- keine Barstruktur
- Layout ungeeignet

→ hohe Kosten

#### Bäckerei → Bar

- Küche vorhanden
- Grundstruktur passt teilweise

→ mittlere Kosten

#### alter Imbiss → Bar

- fast passende Struktur

→ geringe Kosten

## Struktur-basierte Logik

Locations besitzen Eigenschaften, die Umbauten beeinflussen:

- Größe
- Raumaufteilung
- vorhandene Infrastruktur
- technische Voraussetzungen

Diese beeinflussen:

- mögliche Business-Typen
- Umbaukosten
- Effizienz
- Atmosphäre

## District-Einfluss

Jede Location ist Teil eines Districts.

Districts beeinflussen:

- Nachfrage
- Kundentypen
- Tagesrhythmus
- Preisniveau

Beispiel:

- Industrial District → viele Arbeiter → Essen wichtig
- Nightlife District → Bars, Clubs
- Residential → ruhiger, stabil

## Dynamische Stadtentwicklung

Langfristig kann das System dazu führen, dass sich Stadtteile verändern:

- neue Businesses ziehen neue NPCs an
- alte Businesses verschwinden
- Nachfrage verschiebt sich
- Viertel verändern ihren Charakter

## Verbindung zum Business System

Location + Business = funktionierendes Gameplay

- Location bestimmt Nachfrage
- Business bestimmt Angebot
- NPC-System liefert Kunden

## Verbindung zur Exploration

Locations sind Exploration-Ziele.

Der Spieler entdeckt:

- neue Orte
- neue Möglichkeiten
- zukünftige Investitionen

## Langfristige Systeme

Mögliche Erweiterungen:

- mehrere Locations besitzen
- Franchise aufbauen
- Mitarbeiter einstellen
- District dominieren
- passive Einnahmen
- Konkurrenz durch NPC-Businesses

## Engine vs Game Layer

### Engine

- Location
- Ownership
- Conversion
- Struktur
- Preislogik

### Game Layer

- konkrete Shops (Bar, Imbiss, etc.)
- visuelle Gestaltung
- Story / Atmosphäre

## Wichtigste Regel

> Eine Location ist kein Slot. Sie ist ein Ort mit Vergangenheit.
