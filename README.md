```markdown
# Prompt Baukasten

**Strukturierter XML-Editor und Viewer für Prompts**

Ein einfaches, lokal laufendes Web-Tool, mit dem man XML-formatierte Prompts einlesen, visuell bearbeiten und neu erstellen kann. Die Oberfläche trennt Gliederung und Inhalt: links die Struktur, rechts der große, gut lesbare Editor für den jeweils ausgewählten Abschnitt.

Alles läuft ausschließlich im Browser. Es werden keine Daten hochgeladen.

---

## Warum XML in Prompts?

Freitext-Prompts werden schnell unübersichtlich, sobald Rollen, Regeln, Beispiele, Einschränkungen und Ausgabeformate dazukommen. XML (oder xml-ähnliche Tags) bietet mehrere Vorteile:

- **Klare Hierarchie** – Abschnitte wie `<rolle>`, `<aufgabe>`, `<regeln>` oder `<beispiele>` sind eindeutig voneinander getrennt.
- **Einfache Erweiterung** – Neue Elemente oder Unterpunkte lassen sich ohne Umformatierung des gesamten Textes hinzufügen.
- **Bessere Lesbarkeit für Mensch und Modell** – Modelle können strukturierte Abschnitte oft zuverlässiger interpretieren als lange Fließtext-Blöcke.
- **Wiederverwendbarkeit** – Einzelne Bausteine (z. B. Regelwerke oder Beispielpaare) können leichter kopiert, ausgetauscht oder versioniert werden.
- **Validierbarkeit** – Syntaxfehler (offene Tags, ungültige Namen) fallen schneller auf.

Das Tool ersetzt kein Prompt-Engineering-Framework. Es macht den Einstieg in strukturierte XML-Prompts jedoch deutlich komfortabler.

---

## Was das Tool kann

### Viewer
- Bestehenden XML-Prompt einfügen
- Struktur als Gliederung (Outline) anzeigen
- Einzelne Abschnitte und Kommentare gezielt auswählen und lesen
- Verschachtelte Elemente und XML-Kommentare unterstützen

### Generator / Editor
- Neue Elemente und Kommentare anlegen
- Tag-Namen und Inhalte direkt bearbeiten
- Unterpunkte hinzufügen, verschieben und löschen
- Breadcrumb-Navigation durch die Hierarchie
- Live-Aktualisierung des XML-Codes
- Ergebnis mit einem Klick in die Zwischenablage kopieren

### Zusätzliche Funktionen
- Beispiel-Prompt laden
- Validierung der Tag-Namen und Struktur
- Hilfe beim Ersetzen von ungeescapten `&`-Zeichen
- Vollständig offline und ohne Backend

---

## Schnellstart

1. Die HTML-Datei im Browser öffnen (einfach per Doppelklick oder per lokalem Server).
2. Entweder „Beispiel laden“ wählen oder eigenen XML-Code über „XML-Code anzeigen“ einfügen und übernehmen.
3. Links in der Gliederung navigieren, rechts Inhalte bearbeiten.
4. Fertigen Prompt über „Ergebnis in die Zwischenablage kopieren“ exportieren.

Das Tool erwartet in der Regel ein Wurzel-Element `<prompt>…</prompt>`. Beim Einlesen wird dieses automatisch erkannt und die darunterliegenden Kinder als Baum dargestellt.

---

## Typischer Aufbau eines XML-Prompts

```xml
<prompt>
  <rolle>…</rolle>
  <aufgabe>…</aufgabe>
  <regeln>
    <regel>…</regel>
    <!-- optionaler Kommentar -->
    <regel>…</regel>
  </regeln>
  <beispiele>
    <beispiel>
      <eingabe>…</eingabe>
      <ausgabe>…</ausgabe>
    </beispiel>
  </beispiele>
</prompt>
```

Die Tag-Namen sind frei wählbar. Das Tool erzwingt keine feste Schema-Definition.

---

## Technische Hinweise

- Reine Client-Side-Anwendung (HTML + CSS + JavaScript)
- Keine externen Abhängigkeiten außer Google Fonts (können bei Bedarf entfernt werden)
- XML-Parsing über die native `DOMParser`-API des Browsers
- Serialisierung erzeugt eingerücktes, lesbares XML
- Funktioniert in modernen Browsern (Chrome, Firefox, Edge, Safari)

---

## Grenzen

- Kein vollständiger XML-Schema-Validator
- Keine Unterstützung für Attribute an Elementen (nur Tag-Name + Text/Kinder)
- Keine automatische Prompt-Optimierung oder Modell-Anbindung
- Für sehr große oder stark verschachtelte Dokumente ist die Oberfläche noch einfach gehalten

Das Tool ist bewusst schlank gehalten: schneller Einstieg in strukturierte Prompts, ohne Setup und ohne Cloud.

---

*Lokaler Prompt-Baukasten – strukturiert schreiben, klar lesen.*
```
