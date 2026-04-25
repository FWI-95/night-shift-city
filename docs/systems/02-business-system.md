# Business System

## Ziel

Das Business System ist der sanfte Gameplay-Motor von Night Shift City.

Es soll dem Spieler Motivation, Progression und kleine Entscheidungen geben, ohne in Stress, Tycoon-Zwang oder Optimierungsdruck abzurutschen. Der Spieler betreibt und entwickelt lokale Businesses, während er gleichzeitig die Stadt erkundet, NPCs beobachtet und Zusammenhänge entdeckt.

Das System soll bewusst zweischichtig gedacht werden:

1. **Generische Business-Engine** – wiederverwendbare Logik für Businesses, Nachfrage, Kunden, Öffnungszeiten, Bekanntheit und kleine Aktionen.
2. **Night-Shift-City-Game-Layer** – konkrete Cyberpunk-Businesses wie Bar, Essensstand, Lieferdienst, Taxi-Service oder kleiner Shop.

## Design-Kernsatz

> Business ist Motor, nicht Zwang.

Das Business soll den Spieler in Bewegung bringen, aber ihn nicht hetzen.

## Spielerfantasie

Der Spieler soll das Gefühl haben:

- Ich baue mir in dieser Stadt langsam etwas Eigenes auf.
- Mein Laden ist ein Ort, an dem Leben passiert.
- Stammkunden, Stadtteile und Routinen beeinflussen mein Business.
- Wenn ich die Stadt verstehe, kann ich bessere Entscheidungen treffen.
- Ich muss nicht dauernd optimieren, aber kleine Eingriffe lohnen sich.

Nicht das Ziel:

- maximaler Profit pro Minute
- Excel-Tycoon
- globale Mega-Corp-Verwaltung
- permanentes Feuerlöschen

## Beziehung zur Exploration

Das Business System soll Exploration belohnen.

Der Spieler erkundet nicht nur, um neue Orte zu sehen, sondern um Zusammenhänge zu verstehen:

- Wo laufen viele Arbeiter nach Feierabend entlang?
- Welcher Stadtteil hat Nachtleben?
- Wo lohnt sich Werbung?
- Welche NPC-Typen brauchen welche Angebote?
- Welche Öffnungszeiten passen zu welchen Routinen?

Exploration speist das Business. Das Business motiviert Exploration.

## Generische Business-Engine

Die generische Engine sollte folgende Konzepte kennen:

- Business
- Location
- Customer / Actor
- Demand
- Awareness
- Offer
- Opening Hours
- Visit Decision
- Revenue
- Cost
- Upgrade / Improvement
- Micro Action

Sie sollte möglichst keine Cyberpunk-spezifischen Begriffe hardcoden.

### Business

Ein Business ist eine betreibbare wirtschaftliche Einheit.

Generische Eigenschaften:

- ID
- Name
- Business Type
- Location
- Owner
- Opening Hours
- Offers
- Awareness by District
- Reputation
- Customer Tags
- Operating Costs
- Revenue Rules
- Upgrade Slots
- Status

Beispiel:

```yaml
id: lower_market_bar_01
name: Neon Kettle
businessType: bar
location: lower_market.side_street_03
owner: player
openingHours:
  monday-thursday: "18:00-02:00"
  friday-saturday: "18:00-04:00"
  sunday: "closed"
offers:
  - cheap_beer
  - synth_snacks
  - noodle_bowl
awareness:
  lower_market: 35
  harbor_blocks: 12
reputation: 18
status: open
```

### Business Type

Der Business Type beschreibt grundlegende Regeln, nicht konkrete Story.

Beispiele generisch:

- food_stand
- bar
- restaurant
- taxi_service
- delivery_service
- shop
- service_provider

Night Shift City kann daraus konkrete Varianten machen:

- Nudelstand
- After-Work-Bar
- Metro-Kiosk
- Courier Office
- Night Taxi

### Location

Der Standort ist entscheidend. Er verbindet Business, NPC-Routinen und Exploration.

Wichtige Standortwerte:

- District
- Tags
- Foot Traffic
- Nearby Locations
- Rent / Cost
- Visibility
- Time-of-Day Demand
- Customer Archetypes

Beispiel-Tags:

- `industrial`
- `nightlife`
- `residential`
- `metro_hub`
- `back_alley`
- `market`

## Nachfrage / Demand

Demand beschreibt, wie attraktiv ein Business zu einem bestimmten Zeitpunkt für bestimmte Kundentypen ist.

Demand entsteht aus:

- Standort
- Tageszeit
- Wochentag
- NPC-Routinen
- Bedürfnissen
- Angebot
- Preisniveau
- Awareness
- Reputation
- Wetter / Events
- Öffnungszeiten

