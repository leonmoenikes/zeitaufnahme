# Changelog

Alle nennenswerten Änderungen an diesem Projekt werden hier dokumentiert.

Das Format orientiert sich an [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
die Versionsnummern folgen [Semantic Versioning](https://semver.org/lang/de/)
(`MAJOR.MINOR.PATCH`):

- **MAJOR**: nicht kompatible/grundlegende Änderungen
- **MINOR**: neue Funktionen, abwärtskompatibel
- **PATCH**: Bugfixes, kleine Korrekturen

## [Unreleased]

> **Grundlegende Änderung (für den nächsten Release: 2.0.0).** Eine Tabellenzeile ist
> jetzt ein Prozessschritt statt eines Bauteils. Das CSV-Arbeitsformat ändert sich
> (`__FORMAT__;3`); Dateien im neuen Format kann eine ältere App-Version nicht lesen.
> Ältere CSV-Dateien und der gespeicherte Stand der Vorversion werden weiterhin
> übernommen und umgewandelt.

### Laufweg-Rechner
- Neuer Knopf „🚶 Laufwege" (Modus Erweitert). Die Kategorie „Meter in total" kann je
  Prozessschritt gerechnet statt gezählt werden:
  Meter = Σ Auslöser × Meterwert, auf ganze Meter gerundet.
- Sieben Auslöser mit zentralen Meterwerten:
  - Grundweg 2 m
  - Werkzeug 2 m
  - Rollwagen 4 m
  - Kranhub 6 m
  - Scan 3 m
  - Bereitstellen 8 m
  - Kommissionieren 1,5 m je Teil
- Reiter „Parameter":
  - Die Meterwerte stehen als gelbe Eingabefelder da; eine Änderung rechnet sofort alle
    gerechneten Schritte, die Tabelle und die Auswertung neu.
  - Kennzahlen: Σ Meter, Zeit in minD und min, Anteil am Ist, Schritte mit und ohne
    Laufweg sowie Summe und Anteil je Auslöser.
  - „Standardwerte" setzt die Meterwerte zurück.
  - „Auto-Zuordnung" setzt die Auslöser aller Schritte aus den vorhandenen Daten (Montagestufe,
    Werkzeug, Kranhub, Code-Scan, Schrittname). Eingetragene Rollwagen-Werte bleiben erhalten.
- Reiter „Je Schritt": je Schritt die sieben Auslöser als Eingabefelder, dazu Meter und minD.
  - Filter nach Station, Montagestufe und „nur Schritte ohne Laufweg"; die Summenzeile
    zählt die sichtbaren Zeilen.
  - Ein Wert größer 0 schaltet den Schritt aufs Rechnen um. Alle Auslöser auf 0 schaltet ihn
    zurück aufs Zählen; die Meterzahl bleibt auf dem letzten Stand.
  - Schritte ohne Auslöser sind grau hinterlegt.
- Gerechnete Schritte zeigen an der Meter-Kachel und in der Tabelle ein ƒ.
  - Tippen auf die Kachel (oder ihr Tastenkürzel) öffnet die Zeile des Schritts im Reiter
    „Je Schritt", statt zu zählen.
  - Undo, „Anzahl kopieren" und „Alle Zähler zurücksetzen" lassen gerechnete Meter unangetastet.
  - Meterwert- und Auslöseränderungen stehen nicht im Undo-Verlauf; der Weg zurück bei den
    Meterwerten ist „Standardwerte".
- Excel-Export mit fünftem Blatt „Laufwege" im Aufbau des Blatts „Laufweg-Parameter": gelbe
  Meterwerte, je Schritt die Auslöser und der Meter als ROUND-Formel. Gezählte Schritte stehen
  dort als Festwert mit „manuell".
- Die Blätter „Arbeitsablauf" und „Auswertung" rechnen jetzt mit Formeln statt fester Zahlen:
  - Zeit = Anzahl × Zeitwert aus Zeile 5; Gesamt und die Summenzeile sind Summen.
  - Die Meter-Anzahl gerechneter Schritte verweist auf das Blatt „Laufwege".
  - Ist, Kosten und Anteile in der Auswertung verweisen auf den Arbeitsablauf.
  - Eine geänderte gelbe Zelle rechnet in Excel bis ins Ist durch.
  - Zeile 5 zeigt die Zeitwerte jetzt mit voller Genauigkeit (0,0325 statt 0,033).
- CSV: zwei neue Metazeilen `__LWPARAM__` (Meterwerte) und `__LW__` (Auslöser je Datenzeile).
  - Spaltenaufbau und `__FORMAT__;3` bleiben unverändert.
  - Ältere Dateien öffnen sich mit Standardwerten und ohne gerechnete Schritte.
  - Ältere App-Versionen überspringen die neuen Zeilen und zeigen dieselbe Ist-Zeit.

### Behoben (Laufweg-Rechner)
- Tastenkürzel der Kategorien zählten auch, während das Fenster „Bausteine" offen war.
- Der Installationshinweis auf dem iPad greift auf den Sitzungsspeicher nur noch
  abgesichert zu (privates Surfen, Aufruf als data:-URL).

### Hinzugefügt (Standardkategorien)
- „Ø Ölen / Fetten" (0,156 minD, Process, Katalog-Grundelement #36) gehört jetzt fest zu
  den Kategorien eines neuen Projekts, am Ende der Process-Gruppe. Die Tastenkürzel der
  nachfolgenden Kategorien rücken dadurch um eine Taste weiter (Ø Code scan: U → I,
  Screw lock glue: I → O, Screw lock mech.: O → P, Quality gate: P → A, Ø QS check: A → S).
  Bestehende Projekte behalten ihre eigene Kategorienliste.

### Prozessschritte statt Bauteile
- Antippen der Felder „Sachnr." oder „Bauteilbenennung" in einer Schrittzeile klappt
  die Teile auf und wieder zu – eine größere Fläche als das kleine ▸.
- Der Knopf „↓ CSV Export" heißt jetzt „↓ Excel Export": Er öffnet den Dialog, in dem
  es sowohl den Excel-Report (.xlsx) als auch die CSV zum Weiterarbeiten gibt.
  Hinweistexte, die auf den Knopf verweisen, sind angepasst.
- Jede Zeile ist ein Prozessschritt, dem beliebig viele Teile (Sachnummer,
  Bezeichnung, Menge) zugeordnet sind. „Anzahl" ist die Summe der Teilemengen und
  wird berechnet, nicht mehr eingetippt.
- Tabelle: Spalten # · Lvl · Prozessschritt · Sachnummer · Bauteilbenennung. Zugeklappt
  zeigen Sachnummer und Benennung den ersten Eintrag plus „+n". Das Symbol ▸/▾ vor dem
  Namen klappt die Teile als Unterzeilen auf; dort werden Sachnummer, Bezeichnung und
  Menge direkt bearbeitet, „+ Teil hinzufügen" legt ein Teil an, ✕ entfernt es
  (per ↩ Undo rücknehmbar). Fokus in einer Unterzeile aktiviert den Schritt, gezählt
  wird wie bisher immer auf den aktiven Schritt.
- „➕ Schritt" statt „➕ Bauteil"; neuer Knopf „Alle auf-/zuklappen". Der
  Aufklapp-Zustand wird mitgespeichert. Kopieren/Einfügen einer Zeile übernimmt die
  Teile mit eigenen IDs.
- Lvl, Prozessschritt, Sachnummer und Bauteilbenennung lassen sich über
  „🔧 Spalten" ausblenden; ist „Prozessschritt" ausgeblendet, sitzt ▸/▾ in der
  #-Spalte. Beim seitlichen Scrollen bleiben #, Lvl und Prozessschritt stehen.
- Filter auf Sachnummer bzw. Bauteilbenennung zeigen jeden Schritt, bei dem mindestens
  ein Teil passt; aufgeklappt werden die passenden Teile hervorgehoben. Der
  Anzahl-Filter arbeitet auf der berechneten Anzahl.
- Auswertung und Druck sprechen von Prozessschritten; „Anzahl aller Teile" und
  „Ø Zeit/Stk." beruhen auf der Summe der Teilemengen. Der Taktabgleich zeigt je
  Station „Schritte" und „Teile".
- CSV-Format 3: erste Zeile `__FORMAT__;3`, Spalte „Teile" (URL-kodiertes JSON) statt
  „Sachnummer". Export → Import → Export ergibt dieselbe Datei.
- Excel-Report mit vier Blättern: „Arbeitsablauf" (Teile als Zusammenfassung mit
  Sachnummer), neu „Teileliste" (eine Zeile je Teil mit Autofilter, zum Abgleich mit
  der SAP-Stückliste), „Auswertung", „Zeitwerte".
- Speicherstand unter neuem Schlüssel `zeitaufnahme_v21`; der Stand der Vorversion
  (`zeitaufnahme_v20`) wird beim ersten Start übernommen und bleibt unverändert liegen.
- „↺ Alle Zähler zurücksetzen" setzt nur noch Zählwerte zurück, Teile bleiben.
- Behoben: LibreOffice übernahm den Autofilter des Excel-Exports nicht, weil der
  zugehörige versteckte Name `_xlnm._FilterDatabase` fehlte.

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
- Einheit in den Bezeichnungen korrigiert: Grundelement #28 heißt jetzt „Seal or grease
  small (400 cm²)", #27 „Seal or grease large (2500 cm²)" (bisher „400mm"/„2500mm"),
  der darauf aufbauende Baustein „Clean & Seal 400cm²" (bisher „400mm²"). Nur die
  Namen ändern sich, die Zeitwerte bleiben gleich. In bestehenden Projekten trägt die
  Kategorie ihren gespeicherten Namen; umbenennen geht gefahrlos über „⚙ Zeiten".
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
