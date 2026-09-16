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
- Der Taktabgleich lässt sich über ein Auswahlfeld nach jeder Zusatzspalte
  gruppieren (Montagestufe, Werkzeug / WT, Quelle, Station, Zusatz 2, Zusatz 3)
  statt fest nach „Station". Die Auswahl wird im Projekt gespeichert.

### Geändert
- Spaltenfilter arbeitet jetzt wie der Excel-Autofilter: Ein Suchbegriff wählt die
  Treffer direkt vor („Alle Suchergebnisse"), Enter oder OK übernimmt genau diese,
  Abbrechen verwirft. Bisher blieben beim Suchen auch alle nicht passenden Werte
  angehakt — man musste erst alles abwählen, dann suchen, dann wieder auswählen.
  OK ist gesperrt, solange nichts ausgewählt ist.
- Die Top-10-Bauteile zeigen pro Zeile einen gestapelten Balken: Länge = Gesamtzeit
  im Verhältnis zu Platz 1, Farbsegmente = Zeitanteile der Kategorie-Gruppen. Die
  Liste „niedrigste Gesamtzeit" entfällt dafür — sie enthielt bei wenigen Bauteilen
  ohnehin dieselben Einträge in umgekehrter Reihenfolge.
- Die Zeilen-Aktionen (⧉ kopieren, 📋 einfügen, 📝 Notiz, 🗑 löschen) liegen jetzt
  in einer eigenen Spalte direkt hinter „Anzahl" statt in der Spalte „Bauteil" —
  so bleiben sie auch bei ausgeblendeter Bauteil-Spalte erreichbar.
- Der Taktabgleich rechnet Mittelwert und Abweichung jetzt in minD statt in min;
  auch das Balkendiagramm ist auf minD umgestellt. Die Spalte „Zeit [min]" bleibt
  als Umrechnung erhalten.
- „🖨 Drucken / PDF" der Auswertung neu aufgebaut: Kopfzeile mit Projekt, Einheit,
  Verteilzeit und Stundensatz, Kennzahlen als Kacheln, beide Kreisdiagramme
  (je Kategorie-Gruppe und je Kategorie) mit Anteils-Tabelle, Top-10-Listen
  nebeneinander und eine Fußzeile. Tabellenköpfe
  wiederholen sich auf Folgeseiten, Zeilen und kurze Blöcke werden nicht mehr
  über zwei Seiten gerissen.

### Behoben
- Umbenannte Spaltenüberschriften gingen beim CSV-Import verloren, weil die
  Kopfzeile nur übersprungen und rein nach Position eingelesen wurde. Der Export
  schreibt sie jetzt in die Metazeile `__COLLABELS__`, der Import stellt sie
  wieder her. CSV-Dateien ohne diese Zeile (ältere Exporte) lassen die aktuell
  eingestellte Benennung unverändert.
- Der Druck-Export der Auswertung enthielt nur die Übersicht; der Taktabgleich
  fehlte vollständig. Er ist jetzt mit Tabelle und Verteilungsbalken enthalten.
- Im Dunkelmodus druckte die Auswertung helle Schrift auf weißes Papier, weil die
  Druckansicht die Theme-Farben übernahm. Sie bringt jetzt eigene Farben mit.
- Bauteil- und Kategoriebezeichnungen wurden in der Auswertung ungefiltert als
  HTML eingefügt — aus einer importierten CSV konnte so Markup in die Anzeige
  gelangen. Die Bezeichnungen werden jetzt maskiert.
- Der CSV-Import akzeptierte auch Binärdateien (z.B. eine versehentlich gewählte
  `.xlsx`) und ersetzte das Projekt dabei durch Datenmüll. Solche Dateien werden
  jetzt mit einer verständlichen Meldung abgewiesen, die vorhandenen Daten
  bleiben unangetastet.

## [1.0.0] - 2026-09-15

### Hinzugefügt
- Baseline-Version der Zeitaufnahme-App (`index.html`) als Ausgangspunkt für
  die zukünftige Versionierung über Git-Tags und dieses Changelog.
