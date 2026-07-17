# MEILENSTEIN – Elternratgeber

Eine installierbare Progressive Web App (PWA) mit Entwicklungsphasen von der Geburt bis zur Pubertät, einer Volltextsuche nach Verhaltensweisen und einer Erste-Hilfe-Übersicht nach Altersstufe.

## Features

- **Entwicklungsphasen (0–16 Jahre):** 12 Altersstufen mit Körper/Motorik, Sprache/Denken, Verhalten/Gefühle sowie „Was du als Elternteil tun kannst“, navigierbar über ein "Wachstumslineal" am Bildschirmrand
- **Essen & Essverhalten:** altersabhängige Themen von Stillen/Beikost bis Jugendliche, inkl. typischer Essensmuster, praktischer Tipps, Strategien bei Essensablehnung und Lebensmitteln, die je Altersstufe vermieden werden sollten (mit Begründung) – filterbar nach Altersstufe
- **Stichwortsuche:** durchsucht Entwicklungsphasen, Essverhalten und Erste-Hilfe-Inhalte gleichzeitig (umlaut-tolerant), Treffer springen direkt zur passenden Stelle
- **Erste Hilfe nach Alter:** Sofortmaßnahmen zu Fieber, Verschlucken/Ersticken, Verbrennungen, Stürzen, Vergiftungen, Fieberkrampf, Bewusstlosigkeit u. a. – filterbar nach Säugling, Kleinkind, Kindergarten-, Schulkind und Jugendliche
- **Offline-fähig:** Service Worker cached alle Inhalte lokal, keine Datenübertragung an einen Server
- **Installierbar:** kann über den Browser als App auf Smartphone, Tablet oder Desktop installiert werden

## Struktur

```
meilenstein/
├── index.html      # komplette App (Markup, Styles, Daten, Logik)
├── manifest.json    # PWA-Manifest (Name, Icons, Theme-Farbe)
├── sw.js            # Service Worker für Offline-Nutzung
└── icon.svg         # App-Icon
```

Alle Inhalte (Entwicklungsphasen, Essverhalten, Erste-Hilfe-Daten) liegen als JavaScript-Objekte direkt in `index.html` im Abschnitt `PHASES`, `FOOD_TOPICS` bzw. `FIRST_AID` und lassen sich dort erweitern oder anpassen, ohne weitere Dateien zu berühren.

## Deployment (GitHub Pages)

1. Alle vier Dateien in ein GitHub-Repository hochladen (z. B. in den Ordner `docs/` oder direkt ins Root)
2. In den Repository-Einstellungen unter **Pages** die Quelle auf den entsprechenden Branch/Ordner setzen
3. Die App ist danach unter `https://<username>.github.io/<repo>/` erreichbar
4. Beim ersten Aufruf im Browser über "Zum Startbildschirm hinzufügen" bzw. das Installieren-Symbol in der Adressleiste installierbar

## Inhalte erweitern

- **Neue Altersphase:** in `PHASES` ein neues Objekt mit `id`, `ageLabel`, `ageRange`, `name`, `tag` und den vier Kategorien (inkl. „Was du als Elternteil tun kannst“) ergänzen
- **Neues Essen-Thema:** in `FOOD_TOPICS` ein Objekt mit `id`, `title`, `ages` (betroffene Altersgruppen aus `FOOD_AGE_GROUPS`, oder `general: true` für altersübergreifende Themen), `typical`, `tips`, optional `refusal` sowie optional `avoid` (Lebensmittel + Begründung, warum sie in diesem Alter vermieden werden sollten) ergänzen
- **Neue Erste-Hilfe-Situation:** in `FIRST_AID` ein Objekt mit `id`, `title`, `ages` (betroffene Altersgruppen), `steps` und `emergency` ergänzen
- Die Suche indiziert alle drei Datenquellen automatisch, keine zusätzliche Pflege nötig

## Hinweis

Die Erste-Hilfe-Rubrik ersetzt keinen Erste-Hilfe-Kurs am Kind/Säugling und keine ärztliche Behandlung. Im Zweifel immer zuerst den Notruf 112 wählen.