Beispiel:

```text
Industrial District, 19:00
→ viele Arbeiter beenden Schicht
→ Hunger hoch
→ günstiges Essen attraktiv
→ food_stand demand steigt
```

## Awareness / Bekanntheit

Awareness beschreibt, wie bekannt ein Business in einem Stadtteil oder bei bestimmten Gruppen ist.

Sie ist kein globaler Wert, sondern lokal.

Beispiel:

```yaml
awareness:
  lower_market: 55
  harbor_blocks: 22
  neon_residential: 8
```

Dadurch wird Werbung in anderen Stadtteilen sinnvoll.

### Designziel

Awareness soll Exploration und Micro Actions verbinden:

- Spieler besucht anderen Stadtteil
- macht dort Werbung
- Awareness steigt dort temporär oder dauerhaft leicht
- einige NPCs aus diesem Stadtteil besuchen später das Business

## Reputation

Reputation beschreibt, wie gut das Business wahrgenommen wird.

Mögliche Faktoren:

- Preis-Leistung
- Bedienqualität
- Angebot passend zur Zielgruppe
- Stammkunden
- Sauberkeit / Stimmung
- Öffnungszeiten
- besondere Ereignisse

Für den Anfang kann Reputation ein einfacher Wert sein.

Später kann sie nach Gruppen oder Stadtteilen getrennt werden.

## Offer / Angebot

Offers sind das, was ein Business anbietet.

Generisch:

```yaml
id: cheap_noodle_bowl
category: food
price: 8
satisfies:
  hunger: 35
tags:
  - cheap
  - warm_food
  - worker_friendly
```

Night Shift City spezifisch:

- Synth-Nudeln
- Billigbier
- Soy-Coffee
- Metro Snack Pack
- Midnight Ramen

## Customer Visit Decision

NPCs sollen nicht zufällig erscheinen, sondern plausibel entscheiden.

Eine einfache Entscheidung kann auf Scores basieren:

```text
visitScore = needMatch + locationConvenience + awareness + reputation + scheduleFit - priceMismatch
```

Für MVP reicht eine einfache gewichtete Auswahl.

Beispiel:

- NPC hat Hunger
- ist in der Nähe
- kennt den Laden
- Laden ist offen
- Angebot passt zum Geldbeutel
- Wahrscheinlichkeit für Besuch steigt

## Stammkunden

Stammkunden sind besonders wichtig für das Spielgefühl.

Sie verbinden NPC-System und Business-System.

Ein NPC kann Stammkunde werden, wenn:

- er das Business mehrfach besucht
- Angebot zu seinen Traits passt
- Öffnungszeiten zu seiner Routine passen
- Reputation hoch genug ist

Stammkunden erzeugen Wiedererkennung:

> „Ah, der kommt immer nach der Spätschicht.“

## Soft Pressure

Das Business System soll sanften Druck erzeugen, aber keinen harten Stress.

### Nicht gewünscht

- Sofortige Pleite durch einen schlechten Tag
- aggressive Timer
- permanenter Optimierungszwang
- ständig kaputte Systeme

### Gewünscht

- leichte Betriebskosten
- langsam sinkende Bekanntheit ohne Aktivität
- verpasste Chancen statt harte Strafen
- stagnierendes Wachstum statt Game Over
- freiwillige Optimierung

## Stabilitätszustände

Ein Business kann verschiedene Zustände haben:

### Struggling

- geringe Einnahmen
- wenig Kunden
- möglicherweise falscher Standort oder Angebot
- kein sofortiges Scheitern

### Stable

- deckt Kosten
- regelmäßige Kunden
- Spieler kann erkunden

### Growing

- steigende Bekanntheit
- mehr Stammkunden
- neue Optionen werden interessant

### Busy

- viel Nachfrage
- mögliche Engpässe
- später relevant für Mitarbeiter oder Ausbau

## Micro Actions im Business-Kontext

Micro Actions sind kleine, schnell verständliche Eingriffe.

Beispiele:

### Werbung machen

- Ort: anderer Stadtteil
- Effekt: Awareness steigt lokal
- Risiko: kostet Zeit/Geld
- Druck: optional

### Öffnungszeiten ändern

- Effekt: andere NPC-Routinen werden erreichbar
- Beispiel: später öffnen zieht Nachtarbeiter an

### Angebot anpassen

- Effekt: bestimmte Kundentypen werden stärker angesprochen
- Beispiel: günstiges Essen für Arbeiter, teurere Drinks für Nachtleben

### Standort scouten

- Effekt: Spieler erkennt Nachfrageprofile
- Kann später Standortentscheidungen verbessern

### Atmosphäre verbessern

