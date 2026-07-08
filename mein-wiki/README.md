# 📝 Mein Wiki

Ein portables, browser-basiertes Wiki mit **Autosave**, **Volltextsuche** und **Markdown-Editor**.
Läuft ohne Installation – einfach die HTML-Datei doppelklicken und loslegen.

## Features

- **Autosave** – Speichert automatisch 800ms nach der letzten Eingabe, plus beim Verlassen der Seite
- **Markdown-Editor** – Geteilte Ansicht: links schreiben, rechts Live-Vorschau
- **Volltextsuche** – Durchsucht alle Seiteninhalte und Titel mit Treffer-Hervorhebung
- **localStorage** – Alle Daten bleiben im Browser erhalten, auch nach dem Neuladen
- **Portabel** – Eine einzige HTML-Datei (~31 KB), keine Installation, kein Server
- **Export/Import** – Einzelne Seiten als `.md`-Datei, alle Seiten in einen Ordner (File System API) oder als Einzel-Downloads
- **Tastaturkürzel** – `Strg+S` speichern, `Strg+B` für **fett**, `Strg+I` für *kursiv*
- **Wiki-Links** – `[[Seitenname]]` erzeugt einen internen Link
- **Responsive** – Funktioniert auf Desktop und Mobilgeräten

## Verwendung

1. **`index.html`** doppelklicken → öffnet im Browser
2. **Neue Seite** – Button `+ Neue Seite` in der Seitenleiste
3. **Bearbeiten** – ✏️-Button auf einer Seite oder Seitenlisten-Eintrag
4. **Suchen** – Suchfeld in der Seitenleiste (durchsucht Titel + Inhalt)
5. **Einstellungen** – ⚙-Button für Wiki-Titel und -Beschreibung

## Projektstruktur

```
mein-wiki/
├── index.html      ← Die gesamte Wiki-App (HTML + CSS + JS inline)
└── README.md       ← Diese Datei
```

Alles steckt in einer einzigen Datei. Keine Abhängigkeiten, keine Build-Tools.

## Technische Details

| Komponente | Beschreibung |
|---|---|
| **Sprache** | Vanilla JavaScript (kein Framework) |
| **Speicher** | localStorage (ca. 5 MB Speicherplatz – ausreichend für 100+ Seiten) |
| **Markdown** | Eigener Parser (unterstützt: Überschriften, Bold/Italic, Links, Bilder, Listen, Blockquotes, Code, Wiki-Links) |
| **Größe** | ~31 KB (unminifiziert) |
| **Browser** | Chrome, Firefox, Edge, Safari – alle modernen Browser |
| **Export** | File System Access API (Chromium) + Fallback auf Downloads |

### Markdown-Syntax (unterstützt)

```markdown
# Überschrift 1
## Überschrift 2

**fetter Text** und *kursiver Text*

- Ungeordnete Liste
- Noch ein Punkt

1. Erster Punkt
2. Zweiter Punkt

[Link](https://example.com)
![Bild](bild.jpg)

> Zitat

`inline code`

```code block```

[[Interner Link]]  → verlinkt auf eine andere Wiki-Seite
[[Text|seite]]     → Link mit anderem Anzeigetext
```

## Exportieren

Die Export-Funktionen findest du in den **Einstellungen** (⚙):

- **📥 .md** auf einer Seite – lädt die Seite als `.md`-Datei herunter
- **📦 Alle exportieren (.zip)** – lädt alle Seiten als einzelne `.md`-Downloads (Chromium: nutzt stattdessen die Ordner-Funktion)
- **📁 In Ordner exportieren** – öffnet einen Dialog zum Auswählen eines Ordners (File System API, Chromium)
- **📂 .md importieren** – importiert eine oder mehrere `.md`-Dateien

## Migration von Feather Wiki

Falls du bisher Feather Wiki verwendet hast:
1. Exportiere deine Seiten aus Feather Wiki (als `.md`-Dateien)
2. Importiere sie in Mein Wiki über **Einstellungen → 📂 .md importieren**
3. Fertig!

## Lizenz

MIT – mach damit, was du willst.
