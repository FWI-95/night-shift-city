# Immersion over Graphics – Design Philosophy

## Warum dieses Dokument existiert

Dieses Dokument hält eine zentrale Priorität für Night Shift City und die langfristige Living-Sim-/Business-Engine fest:

> Immersives Gameplay ist wichtiger als grafische Perfektion.

Night Shift City soll nicht versuchen, durch High-End-Grafik zu beeindrucken. Das Projekt soll durch Spielgefühl, Systeme, Atmosphäre, Wiedererkennbarkeit, Weltlogik und emergente Geschichten tragen.

## Design-Kernsatz

> Scheiß auf Grafik. Immersive Gameplay ist, was wir wollen.

Dieser Satz ist bewusst direkt formuliert, weil er eine wichtige Schutzfunktion hat: Er verhindert, dass das Projekt zu früh in Rendering, Polishing, Shader, Asset-Perfektion oder optische Vergleichbarkeit mit AAA-Spielen abdriftet.

## Inspirationsgedanke

Viele Spiele bleiben nicht wegen ihrer technischen Grafik im Kopf, sondern wegen ihres Spielgefühls, ihrer Systeme oder ihrer Atmosphäre.

Beispiele für diese Art von Priorität:

- Minecraft: einfache Optik, extrem starke Freiheit und Systemik
- RimWorld: reduzierte Darstellung, aber tiefe emergente Geschichten
- Dwarf Fortress: ursprünglich extrem reduzierte ASCII-/Konsolen-Darstellung, aber darunter eine absurd tiefe Welt-, Figuren- und Ereignissimulation
- ältere Need-for-Speed-Spiele wie Most Wanted oder Underground: starkes Gefühl, klare Identität, erinnerbare Atmosphäre
- viele alte Spiele allgemein: technische Begrenzung, aber starkes Gameplay und starke Immersion

Diese Beispiele sind keine direkten Designvorlagen, sondern Belege für eine Haltung:

> Grafik altert. Spielgefühl bleibt.

## Dwarf-Fortress-Lektion

Dwarf Fortress ist als Referenz besonders wichtig, weil es zeigt, dass Immersion nicht aus Darstellungstiefe entstehen muss, sondern aus Simulations- und Bedeutungstiefe.

Ein Spiel kann visuell extrem reduziert sein und trotzdem eine Welt erzeugen, über die Spieler Geschichten erzählen, weil darunter Systeme arbeiten:

- Figuren mit Bedürfnissen, Zuständen und Geschichten
- Orte mit Funktion
- Ereignisse mit Folgen
- emergente Katastrophen
- nachvollziehbare Kausalität
- Spieler, die aus Simulation Geschichten rekonstruieren

Für Night Shift City bedeutet das:

> Wenn die Stadt als Simulation lebt, kann auch eine einfache Darstellung stark immersiv sein.

Die frühe Version darf daher sogar eher wie ein Debug-/Konsolenprogramm wirken, solange sie zeigt, dass die Systeme atmen.

## Was Immersion hier bedeutet

Immersion bedeutet für Night Shift City nicht fotorealistische Darstellung.

Immersion bedeutet:

- Die Stadt wirkt, als würde sie auch ohne den Spieler existieren.
- NPCs haben glaubwürdige Routinen.
- Orte haben Funktion, Geschichte und Rhythmus.
- Der Spieler versteht durch Beobachtung, wie die Welt funktioniert.
- Business-Entscheidungen fühlen sich in der Welt verankert an.
- Rückschläge sind Teil des Lebens, nicht das Ende des Spiels.
- Kleine Details erzeugen Wiedererkennung.
- Systeme greifen ineinander und erzeugen Geschichten.

## Prioritätenreihenfolge

Wenn Zeit, Energie oder technische Kapazität knapp sind, gilt:

1. Spielgefühl
2. Systemklarheit
3. Beobachtbarkeit
4. Datengetriebene Erweiterbarkeit
5. Debugbarkeit
6. Atmosphäre
7. Lesbare, einfache Darstellung
8. Visuelles Polishing
9. Grafische Effekte

