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
- Soll-Taktzeit im Taktabgleich: Eingabefeld (minD, mit Umrechnung in min und s),
  daraus Auslastung je Station in %, eine gestrichelte Taktlinie im Balkendiagramm
  (Balken über dem Takt rot) und die Kennzahlen Engpass, Bandwirkungsgrad
  (Σ Stationszeiten ÷ (Anzahl Stationen × längste Station)) mit Abstimmungsverlust
  sowie Anzahl Stationen über Takt. Ein Schalter legt fest, ob die Stationszeiten
  mit oder ohne Verteilzeit gegen den Takt gestellt werden.
- Was-wäre-wenn-Szenario im Taktabgleich (Umschalter „Ist / 🔀 Szenario"):
  Bauteile per Auswahlfeld probeweise zwischen Stationen verschieben, neue
  Stationen anlegen und sofort sehen, wie sich Balken, Auslastung und Kennzahlen
  ändern — mit Ist-Wert als gestricheltem Rahmen und Δ-Spalte. Die Basisdaten
  bleiben dabei unberührt. Das Szenario wird im Projekt und in der CSV gespeichert
  (`__TAKT__`, `__SZENARIO__`), lässt sich verwerfen oder nach Rückfrage in die
  Tabelle übernehmen (per Undo Bauteil für Bauteil rücknehmbar) und erscheint im
  PDF-Bericht als eigener Abschnitt mit Vorher/Nachher und Liste der Verschiebungen.
- Baustein-Rechner (Toolbar „🧱 Bausteine", nur im Erweitert-Modus): macht sichtbar,
  wie jeder Zeitwert entsteht — Baustein → Grundelemente (mit Gewicht) → MTM-Codes
  mit Einzelzeit, Anzahl und Häufigkeit, jeweils mit ausgeschriebener Formel.
  Aus demselben Fenster lassen sich neue Bausteine anlegen: Grundelemente wählen,
  Gewichte setzen, Zeitwert wird live berechnet. Die drei im Katalog enthaltenen,
  bisher nicht genutzten Bausteine (u.a. „Ø Ölen / Fetten") sind per Knopfdruck
  übernehmbar. Die MTM-Datenbasis (278 Codes, 38 Grundelemente, 24 Bausteine) liegt
  statisch im Code; geschrieben wird ausschließlich `COLS`.
- Vierter Reiter „Neues Grundelement" im Baustein-Rechner: baut aus LAMA-Elementen
  ein eigenes Grundelement. Die Auswahl der 278 LAMA-Elemente läuft über die
  Katalog-Gliederung — Bereich (13) → Untergruppe → Trefferliste — zusätzlich
  filtert ein Suchfeld über Code, Kurztext und Bereich. Je Element lassen sich
  Anzahl und Häufigkeit setzen, dazu eine Bezugsmenge; der Zeitwert wird live nach
  Σ(Zeit × Anzahl × Häufigkeit) ÷ Bezugsmenge gerechnet. Dasselbe Element darf
  mehrfach vorkommen (Katalog-Grundelement #32 tut das auch). Fertige eigene
  Grundelemente stehen sofort im Reiter „Neuer Baustein" zur Auswahl und werden im
  Projekt sowie in der CSV (`__MTMGE__`) mitgeführt.
- Selbst angelegte Bausteine lassen sich im Reiter „Bausteine" wieder löschen,
  selbst angelegte Grundelemente im Reiter „Grundelemente". Beides nur, solange
  nichts daran hängt: ein Baustein mit erfassten Zählwerten und ein Grundelement,
  das ein Baustein verwendet, werden mit Hinweis abgelehnt. Der Katalog bleibt
  unantastbar.
- Dritter Reiter „Grundelemente" im Baustein-Rechner: schlägt alle 38 Grundelemente
  der Datenbasis nach — aufgeklappt zeigt jedes seine MTM-Codes mit Einzelzeit,
  Anzahl, Häufigkeit und Anteil sowie die Bezugsmenge, dazu die Gegenrichtung zum
  ersten Reiter: in welchen Bausteinen das Grundelement mit welchem Gewicht steckt.
  Ein Tipp auf einen dieser Bausteine springt dorthin. Ein Suchfeld filtert über
  Name, MTM-Code und Kurztext. Reine Anzeige — Grundelemente und Katalog bleiben
  unveränderlich.
- Umbenennbare Spaltenüberschriften für Montagestufe, Werkzeug / WT, Quelle und
  Station (Zusatz 2 und Zusatz 3 bereits vorher). Die Bezeichnungen werden im
  Projekt gespeichert und in CSV-/Excel-Export sowie im Taktabgleich mitgeführt.
- Spalte „Bauteil" lässt sich über 🔧 Spalten aus- und wieder einblenden.
- Der Taktabgleich lässt sich über ein Auswahlfeld nach jeder Zusatzspalte
  gruppieren (Montagestufe, Werkzeug / WT, Quelle, Station, Zusatz 2, Zusatz 3)
  statt fest nach „Station". Die Auswahl wird im Projekt gespeichert.

### Geändert
- Taktabgleich: Bauteile ohne Stationseintrag („(ohne Station)") zählen nicht mehr
  als eigene Station — sie gehen weder in den Mittelwert noch in die Abweichung,
  den Engpass oder den Bandwirkungsgrad ein und stehen grau am Ende der Liste.
  Bisher verschob diese Pseudo-Station den Mittelwert.
- Taktabgleich: Stationszeiten werden standardmäßig inklusive Verteilzeit
  angezeigt (Schalter „mit Verteilzeit"); bei eingestellter Verteilzeit liegen die
  Werte daher um diesen Faktor höher als bisher. Die Spaltenüberschrift sagt es an.
- Der erste Reiter des Baustein-Rechners heißt jetzt „Bausteine" statt
  „Zusammensetzung"; die unterste Ebene heißt durchgängig „LAMA-Elemente" statt
  „MTM-Codes". Damit tragen alle drei Ebenen die Namen, unter denen sie in der
  Zeitwirtschaft geführt werden: Baustein → Grundelement → LAMA-Element.
- Zeiten werden in der Tabelle ab der ∑-Spalte, in der Aktiv-Leiste und in der
  gesamten Auswertung (inkl. Taktabgleich und PDF-Bericht) mit zwei statt drei
  Nachkommastellen angezeigt. Die Kategorie-Buttons bleiben dreistellig.
  Gerechnet wird unverändert mit voller Genauigkeit, CSV- und Excel-Export
  liefern weiterhin drei Nachkommastellen.
- „➕ Bauteil" fragt jetzt nach dem Namen (vorbelegt mit dem bisherigen
  Automatik-Namen); Abbrechen legt nichts an. Die Einfügeposition bleibt
  unverändert direkt hinter dem aktiven Bauteil.
- Der Notiz-Button (📝) je Zeile ist jetzt auch im Einfach-Modus sichtbar.
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

### Entfernt
- Dunkelmodus wieder ausgebaut: Umschalt-Button, dunkle Farbpalette, die
  zugehörigen `body.dark-mode`-Regeln und die gespeicherte Einstellung sind
  entfallen. Die Oberfläche ist wieder durchgehend hell. Ein eventuell noch
  gespeicherter Schlüssel `zeitaufnahme_theme` wird nicht mehr gelesen.

### Behoben
- Im Einfach-Modus wurden die linken Spalten (vor allem Station und Anzahl)
  deutlich breiter als im Erweitert-Modus, sobald die Tabelle ohne die
  [minD]-Spalten schmaler war als der Bildschirm — gemessen bei sechs Kategorien
  auf iPad-Breite: Station 80 → 146 px, Anzahl 60 → 169 px. Die Tabelle wird auf
  Bildschirmbreite gestreckt, und der Browser verteilte den Rest auch auf diese
  Spalten. Bauteil, Zusatzspalten, Anzahl, Aktionen und ∑ sind jetzt nur so breit
  wie ihr Inhalt; übriger Platz geht ausschließlich an die Zählspalten.
- Der Baustein-Rechner zeigte nach einem Umbenennen unter „⚙ Zeiten" weiter den
  Katalognamen statt der eigenen Bezeichnung. Steht ein Baustein im Tool, gelten
  jetzt dessen Name und Gruppe.
- Ein von Hand geänderter Zeitwert ließ sich nur durch erneutes Eintippen
  zurückholen. Abweichende Bausteine haben im Rechner jetzt einen Knopf
  „zurücksetzen", der den errechneten Wert wieder einsetzt.
- Eine Kategorie unter „⚙ Zeiten" umzubenennen löschte bislang sämtliche dafür
  erfassten Zählwerte: Der Dialog suchte den Schlüssel über den Namen, ein neuer
  Name ergab also einen neuen Schlüssel und die Spalte startete bei null. Die
  Identität hängt jetzt am Schlüssel; Umbenennen lässt Werte, Zeiten und die
  hinterlegte Herleitung unangetastet. Eine neu angelegte Kategorie bekommt immer
  einen eigenen Schlüssel — gleicher Name bedeutet damit nicht mehr dieselbe Spalte.
- Selbst angelegte Bausteine ließen sich im Rechner nicht aufklappen: Ihre
  Zusammensetzung wurde nirgends gemerkt, deshalb standen sie ohne Herleitung am
  Ende der Liste. Sie wird jetzt mitgespeichert, überlebt Neuladen und CSV-Export/
  -Import und klappt wie die Katalog-Bausteine auf. Der CSV-Import überspringt
  unbekannte Metazeilen jetzt generisch, ältere Dateien bleiben lesbar.
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