- Licht, Musik, Deko
- Effekt: Zielgruppen und Aufenthaltsdauer ändern sich

## Night-Shift-City-spezifischer Game Layer

Im konkreten Spiel sollen Businesses persönlich und lokal wirken.

Mögliche erste Business-Fantasien:

### Essensstand

Guter MVP-Kandidat.

- einfache Angebote
- klare Nachfrage durch Hunger
- Arbeiter, Pendler, Nachtmenschen als Kunden
- leicht verständliche Standortlogik

### Bar

Atmosphärisch sehr stark.

- Stammkunden
- Gesprächsfetzen
- längere Aufenthaltsdauer
- Nachtleben
- stärkere NPC-Immersion

### Lieferdienst

Gut für Bewegung durch die Stadt.

- verbindet Exploration mit Einkommen
- kann später Business-Vorläufer sein
- einfache Missionen ohne Story-Zwang

### Taxi-Service

Interessant für Stadtkenntnis und Routinen.

- NPCs wollen von A nach B
- Metro und Stadtteile werden relevant
- spätere Erweiterung, nicht MVP 0

## MVP-Vorschlag

Für den ersten Business-Prototyp sollte nur ein Business-Typ umgesetzt werden.

Empfehlung:

> Food Stand oder kleine Bar.

### Warum Food Stand?

- einfaches Bedürfnis: Hunger
- kurze Aufenthalte
- klare Nachfrage
- niedrige Komplexität

### Warum Bar?

- stärkeres Night-Shift-City-Gefühl
- Gesprächsfetzen und Stammkunden passen besser
- längere Aufenthalte machen NPCs beobachtbarer

### Empfehlung für MVP 2

Start mit einem hybriden kleinen Ort:

> ein kleiner Nacht-Imbiss mit Bar-Charakter.

Er kann Essen verkaufen, aber NPCs können auch kurz verweilen. Dadurch bleiben Mechaniken einfach, aber Atmosphäre entsteht.

## MVP 2 Scope

Benötigt:

- Business-Datenmodell
- ein Business-Typ
- Öffnungszeiten
- einfache Offers
- lokale Awareness
- einfache Customer Visit Decision
- Einnahmen
- Betriebskosten
- Debug-Ausgabe

Nicht benötigt:

- Mitarbeiter
- Inventarsystem
- komplexe Preise
- Lieferketten
- Ausbau-Bäume
- mehrere Businesses
- vollständiges UI

## Beispiel für MVP-Business

```yaml
id: night_kiosk_01
name: Blue Hour Noodles
businessType: food_bar_hybrid
location: lower_market.metro_exit_east
owner: player
openingHours:
  monday-sunday: "18:00-02:00"
offers:
  - midnight_noodles
  - synth_coffee
  - cheap_beer
awareness:
  lower_market: 25
reputation: 10
operatingCosts:
  daily: 40
```

## Debug-Ausgabe für MVP

Beispiel:

```text
18:00 Blue Hour Noodles opens.
18:20 Jaro Klein considers Blue Hour Noodles: hunger=72, awareness=25, distance=near, score=68 -> visits.
18:25 Jaro Klein buys midnight_noodles for 8 credits.
19:10 Riko Malden considers Blue Hour Noodles: stress=62, wants_bar=true, score=45 -> visits.
02:00 Blue Hour Noodles closes. Revenue: 96, Costs: 40, Profit: 56.
```

## Generische Wiederverwendbarkeit

Das System soll später auch andere Settings tragen können.

Beispiel: Tankstellen-Sim

```yaml
businessType: gas_station
location: roadside_exit_12
offers:
  - regular_fuel
  - coffee
  - sandwich
awareness:
  highway: 35
customerTags:
  - commuter
  - truck_driver
  - local_regular
```

Die Engine muss dafür nicht wissen, was eine Cyberpunk-Bar oder Tankstelle ist. Sie verarbeitet Business, Offer, Demand, Awareness und Customer Decisions.

## Offene Fragen

- Starten wir mit Food Stand, Bar oder Hybrid?
- Wie stark soll Geld im MVP eine Rolle spielen?
- Soll der Spieler aktiv bedienen oder nur verwalten?
- Wie sichtbar sollen Kundenentscheidungen im UI sein?
- Wie lange bleibt Werbung wirksam?
- Sollen Betriebskosten täglich, pro Öffnung oder abstrakt berechnet werden?
- Ab wann wird ein NPC Stammkunde?
- Können Businesses auch geschlossen bleiben, ohne sofort hart bestraft zu werden?

## Wichtigste Regel

> Ein Business ist nicht nur eine Einnahmequelle. Es ist ein Ort, an dem Stadtleben sichtbar wird.
