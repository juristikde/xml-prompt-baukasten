# Prompt Baukasten – Strukturierter XML-Editor

<div align="center">

**Visueller Editor für strukturierte LLM-Prompts.**  
Kein Backend · eine HTML-Datei · offline-fähig · mehrsprachig

[![Single File](https://img.shields.io/badge/single%20file-HTML-blue?style=flat-square)](#technik)
[![Offline](https://img.shields.io/badge/offline-fähig-75C46B?style=flat-square)](#technik)
[![No Dependencies](https://img.shields.io/badge/dependencies-0-lightgrey?style=flat-square)](#technik)
[![i18n](https://img.shields.io/badge/i18n-38%20Sprachen-purple?style=flat-square)](#internationalisierung)
[![License: MIT](https://img.shields.io/badge/license-MIT-00ACD7?style=flat-square)](#lizenz)

**[➜ Live-Demo](https://juristikde.github.io/xml-prompt-baukasten)** · **[➜ Prompt-Bibliothek](https://juristikde.github.io/xml-prompt-bibliothek/)**

![Prompt Baukasten Screenshot](screenshots/editor-overview.webp)

</div>

---

## Inhaltsverzeichnis

- [Warum?](#warum)
- [Features](#features)
- [Quickstart](#quickstart)
- [Bedienung](#bedienung)
  - [Workspace & Tabs](#workspace--tabs)
  - [Struktur-Liste](#struktur-liste)
  - [Detail-Editor](#detail-editor)
  - [XML-Ansicht](#xml-ansicht)
  - [Protokoll & Validierung](#protokoll--validierung)
  - [WikiText](#wikitext)
  - [Prompt-Bibliothek](#prompt-bibliothek)
- [Mobile](#mobile)
- [Internationalisierung](#internationalisierung)
- [URL-Parameter](#url-parameter)
- [Technik](#technik)
- [Browser](#browser)
- [Projektstruktur](#projektstruktur)
- [Mitwirken](#mitwirken)
- [Lizenz](#lizenz)

---

## Warum?

> Ein guter Prompt ist kein Fließtext – er ist Architektur.

Strukturierte XML-Prompts (`<rolle>`, `<regeln>`, `<beispiele>`, …) sind robuster, wiederverwendbarer und für LLMs oft klarer als langer Fließtext. Handgeschriebenes XML wird schnell unübersichtlich: Verschachtelung, Tippfehler in Tag-Namen, vergessene Entities.

**Prompt Baukasten** löst das mit zwei synchronen Ansichten:

| Links | Rechts |
| --- | --- |
| Hierarchische Struktur-Liste (Outline) | Fokussierter Detail-Editor für Tag & Text |
| Drag & Drop, Klappen, Vorschau | Ebene, Pfad, Werkzeuge, Textfeld |

Das Ergebnis ist immer sauber serialisiertes XML – ohne Server, ohne Upload, ohne Tracking.

**Typische Einsatzfelder:** System-Prompts, Agenten-Rollen, Few-Shot-Beispiele, Chat-Turn-Strukturen (`user` / `assistant`), mandantenspezifische Regelwerke.

---

## Features

| Bereich | Was du bekommst |
| --- | --- |
| **Editor** | Visuelle Baumstruktur statt Roh-XML; unbegrenzte Verschachtelung; Kommentare als eigene Elemente (`💬`) |
| **Sync** | Liste ↔ XML jederzeit synchron; XML einfügen und „Übernehmen“ baut die Struktur neu auf |
| **Tabs** | Mehrere Prompts parallel; Titel editierbar; Duplizieren; Gesamt-Config aller Tabs |
| **Validierung** | Protokoll-Fenster mit Fehlern, Warnungen und Hinweisen; Sprung zur Stelle; Badge am Protokoll-Button |
| **WikiText** | Zufälliger Wikipedia-Auszug (11 Sprachen + zufällig) an der Cursor-Position |
| **Bibliothek** | Externe kuratierte Vorlagen-Sammlung in neuem Tab |
| **Mobile** | Bottom-Sheets, Long-Press-Drag, 44px Touch-Ziele, kein hängendes Hover |
| **i18n** | UI in 38 Sprachen; Sprache per Menü oder URL |
| **Teilen** | Layout- und Optionen-Zustand im URL-Hash (ohne Prompt-Inhalt) |

Kein Account, kein Backend, keine Telemetrie.

---

## Quickstart

**A – Live im Browser**

→ [juristikde.github.io/xml-prompt-baukasten](https://juristikde.github.io/xml-prompt-baukasten)

**B – Lokal öffnen**

```bash
# Datei doppelklicken oder:
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows
```

**C – Lokaler Server** (empfohlen, wenn `lang/*.json` relativ geladen werden)

```bash
python3 -m http.server 8000
# → http://localhost:8000/
```

Keine Dependencies, kein Build-Schritt.

---

## Bedienung

### Workspace & Tabs

Jeder Tab speichert eigene Struktur, Auswahl und internen Zähler.

- **Titel** im Panel-Kopf (neben Duplizieren) – live editierbar
- **`+`** in der Tab-Leiste → neuer leerer Prompt
- **`×`** am Tab → schließen (der letzte Tab wird geleert, nicht entfernt)
- **Duplizieren** → Kopie des aktuellen Tabs inkl. Struktur
- **Zurücksetzen** → aktuellen Tab leeren (mit Bestätigung)

Desktop: Duplizieren und Zurücksetzen sitzen im Prompt-Header.  
Mobil: beides im **Optionen**-Menü desselben Headers.

### Struktur-Liste

Linke Spalte – Übersicht über den Baum.

| Aktion | Wirkung |
| --- | --- |
| Klick auf Zeile | Auswahl + Detail-Editor |
| `▾` / `▸` | Unterbaum auf-/zuklappen |
| Ziehen (Maus) | Reihenfolge **innerhalb derselben Ebene** |
| Long-Press (Touch, ~420 ms) | Verschiebe-Modus, optional Vibration |
| Fußbereich | `+ Element`, `+ Kommentar`, `+ user`, `+ assistant`, `+ Unterpunkt`, `Löschen`, **Ergebnis kopieren** |

Tag-Namen in Serif-Bold, Textvorschau und Kind-Anzahl in der Zeile. Fehlerhafte Knoten bekommen eine rote Markierung.

### Detail-Editor

Nach Auswahl rechts (Desktop) bzw. als Sheet von rechts (Mobil):

1. **Ebenen-Badge** + klickbarer **Breadcrumb-Pfad**
2. **Tag-Zeile** `< name >` – Leerzeichen werden zu `-`
3. **Werkzeuge:** ↑/↓, Kopieren/Einfügen (Knoten-Clipboard), Suchen & Ersetzen, **+ WikiText**
4. **Textfeld** für Inhalt (bei Container-Tags mit Kindern deaktiviert – Inhalt gehört in Kind-Knoten)
5. Optionaler **Zeichenzähler** (per URL-Parameter)

Kommentare erscheinen als `💬 Anmerkung` mit kursivem Feld.

### XML-Ansicht

Toolbar: **XML anzeigen** (Desktop) bzw. Optionen → XML anzeigen (Mobil).

- Desktop: zweite Spalte neben dem Editor  
- Mobil: Sheet von links  
- **Übernehmen** parst den Text zurück in den Baum (erkennt äußeres `<prompt>`)  
- **Kopieren** in die Zwischenablage  
- **Gesamt** / **Tab-XML**: alle Tabs als Gesamt-Config oder nur den aktiven Tab  
- **Umbruch** an/aus, **Suchen** im Quelltext  

Beispiel-Ausgabe:

```xml
<prompt>
  <rolle>Du bist ein hilfsbereiter Assistent …</rolle>
  <regeln>
    <regel>Nenne niemals interne Artikelnummern.</regel>
    <!-- Interner Hinweis: pro Mandant anpassen. -->
  </regeln>
</prompt>
```

Einzelne `&` im Import werden beim Parsen zu `&amp;` normalisiert.

### Protokoll & Validierung

**Protokoll** öffnet ein modales Log (nicht nur ein Banner).

- **Prüfen** validiert die Struktur:
  - harte Fehler: leere oder ungültige Tag-Namen (`/^[A-Za-z_][A-Za-z0-9_.\-]*$/`)
  - weiche Hinweise: generische Namen (`data`, `item`, …), tiefe Verschachtelung (> 4), leere Tags, `<example>` außerhalb von `<examples>`
- Einträge mit Zeitstempel; Fehler erhöhen einen **Badge** am Protokoll-Trigger
- **Leeren** löscht das Log; beim Öffnen des Protokolls wird der Badge zurückgesetzt
- Max. Einträge steuerbar über `protocolThreshold` (Standard: 20)

### WikiText

Geteilter Button **+ WikiText** im Detail-Editor (Desktop: gleiche Höhe wie die anderen Small-Buttons).

| Teil | Aktion |
| --- | --- |
| Hauptfläche | Sofort einfügen mit letzten Einstellungen |
| Pfeil | Sprache + ca. Zeichen (80–2000) |

Quelle: Wikipedia-API (`generator=random`). Sprachen: de, en, fr, es, it, pt, nl, pl, ru, ja, zh sowie **zufällig**. Einfügeposition = Cursor im Textfeld. Braucht Internet; der Rest der App läuft offline.

### Prompt-Bibliothek

Der Button **Bibliothek** (Desktop-Toolbar bzw. Optionen mobil) öffnet in einem **neuen Tab**:

→ [juristikde.github.io/xml-prompt-bibliothek](https://juristikde.github.io/xml-prompt-bibliothek/)

Dort liegen kuratierte Vorlagen. In die App übernimmst du sie per Kopieren in die XML-Ansicht und **Übernehmen**.

---

## Mobile

Ab **≤ 900 px** (nochmals verdichtet ab ≤ 480 px):

- Toolbar: nur **Optionen** (Sprache, Protokoll, XML, Bibliothek)
- Prompt-Header: **Optionen** (Duplizieren, Zurücksetzen)
- Detail und XML als **Sheets** über der Liste; Struktur bleibt bedienbar
- **›** in der Listenzeile öffnet den Editor-Sheet
- Alle `:hover`-Styles nur unter `@media (hover: hover) and (pointer: fine)`
- Mindesthöhe interaktiver Elemente: 44 px

![Mobile Ansicht](screenshots/mobile-sheet.webp)

---

## Internationalisierung

UI-Texte liegen in `lang/{code}.json` (ISO 639-1). Die App lädt die Datei dynamisch; Fallback ist Deutsch.

- **38 Sprachen** im Languages-Objekt der JSON-Pakete
- Anzeige im Sprachmenü: **native** (Endonym), Suche auch über **local** (Name in der aktuellen UI-Sprache) und Code
- Parameter: `setLanguage=de` (auch im Hash; wird bei Wechsel aktualisiert)
- **Nicht übersetzt:** Prompt-/Template-Inhalte und Tag-Namen – nur UI-Chrome

Bei UI-Änderungen: Keys in **allen** `lang/*.json` nachziehen (siehe Hinweisblock im `<head>` der HTML-Datei).

---

## URL-Parameter

Zustand im **Hash** (ohne Prompt-Inhalt), damit Layout und Optionen teilbar sind:

```
#setLanguage=de&tabBarLocation=top&tabBarShown=true&showCharacterCount=false&xmlCodeLineWrap=true&unpackMobileOptionsButton=false&protocolThreshold=20
```

| Parameter | Werte | Standard | Wirkung |
| --- | --- | --- | --- |
| `setLanguage` | ISO-639-1 | System / `de` | UI-Sprache |
| `tabBarLocation` | `top` / `left` | `top` | Tab-Leiste oben oder links |
| `tabBarShown` | `true` / `false` | `true` | Tab-Leiste ein-/ausblenden |
| `showCharacterCount` | `true` / `false` | `false` | Zeichenzähler an Feldern und Ergebnis |
| `xmlCodeLineWrap` | `true` / `false` | `true` | Zeilenumbruch in der XML-Ansicht |
| `unpackMobileOptionsButton` | `true` / `false` | `false` | Auf Mobil Werkzeuge „ausgepackt“ statt Options-Menü |
| `protocolThreshold` | 1–1000 | `20` | Max. Einträge im Protokoll |

Alle optional und kombinierbar. `setLanguage` steht bewusst zuerst im Hash.

---

## Technik

| Aspekt | Umsetzung |
| --- | --- |
| Auslieferung | Eine `index.html` (CSS + JS inline); Icons/Favicons von CDN bzw. Repo |
| Laufzeit | Reiner Client; kein Build, kein Bundler |
| Zustand | `tabs[]`, aktiver Baum, Auswahl, Protokoll – **kein** LocalStorage (bewusst frischer Start) |
| XML | `DOMParser` mit temporärer `__root__`-Hülle; Serialisierung mit Escape; Mixed Content → automatische `_text`-Kinder |
| i18n | `fetch('lang/xx.json')`, `data-i18n*` Attribute, `t(default, key, vars)` |
| Drag | HTML5 Drag & Drop (Desktop); Touch Long-Press (Mobil) |

---

## Browser

Getestet in aktuellen Chromium-, Firefox- und Safari-Versionen (Desktop und iOS).

| API | Nutzung |
| --- | --- |
| `fetch` | Sprachen + WikiText (Internet) |
| `navigator.clipboard` | Kopieren; Fallback `document.execCommand('copy')` |
| `navigator.vibrate` | Optional bei Long-Press |
| `DOMParser` | XML-Import |

Ohne Netz: Editor, Tabs, Validierung und XML-Sync funktionieren; WikiText und Sprachwechsel auf noch nicht geladene JSONs brauchen Verbindung.

---

## Projektstruktur

```
xml-prompt-baukasten/
├── index.html          # App (HTML + CSS + JS)
├── lang/               # i18n-Pakete (de.json, en.json, …)
├── icons/              # Favicons & Logo
├── screenshots/        # README-Bilder
├── LICENSE
└── README.md
```

Verwandtes Projekt: **[xml-prompt-bibliothek](https://juristikde.github.io/xml-prompt-bibliothek/)** – kuratierte Vorlagen zum Import.

---

## Mitwirken

Issues und Pull Requests sind willkommen.

1. Forken  
2. Änderungen in `index.html` und bei UI-Texten in **allen** betroffenen `lang/*.json`  
3. Desktop **und** Mobil testen (≤ 900 px und ≤ 480 px)  
4. PR mit kurzer Beschreibung und idealerweise Screenshot/GIF  

Bitte keine eingebetteten Tracking-Skripte und den Single-File-Charakter der App beibehalten.

---

## Lizenz

MIT – freie Nutzung privat und kommerziell. Details in [`LICENSE`](LICENSE).