Grafik ist nicht unwichtig. Sie soll Atmosphäre unterstützen. Aber sie darf niemals der Haupttreiber des Projekts werden.

## Was zuerst funktionieren muss

Bevor visuelles Polishing wichtig wird, müssen diese Dinge funktionieren:

- NPCs können ihren Tag als Simulation durchleben.
- Locations haben Bedeutung.
- Businesses ziehen plausibel Kunden an.
- Der Spieler kann einfache Jobs erledigen.
- Progression erweitert Möglichkeiten, ohne alte Aktivitäten abzuschneiden.
- Debug-Ausgaben erklären, warum etwas passiert.
- Content kann datengetrieben ergänzt werden.

## Welche Darstellung ausreicht

Für frühe Versionen reicht eine einfache Darstellung:

- Debug-Text
- einfache Konsolen-/Textsimulation
- einfache 2D-/Top-Down-Ansicht
- simple Icons
- Platzhalter-Sprites
- reduzierte Animationen
- klare UI-Informationen

Die Darstellung muss verständlich und atmosphärisch genug sein, aber nicht beeindruckend.

## Night Shift City als Showcase

Night Shift City kann langfristig eine Art Showcase für die Engine werden.

Nicht im Sinne von maximaler grafischer Präsentation, sondern im Sinne von:

- zeigt, wie viele Systeme ineinandergreifen können
- zeigt, wie eine Stadt über Routinen lebendig wirkt
- zeigt, wie Business, NPCs, Locations und Exploration ein gemeinsames Spielgefühl erzeugen
- zeigt, dass eine kleine eigene Engine mehrere Ideen tragen kann

In diesem Sinne kann Night Shift City irgendwann ein großer Demonstrator dafür werden, was die Engine kann.

## Verhältnis zur Engine-Vision

Die langfristige Engine soll möglichst viele der eigenen Gedankenblitze tragfähig machen.

Das bedeutet nicht, dass die Engine alles kann. Sie soll aber die wiederkehrenden Kernideen unterstützen:

- lebendige Orte
- wiederkehrende NPCs
- Routinen
- kleine Businesses
- sanfte Progression
- Exploration
- emergente Geschichten
- datengetriebene Content-Packs

Night Shift City ist der Einstiegspunkt und erste große Beweisfall.

## Schutz vor Scope-Fallen

Diese Philosophie schützt vor typischen Fallen:

- zu früh ein Renderingsystem perfektionieren
- zu lange nach passenden Assets suchen
- Features an AAA-Optik messen
- Animationen vor Systemen priorisieren
- technische Grafikprobleme als Kernblocker behandeln
- die Engine zu breit bauen, bevor sie Spielgefühl erzeugt

## Gute Fragen bei Entscheidungen

Bei neuen Ideen, Features oder technischen Aufgaben sollte gefragt werden:

1. Erhöht das Immersion oder nur Optik?
2. Macht es die Welt glaubwürdiger?
3. Erzeugt es beobachtbares Verhalten?
4. Hilft es dem Spieler, Zusammenhänge zu verstehen?
5. Unterstützt es die Engine langfristig?
6. Kann es mit einfachen Mitteln getestet werden?
7. Ist es jetzt wichtig oder späteres Polishing?

## Nicht falsch verstehen

Grafik darf schön sein.

Night Shift City soll atmosphärisch wirken:

- Neon
- Regen
- Nacht
- Metro
- enge Straßen
- kleine Läden
- überfüllte Stadt
- melancholischer Cozy-Cyberpunk

Aber diese Atmosphäre darf aus einfachen Mitteln entstehen:

- Lichtstimmung
- Sound
- Wiedererkennung
- UI
- Text
- Routinen
- Orte
- kleine Animationen

Nicht aus High-End-Rendering als Voraussetzung.

## Wichtigste Regeln

> Grafik unterstützt Immersion. Sie ersetzt sie nicht.

> Systeme zuerst. Polishing später.

> Eine lebendige Debug-Simulation ist wertvoller als eine schöne leere Stadt.

> Night Shift City soll zeigen, was die Engine fühlen lassen kann, nicht wie teuer sie aussieht.
