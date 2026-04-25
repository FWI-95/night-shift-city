# Future Direction – Absurdly Realistic Engine Sandboxes

## Warum dieses Dokument existiert

Dieses Dokument hält eine humorvolle, aber konzeptionell wichtige Zukunftsrichtung fest: Die Living-Sim-/Business-Engine könnte nicht nur ernsthafte cozy Sims wie Night Shift City tragen, sondern auch absurde, „viel zu realistische“ Spielideen.

Diese Ideen sind aktuell kein Umsetzungsziel. Sie dienen als späterer Experimentier- und Beweisraum für die Engine.

## Design-Kernsatz

> Peak Comedy entsteht, wenn eine absurde Prämisse mit tödlicher Ernsthaftigkeit simuliert wird.

## Grundgefühl

Die Engine kann banale oder übertriebene Situationen so ernst nehmen, dass daraus Humor entsteht.

Nicht durch Gags im klassischen Sinne, sondern durch Simulation:

- zu viel Weltlogik
- zu viele Systeme
- zu ernsthafte Konsequenzen
- zu realistische Wege zu eigentlich simplen Zielen
- normale Spielkonzepte, die vorher ein komplettes Alltagsleben verlangen

## Beispiel 1: Text Adventure mit absurdem Realismus

Klassisches Text-Adventure:

```text
> gehe nach Norden
Du siehst Wald.

> gehe weiter nach Norden
Noch mehr Wald.

> steige auf einen Baum und gucke nach Norden
Du siehst noch viel mehr Wald.
```

Die Pointe ist, dass die Welt nicht aus klaren Spielräumen besteht, sondern aus einer viel zu großen, viel zu banalen Realität.

### Engine-Relevanz

Auch ein absurd langweiliger Wald könnte dieselben Systeme nutzen:

- Locations
- Nachbarschaften
- Sichtlinien
- Bewegung
- Erschöpfung
- Orientierung
- Umgebungserkennung
- emergente Ereignisse

## Beispiel 2: Street Fighter, aber man muss sich erst finden

Prämisse:

Zwei Kämpfer wollen gegeneinander antreten, aber das eigentliche Spiel beginnt nicht sofort im Kampf.

Stattdessen müssen sie sich erst in einer Stadt finden:

- Adresse herausfinden
- U-Bahn nehmen
- falscher Stadtteil
- Verspätung
- Orientierung
- vielleicht erst jemanden fragen
- eventuell Hunger bekommen
- dann endlich kämpfen

Der eigentliche Kampf ist fast Nebensache. Die absurde Simulation des Wegs dahin ist der Witz.

### Engine-Relevanz

Dieses Beispiel nutzt dieselben Grundsysteme:

- Actors
- Locations
- Travel / Metro
- Time
- Need States
- World Knowledge
- Objectives
- Chance Events
- Meeting Logic

## Warum das für die Engine wichtig ist

Diese absurden Beispiele zeigen, dass die Engine nicht nur Night-Shift-City-spezifische Inhalte abbildet, sondern allgemein Situationen simulieren kann, in denen:

- Akteure Ziele haben
- Orte existieren
- Wege Zeit kosten
- Bedürfnisse stören
- Wissen unvollständig ist
- Systeme unerwartete Geschichten erzeugen

## Humor durch Systemübertreibung

Die Komik entsteht nicht dadurch, dass das Spiel Witze erzählt.

Sie entsteht dadurch, dass das Spiel Dinge simuliert, die normalerweise übersprungen werden.

Beispiele:

- Der Kampf beginnt nicht, weil beide Kämpfer dieselbe U-Bahn verpassen.
- Der Spieler findet den Gegner nicht, weil er nur „nördlich vom Kiosk“ gesagt bekommen hat.
- Im Text-Adventure gibt es keinen Dungeon, nur 47 Kilometer Wald.
- Ein NPC hat den finalen Bosskampf verpasst, weil er vorher noch Abendbrot kaufen wollte.

## Verhältnis zu Night Shift City

Night Shift City bleibt der Anker.

Diese Future-Ideen sind keine Ablenkung, sondern zeigen später mögliche Engine-Spielräume.

Night Shift City nutzt dieselben Kernsysteme ernsthaft:

- Stadtleben
- Business
- Routinen
- Exploration
- sanfte Progression

Absurdly Realistic Sandboxes könnten dieselben Systeme komödiantisch nutzen.

## Scope-Regel

Diese Ideen dürfen gesammelt werden, sollen aber nicht in den MVP von Night Shift City hineinlaufen.

Regel:

> Erst Night Shift City lebendig machen. Dann absurde Engine-Spielplätze bauen.

## Wichtigste Regel

> Wenn ein simples Spielziel durch realistische Umwege absurd kompliziert wird, ist das kein Bug – das ist ein Future Sandbox Feature.
