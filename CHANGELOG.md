# Changelog

Alle nennenswerten Änderungen an diesem Projekt werden hier dokumentiert.

Das Format orientiert sich an [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
die Versionsnummern folgen [Semantic Versioning](https://semver.org/lang/de/)
(`MAJOR.MINOR.PATCH`):

- **MAJOR**: nicht kompatible/grundlegende Änderungen
- **MINOR**: neue Funktionen, abwärtskompatibel
- **PATCH**: Bugfixes, kleine Korrekturen

## [Unreleased]

### Hinzugefügt
- Dunkelmodus: manueller Umschalt-Button (🌙/☀) in der Toolbar, Auswahl wird
  projektübergreifend in `localStorage` gespeichert und beim Start
  wiederhergestellt.
- Umbenennbare Spaltenüberschriften für Montagestufe, Werkzeug / WT, Quelle und
  Station (Zusatz 2 und Zusatz 3 bereits vorher). Die Bezeichnungen werden im
  Projekt gespeichert und in CSV-/Excel-Export sowie im Taktabgleich mitgeführt.
- Spalte „Bauteil" lässt sich über 🔧 Spalten aus- und wieder einblenden.

### Geändert
- Die Zeilen-Aktionen (⧉ kopieren, 📋 einfügen, 📝 Notiz, 🗑 löschen) liegen jetzt
  in einer eigenen Spalte direkt hinter „Anzahl" statt in der Spalte „Bauteil" —
  so bleiben sie auch bei ausgeblendeter Bauteil-Spalte erreichbar.

### Behoben
- Umbenannte Spaltenüberschriften gingen beim CSV-Import verloren, weil die
  Kopfzeile nur übersprungen und rein nach Position eingelesen wurde. Der Export
  schreibt sie jetzt in die Metazeile `__COLLABELS__`, der Import stellt sie
  wieder her. CSV-Dateien ohne diese Zeile (ältere Exporte) lassen die aktuell
  eingestellte Benennung unverändert.
- Der CSV-Import akzeptierte auch Binärdateien (z.B. eine versehentlich gewählte
  `.xlsx`) und ersetzte das Projekt dabei durch Datenmüll. Solche Dateien werden
  jetzt mit einer verständlichen Meldung abgewiesen, die vorhandenen Daten
  bleiben unangetastet.

## [1.0.0] - 2026-09-15

### Hinzugefügt
- Baseline-Version der Zeitaufnahme-App (`index.html`) als Ausgangspunkt für
  die zukünftige Versionierung über Git-Tags und dieses Changelog.
