# Game Time & Calendar System

## Ziel

Das Game Time & Calendar System beschreibt, wie Zeit in Night Shift City und der langfristigen Living-Sim-/Business-Engine funktioniert.

Eine zentrale Entscheidung ist:

> Night Shift City darf nicht an reale Uhrzeit, reale Wochentage oder reale Kalenderdaten gebunden sein.

Das Spiel soll ein eigenes internes Zeitmodell besitzen. Der Fortschritt im Spiel hängt davon ab, was im Spiel passiert – nicht davon, wann der Spieler im echten Leben online ist.

## Design-Kernsatz

> Die Welt hat ihren eigenen Rhythmus. Nicht den Kalender des Spielers.

## Warum keine Live-Zeit?

Spiele wie Animal Crossing, Harvest Moon-ähnliche Life-Sims oder vergleichbare Cozy Games können stark mit Tageszeiten, Wochentagen oder Real-Life-Timern arbeiten.

Das kann atmosphärisch sein, erzeugt aber auch Probleme:

- Der Spieler muss zu bestimmten echten Uhrzeiten spielen.
- Inhalte können verpasst werden, weil man im echten Leben keine Zeit hatte.
- Bauzeiten fühlen sich wie Wartebarrieren an.
- Das Spiel kann Druck erzeugen, obwohl es cozy sein soll.
- Spieler mit unregelmäßigem Alltag werden benachteiligt.

Night Shift City soll diese Falle vermeiden.

## Grundregel

Alle relevanten Zeitmechaniken basieren auf Spielzeit, nicht auf Realzeit.

Nicht gewünscht:

- „Komm morgen in Echtzeit wieder.“
- „Dieser Laden ist nur montags real um 19 Uhr offen.“
- „Bauprojekt dauert 24 reale Stunden.“
- „Event verpasst, weil du nicht online warst.“

Gewünscht:

- Bauprojekt dauert 3 Spieltage.
- NPC arbeitet jeden Ingame-Werktag von 11:00 bis 19:00.
- Bar ist ingame freitags länger geöffnet.
- Der Spieler kann schlafen, warten, vorspulen oder andere Aktivitäten machen.
- Der Spielstand merkt sich den internen Kalender.

## Spielzeit statt Realzeit

Das Spiel besitzt einen eigenen Kalender.

Mögliche Elemente:

- Ingame-Uhrzeit
- Ingame-Wochentag
- Ingame-Tagnummer
- optionale Seasons / Perioden
- optionaler Monats- oder Kalendername

Beispiel:

```text
Day 12, Friday, 21:45
```

Diese Zeit kann unabhängig von der echten Uhr laufen.

## Zeitfortschritt

Zeit kann auf verschiedene Weise fortschreiten:

- während der Spieler läuft oder fährt
- während Jobs
- während Reisen per Metro
- während Arbeitsschichten
- während Schlafen
- während bewusster Warteaktionen
- während Zeitsprüngen zwischen Szenen

Wichtig: Zeitfortschritt soll spielerisch kontrollierbar bleiben.

## Schlafen und Warten

Der Spieler soll nicht real warten müssen.

Wenn ein Bauprojekt mehrere Spieltage dauert, kann der Spieler:

- Jobs machen
- erkunden
- mit NPCs interagieren
- andere Businesses verwalten
- schlafen
- warten
- Zeit vorspulen, falls das Design es erlaubt

## Construction Time mit Ingame-Zeit

Das Construction & Upgrade Time System nutzt ausschließlich Ingame-Zeit.

Beispiel:

```text
Day 3, Monday, 10:00: Umbau gestartet.
Day 6, Thursday, 18:00: Umbau abgeschlossen.
```

Das bedeutet nicht:

```text
Komm in 72 echten Stunden wieder.
```

## NPC-Routinen mit Ingame-Zeit

NPCs folgen dem internen Kalender.

Beispiel:

- Montag bis Freitag: Arbeitsschicht
- Freitagabend: höhere Bar-Wahrscheinlichkeit
- Sonntag: keine Arbeit, andere Aktivitäten

Diese Logik ist Teil der Spielsimulation, nicht der echten Woche.

## Events und Verfügbarkeit

Events dürfen an Ingame-Zeit gebunden sein, aber nicht an Realzeit.

Gut:

