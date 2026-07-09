# 📝 Bettina Wiki

Ein portables, browser-basiertes Wiki mit **Autosave**, **Volltextsuche**, **Markdown-Editor** und **stickiger Formatierungsleiste**.
Läuft ohne Installation – einfach die HTML-Datei doppelklicken und loslegen.

Erstellt mit ♥ von **Elmar** für **Bettina** – [github.com/elmohuppi-stack/bettina-wiki](https://github.com/elmohuppi-stack/bettina-wiki)

## Features

- **Autosave** – Speichert automatisch 800 ms nach der letzten Eingabe, plus beim Verlassen der Seite
- **Markdown-Editor** – Geteilte Ansicht: links schreiben, rechts Live-Vorschau
- **Stickige Toolbar** – Formatierungs-Buttons bleiben beim Scrollen am oberen Rand fixiert
- **Volltextsuche** – Durchsucht alle Seiteninhalte und Titel mit Treffer-Hervorhebung
- **localStorage** – Alle Daten bleiben im Browser erhalten, auch nach dem Neuladen
- **Portabel** – Eine einzige HTML-Datei, keine Installation, kein Server
- **Export/Import** – Einzelne Seiten als `.md`-Datei, alle Seiten in einen Ordner (File System API) oder als Einzel-Downloads
- **Tastaturkürzel** – `Strg+S` speichern, `Strg+B` für **fett**, `Strg+I` für _kursiv_, `Strg+K` für Link
- **Wiki-Links** – `[[Seitenname]]` erzeugt einen internen Link
- **Favicon** – Eigenes SVG-Favicon mit „B"
- **Hilfe-Artikel** – Beim ersten Start wird automatisch eine Hilfeseite mit Bedienungsanleitung angelegt
- **Responsive** – Funktioniert auf Desktop und Mobilgeräten

## Verwendung

1. **`index.html`** doppelklicken → öffnet im Browser
2. **Neue Seite** – Button `+ Neue Seite` in der Seitenleiste
3. **Bearbeiten** – ✏️-Button auf einer Seite oder Seitenlisten-Eintrag
4. **Suchen** – Suchfeld in der Seitenleiste (durchsucht Titel + Inhalt)
5. **Einstellungen** – ⚙-Button für Wiki-Titel, -Beschreibung, Version & Impressum

## Projektstruktur

```
bettina-wiki/
├── index.html      ← Die gesamte Wiki-App (HTML + CSS + JS inline)
└── README.md       ← Diese Datei
```

Alles steckt in einer einzigen Datei. Keine Abhängigkeiten, keine Build-Tools.

## Technische Details

| Komponente   | Beschreibung                                                                                                   |
| ------------ | -------------------------------------------------------------------------------------------------------------- |
| **Sprache**  | Vanilla JavaScript (kein Framework)                                                                            |
| **Speicher** | localStorage (ca. 5 MB Speicherplatz – ausreichend für 100+ Seiten)                                            |
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

- **📥 .md** auf einer Seite – lädt die Seite als `.md`-Datei herunter
- **📦 Alle exportieren (.zip)** – lädt alle Seiten als einzelne `.md`-Downloads (Chromium: nutzt stattdessen die Ordner-Funktion)
- **📁 In Ordner exportieren** – öffnet einen Dialog zum Auswählen eines Ordners (File System API, Chromium)
- **📂 .md importieren** – importiert eine oder mehrere `.md`-Dateien

## Lizenz

MIT – mach damit, was du willst.
