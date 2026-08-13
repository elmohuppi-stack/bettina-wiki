# 📝 Bettina Wiki

Ein portables, browser-basiertes Wiki mit **Autosave**, **Volltextsuche**, **Markdown-Editor** und **stickiger Formatierungsleiste**.
Läuft ohne Installation – einfach die HTML-Datei doppelklicken und loslegen.

Erstellt mit ♥ von **Elmar** für **Bettina** – [github.com/elmohuppi-stack/bettina-wiki](https://github.com/elmohuppi-stack/bettina-wiki)

## Features

- **Autosave** – Speichert automatisch 800 ms nach der letzten Eingabe, plus beim Verlassen der Seite
- **Markdown-Editor** – Geteilte Ansicht: links schreiben, rechts Live-Vorschau
- **Stickige Toolbar** – Formatierungs-Buttons bleiben beim Scrollen am oberen Rand fixiert
- **Volltextsuche** – Durchsucht alle Seiteninhalte und Titel mit Treffer-Hervorhebung
- **Datei-Speicher** – Alle Daten in einer echten Datei `wiki-data.json` samt täglicher Sicherung (siehe [Datenspeicherung](#datenspeicherung))
- **Portabel** – Eine einzige HTML-Datei, keine Installation, kein Server
- **Export/Import** – Vollständige Sicherung als `.json`, einzelne Seiten als `.md`-Datei, alle Seiten in einen Ordner (File System API) oder als Einzel-Downloads
- **Tastaturkürzel** – `Strg+S` speichern, `Strg+B` für **fett**, `Strg+I` für _kursiv_, `Strg+K` für Link
- **Wiki-Links** – `[[Seitenname]]` erzeugt einen internen Link
- **Favicon** – Eigenes SVG-Favicon mit „B"
- **Hilfe-Artikel** – Beim ersten Start wird automatisch eine Hilfeseite mit Bedienungsanleitung angelegt
- **Responsive** – Funktioniert auf Desktop und Mobilgeräten

## Verwendung

1. **`index.html`** doppelklicken → öffnet im Browser
2. **Datenordner verbinden** – ⚙ Einstellungen → `📁 Datenordner wählen` (einmalig, siehe unten)
3. **Neue Seite** – Button `+ Neue Seite` in der Seitenleiste
4. **Bearbeiten** – ✏️-Button auf einer Seite oder Seitenlisten-Eintrag
5. **Suchen** – Suchfeld in der Seitenleiste (durchsucht Titel + Inhalt)
6. **Einstellungen** – ⚙-Button für Wiki-Titel, -Beschreibung, Speicherort, Export & Impressum

## Datenspeicherung

Die Logik steckt in `index.html`, die **Daten liegen in einer eigenen Datei**.
Beim ersten Start ist noch kein Datenordner verbunden – ein Banner weist darauf hin.
Über ⚙ → `📁 Datenordner wählen` einen Ordner auswählen, danach schreibt das Wiki
bei jeder Änderung dorthin:

```
<gewählter Ordner>/
├── wiki-data.json              ← alle Seiten + Einstellungen
└── backups/
    ├── wiki-2026-08-13.json    ← automatische Tagessicherung (letzte 14)
    └── vor-ueberschreiben-…    ← Sicherheitskopie vor einem Stand-Wechsel
```

**Warum nicht nur der Browser-Speicher?**
`localStorage` hängt an der Browser-Origin. Bei `file://` reicht schon ein anderer
Pfad oder Laufwerksbuchstabe, ein zurückgesetztes Windows-Profil (typisch bei
Remote-Desktop / VDI) oder ein „Browserdaten löschen“, und alle Seiten sind weg.
Eine echte Datei übersteht das – und lässt sich sichern, kopieren und in einen
Cloud-Ordner legen.

Empfehlung: einen Ordner in **OneDrive/Dropbox** wählen. Dann gibt es zusätzlich
Versionierung und eine Kopie außerhalb des Rechners.

**Wie es zusammenspielt**

- Der Browser-Speicher läuft als schneller Zwischenspeicher weiter – die Datei ist maßgeblich.
- Beim Start werden beide Stände verglichen; der neuere gewinnt.
- Hätte der Browser-Stand *weniger* Seiten als die Datei, wird nachgefragt statt überschrieben – und der bisherige Dateistand vorher nach `backups/` gesichert.
- Nach einem Browser-Neustart fragt der Browser einmal nach der Ordner-Freigabe. Ein Klick auf **Jetzt freigeben** genügt; bis dahin läuft das Wiki aus dem Browser-Speicher weiter.
- Der Punkt links unten in der Seitenleiste zeigt den Status: 🟢 Datei-Speicher aktiv, 🟡 nur Browser-Speicher.

**Firefox / Safari** unterstützen die File System Access API nicht. Dort läuft das
Wiki weiter aus dem Browser-Speicher und warnt sichtbar – hier bitte regelmäßig
`💾 Vollständige Sicherung (.json)` nutzen oder Edge/Chrome verwenden.

## Projektstruktur

```
bettina-wiki/
├── index.html      ← Die gesamte Wiki-App (HTML + CSS + JS inline)
└── README.md       ← Diese Datei
```

Die App selbst steckt in einer einzigen Datei. Keine Abhängigkeiten, keine Build-Tools.
Die Nutzdaten liegen getrennt davon im gewählten Datenordner.

## Technische Details

| Komponente   | Beschreibung                                                                                                   |
| ------------ | -------------------------------------------------------------------------------------------------------------- |
| **Sprache**  | Vanilla JavaScript (kein Framework)                                                                            |
| **Speicher** | `wiki-data.json` im gewählten Ordner (File System Access API) + localStorage als Cache/Fallback                 |
| **Markdown** | Eigener Parser (unterstützt: Überschriften, Bold/Italic, Links, Bilder, Listen, Blockquotes, Code, Wiki-Links) |
| **Größe**    | ~35 KB (unminifiziert)                                                                                         |
| **Browser**  | Chrome, Firefox, Edge, Safari – alle modernen Browser                                                          |
| **Export**   | File System Access API (Chromium) + Fallback auf Downloads                                                     |

### Markdown-Syntax (unterstützt)

````markdown
# Überschrift 1

## Überschrift 2

**fetter Text** und _kursiver Text_

- Ungeordnete Liste
- Noch ein Punkt

1. Erster Punkt
2. Zweiter Punkt

[Link](https://example.com)
![Bild](bild.jpg)

> Zitat

`inline code`

```js
code block
```

[[Interner Link]] → verlinkt auf eine andere Wiki-Seite
[[Text|seite]] → Link mit anderem Anzeigetext
````

## Exportieren

Die Export-Funktionen findest du in den **Einstellungen** (⚙):

- **💾 Vollständige Sicherung (.json)** – alle Seiten *und* Einstellungen in einer Datei; funktioniert in jedem Browser
- **♻️ Sicherung wiederherstellen** – liest eine solche `.json` wieder ein (mit Rückfrage)
- **📥 .md** auf einer Seite – lädt die Seite als `.md`-Datei herunter
- **📦 Alle exportieren (.md)** – lädt alle Seiten als einzelne `.md`-Downloads (Chromium: nutzt stattdessen die Ordner-Funktion)
- **📁 In Ordner exportieren** – öffnet einen Dialog zum Auswählen eines Ordners (File System API, Chromium)
- **📂 .md importieren** – importiert eine oder mehrere `.md`-Dateien

Die `backups/`-Dateien im Datenordner haben dasselbe Format wie die vollständige
Sicherung – eine davon lässt sich über **♻️ Sicherung wiederherstellen** direkt einlesen.

## Lizenz

MIT – mach damit, was du willst.