- „Jeden Ingame-Freitag ist die Bar voller.“
- „Nach 5 Spieltagen ist der Umbau fertig.“
- „Ein NPC kommt immer nach seiner Ingame-Schicht vorbei.“

Schlecht:

- „Nur echten Freitagabend verfügbar.“
- „Du musst morgen real wiederkommen.“
- „Event verpasst, weil du offline warst.“

## Cozy ohne FOMO

Night Shift City soll cozy sein, ohne Fear of Missing Out.

Der Spieler soll das Gefühl haben:

- Ich kann in meinem Tempo spielen.
- Ich verpasse nichts Wichtiges durch mein reales Leben.
- Die Stadt hat Rhythmus, aber keinen realen Termindruck.
- Ich kann planen, schlafen, warten oder weitermachen.

## Pausieren und Speichern

Die Spielzeit muss speicherbar und pausierbar sein.

Ein Spielstand enthält mindestens:

- aktuelle Ingame-Zeit
- aktueller Ingame-Tag
- Wochentag
- laufende Bauprojekte
- NPC-Zustände oder rekonstruierbare Simulationsdaten
- Business-Zustände

Wenn der Spieler das Spiel beendet, läuft die Simulation nicht in Realzeit weiter, außer diese Entscheidung wird später explizit getroffen. Standard ist: Spielzeit pausiert mit dem Spiel.

## Optional: Offline-Fortschritt als spätere Frage

Falls später jemals Offline-Fortschritt gewünscht wird, muss er sehr vorsichtig behandelt werden.

Default:

> Kein automatischer Realzeit-Fortschritt.

Falls überhaupt, dann nur optional und begrenzt, z. B. für sehr abstrakte passive Systeme. Aber das ist kein aktuelles Ziel.

## Generische Engine-Sicht

Die Engine sollte ein internes Zeitmodell bereitstellen:

- GameClock
- Calendar
- DayCycle
- WeekCycle
- TimeScale
- Scheduled Events
- Time Advance
- Sleep / Wait Actions

Die Engine darf nicht davon ausgehen, dass echte Systemzeit relevant ist.

Systemzeit kann höchstens für technische Zwecke genutzt werden:

- Savegame-Timestamp
- Logs
- Debugging

Aber niemals als Gameplay-Quelle für Kernsysteme.

## Verbindung zu anderen Systemen

### NPC Routine System

NPCs nutzen Ingame-Wochentage, Zeitfenster und Aktivitätsdauer.

### Business System

Businesses nutzen Ingame-Öffnungszeiten, Nachfragewellen und Tagesabschlüsse.

### Construction & Upgrade Time System

Bauprojekte dauern Ingame-Zeit.

### Exploration System

Reisen und Erkunden verbrauchen Ingame-Zeit und können dadurch Stadtmuster sichtbar machen.

### Progression System

Progression hängt an Spielhandlungen und Ingame-Zeit, nicht an Real-Life-Login-Frequenz.

## Beispiel-Debug-Ausgabe

```text
[GameTime] Day 4, Wednesday, 08:00
[Schedule] Jaro Klein leaves home for breakfast.
[Business] Blue Hour Noodles opens at 18:00.
[Construction] Neon Kettle renovation: 2 days remaining.
[Sleep] Player sleeps until Day 5, Thursday, 07:30.
[Construction] Neon Kettle renovation: 1 day remaining.
```

## Anti-Patterns

Vermeiden:

- Real-Life-Wartezeiten für Bauprojekte
- echte Wochenkalender als Gameplay-Gate
- Events, die der Spieler durch Offline-Sein verpasst
- Login-Pflicht
- Mobile-Game-Timer
- tägliche Belohnungen als Druckmechanik
- Systemzeit als Quelle für NPC-Routinen

## Offene Fragen

- Wie lang ist ein Ingame-Tag in realer Spielzeit?
- Gibt es Zeitbeschleunigung?
- Kann der Spieler jederzeit schlafen?
- Wie stark sollen NPC-Routinen während Zeitsprüngen simuliert werden?
- Gibt es Seasons oder nur Wochentage?
- Soll Zeit in Innenräumen anders laufen als draußen?
- Wie detailliert müssen laufende Systeme beim Schlafen berechnet werden?

## Wichtigste Regel

> Kein Spielsystem darf verlangen, dass der Spieler zu einer realen Uhrzeit oder an einem realen Tag online ist.
