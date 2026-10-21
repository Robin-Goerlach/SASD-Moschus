# Pflichtenheft — SASD Moschus

| Merkmal | Inhalt |
|---|---|
| Dokument | Technisches Pflichtenheft |
| Projekt | SASD Moschus |
| Auftraggeber und Product Owner | Robin Goerlach / SASD-GmbH |
| Repository | https://github.com/Robin-Goerlach/SASD-Moschus |
| Version | 0.1 |
| Stand | 21. Oktober 2026 |
| Status | Verbindliche Arbeitsgrundlage; offene Entscheidungen sind ausdrücklich gekennzeichnet |
| Lizenz des Projekts | MIT |
| Erste Zielmarke | Vollständige, überprüfte Format- und Werkzeug-Epoche bis einschließlich 31. Dezember 1990 |
| Zugehöriges Lastenheft | [LASTENHEFT.md](LASTENHEFT.md) |

## 1. Zweck des Dokuments

Dieses Pflichtenheft beschreibt, wie SASD Moschus die im
[Lastenheft](LASTENHEFT.md) festgelegten Ziele und Anforderungen technisch und
organisatorisch umsetzt. Es ist die verbindliche Grundlage für Architektur,
Implementierung, Tests, Dokumentation und Abnahme.

Moschus ist kein bloßer Dateikonverter. Das Projekt soll historische
Dateiformate verlässlich erkennen, lesen, validieren, schreiben und – soweit
semantisch sinnvoll – ineinander überführen. Die Formatentwicklung wird
chronologisch nachvollzogen. Parallel dazu entwickelt sich die verwendete
C-/C++-Technik von einer 1990 kompatiblen Basis schrittweise bis C++20.

Dieses Dokument verwendet die Schlüsselwörter **MUSS**, **SOLL** und **KANN**:

- **MUSS** bezeichnet eine zwingende Anforderung.
- **SOLL** bezeichnet eine Anforderung, von der nur mit dokumentierter
  Begründung abgewichen werden darf.
- **KANN** bezeichnet eine optionale Erweiterung.
- Jede Abweichung von einer MUSS-Anforderung erfordert eine genehmigte
  Architekturentscheidung (ADR) und eine Anpassung dieses Pflichtenhefts.

## 2. Ausgangssituation

Historische Dateien sind häufig nur noch mit nicht mehr unterstützten
Anwendungen, Betriebssystemen oder proprietären Konvertern lesbar. Selbst
gleichnamige Formate unterscheiden sich zwischen Versionen, Herstellern und
Programmen. Dateiendungen reichen daher nicht zur zuverlässigen Erkennung aus.

Als erste Forschungsgrundlage dienen insbesondere:

1. Ralf Kussmann: *Dateiformate und Konvertierung*, DATA BECKER, 1. Auflage,
   1989.
2. Günter Born: *Referenzhandbuch Dateiformate: Grafik, Text, Datenbanken,
   Tabellenkalkulation*, Addison-Wesley, 2. überarbeitete Auflage /
   1. unveränderter Nachdruck, 1992, ISBN 3-89319-446-0.
3. Zeitgenössische Herstellerunterlagen, veröffentlichte Standards,
   nachvollziehbare Dateibeispiele und experimentelle Verifikation.

Die Bücher ergänzen sich: Born liefert vor allem strukturelle Informationen,
Kussmann beschreibt zusätzlich zeitgenössische Import-, Export- und
Austauschwege. Keine einzelne Quelle gilt ungeprüft als fehlerfreie
Spezifikation.

## 3. Produktvision

SASD Moschus soll langfristig eine offene, nachvollziehbare und sichere
Werkzeugfamilie für historische und moderne Dateiformate werden.

Die Kernidee lautet:

> Historische Genauigkeit an der Dateigrenze, nachvollziehbare
> Sprachentwicklung im Quellcode und moderne Sicherheitsansprüche in jeder
> Epoche.

Moschus soll:

- historische Dateien ohne das ursprüngliche Anwendungsprogramm erschließen;
- Formatvarianten ausdrücklich unterscheiden;
- beschädigte Dateien sicher analysieren können;
- Datenverluste vor einer Konvertierung sichtbar machen;
- mehrere unabhängige Bibliotheksimplementierungen anbieten;
- einen eigenständigen C++-Kommandozeilenkonverter bereitstellen;
- die Entwicklung von C89/C90 und frühem C++ bis C++20 dokumentiert
  nachvollziehen;
- als technische und didaktische Referenz dienen.

## 4. Produktumfang und Abgrenzung

### 4.1 Im Lieferumfang

**PFL-SCP-001 (MUSS):** Die erste vollständige Produktepoche umfasst nur
Formatversionen, deren Veröffentlichung oder praktische Nutzung bis
einschließlich 31. Dezember 1990 nachgewiesen wurde.

**PFL-SCP-002 (MUSS):** Jede unterstützte Version erhält eine eindeutige,
stabile Moschus-Kennung. Eine Dateiendung darf mehrere Versionen abbilden.

**PFL-SCP-003 (MUSS):** Die Kernfunktionen sind Erkennen, Lesen, Validieren,
Schreiben und Konvertieren.

**PFL-SCP-004 (MUSS):** Die Bibliothek wird langfristig in mehreren
Programmiersprachen implementiert. Gemeinsame Formatspezifikationen und
Konformitätstests sind sprachneutral.

**PFL-SCP-005 (MUSS):** Der offizielle Kommandozeilenkonverter wird
ausschließlich in C beziehungsweise C++ entlang der festgelegten
Sprachepochen entwickelt.

**PFL-SCP-006 (SOLL):** Die erste Epoche soll auch auf zeitgenössischen
16-Bit-DOS-Werkzeugen übersetzbar und ausführbar sein, soweit die notwendigen
Compiler rechtmäßig verfügbar sind.

### 4.2 Nicht Bestandteil der Epoche 1990

**PFL-SCP-020 (MUSS):** Microsoft Access ist kein Bestandteil der
1990-Abnahme. Die später geplante Konvertierung dBASE ↔ Access gehört zu einer
nachfolgenden Formatepoche.

**PFL-SCP-021 (MUSS):** JPEG/JFIF und später eingeführte Formate oder
Formatrevisionen dürfen nicht stillschweigend in die 1990-Epoche aufgenommen
werden.

**PFL-SCP-022 (MUSS):** Moschus emuliert keine vollständigen
Anwendungsprogramme und führt keine in Dokumenten enthaltenen Makros,
Programme oder Druckerbefehle aus.

**PFL-SCP-023 (MUSS):** Nicht jede theoretische Kombination zweier Formate
muss konvertierbar sein. Konvertierungen werden nur bei sinnvoller gemeinsamer
Semantik angeboten.

**PFL-SCP-024 (MUSS):** Proprietäre Compiler, Bücher, Disketteninhalte und
nicht frei verteilbare Beispieldateien werden nicht mit dem Repository
ausgeliefert.

## 5. Begriffe

| Begriff | Bedeutung |
|---|---|
| Formatfamilie | Zusammengehörige Varianten, beispielsweise dBASE DBF |
| Formatversion | Konkrete, auf dem Datenträger unterscheidbare Ausprägung |
| Profil | Begrenzte Teilmenge oder anwendungsspezifische Ausprägung einer Version |
| Codec | Reader, Writer und Validator einer Formatversion oder eines Profils |
| Probe | Erkennung einer Formatfamilie und Version mit begründeter Sicherheit |
| neutrales Modell | Formatunabhängige semantische Darstellung eines Dokuments |
| Round-trip | Lesen, Schreiben und erneutes Lesen unter definierten Erhaltungseigenschaften |
| kanonisches Schreiben | Deterministische, dokumentierte Ausgabe ohne Anspruch auf byteidentische Reproduktion |
| strikter Modus | Ablehnung strukturell oder semantisch ungültiger Eingaben |
| Recovery-Modus | Begrenzte, diagnostizierte Gewinnung noch verwertbarer Inhalte |
| Format-Horizont | Spätestes Veröffentlichungsdatum der aufgenommenen Formatversionen |
| Sprachepoche | Für einen Projektstand festgelegter C-/C++-Sprach- und Compilerumfang |

## 6. Stakeholder und Nutzergruppen

- **Product Owner:** priorisiert Formatfamilien, genehmigt Scope- und
  Architekturänderungen und nimmt Meilensteine ab.
- **Bibliotheksnutzer:** integrieren Reader, Writer und Validatoren in eigene
  Programme.
- **Konverternutzer:** analysieren und konvertieren Dateien über die
  Kommandozeile.
- **Archivare und Datenretter:** benötigen sichere Erkennung, Validierung,
  Provenienz und Recovery-Diagnosen.
- **Entwickler und Forschende:** ergänzen Spezifikationen, Codecs und
  Testmaterial.
- **Maintainer weiterer Sprachen:** implementieren dieselben Verträge idiomatisch
  in C#, Java und späteren Sprachen.

## 7. Architekturvorgaben

### 7.1 Schichten

**PFL-ARC-001 (MUSS):** Die Architektur besteht mindestens aus:

1. Quellen- und Spezifikationsschicht;
2. portablen Byte-, Text- und Ressourcenprimitiven;
3. Formaterkennung;
4. Readern, Writern und Validatoren;
5. neutralen Domänenmodellen;
6. Konvertierungsplanung und Verlustanalyse;
7. öffentlichen Sprach-APIs;
8. C++-Konverter;
9. gemeinsamer Konformitätssuite.

**PFL-ARC-002 (MUSS):** Spezifikationen und Konformitätsdaten dürfen von keiner
konkreten Sprachimplementierung abhängen.

**PFL-ARC-003 (MUSS):** Der Konverter darf keine eigenen privaten Parser
enthalten. Er benutzt ausschließlich die öffentliche API der jeweils aktiven
C-/C++-Bibliothek.

**PFL-ARC-004 (MUSS):** Direkte paarweise Konverter werden vermieden. Reader
und Writer koppeln über neutrale Domänenmodelle.

**PFL-ARC-005 (MUSS):** Compiler- und Plattformunterschiede werden in einer
zentralen Kompatibilitätsschicht gekapselt. Compilerbedingte Präprozessorzweige
dürfen nicht unkontrolliert über die Codecs verteilt werden.

**PFL-ARC-006 (SOLL):** Ein Codec soll weitgehend aus portablem,
plattformunabhängigem Code bestehen.

**PFL-ARC-007 (MUSS):** Abhängigkeiten verlaufen ausschließlich in folgender
Richtung:

```text
Konverter
   |
öffentliche C-/C++-API
   |
Codec-Verträge ------ Diagnosen
   |                      |
Domänenmodelle       Ressourcenlimits
   |                      |
portable Byte-/Text- und Plattformprimitive
   |
sprachneutrale Spezifikationen + Konformitätsmanifeste
```

### 7.2 Neutrale Domänenmodelle

**PFL-MOD-001 (MUSS):** Für tabellarische Formate existiert ein Modell für
Tabellen, Spalten, Feldtypen, Werte, Null-/Leerzustände, gelöschte Datensätze,
Formeln, Formatierungen und herstellerspezifische Metadaten.

**PFL-MOD-002 (MUSS):** Für Textdokumente existiert ein Modell für
Dokumentstruktur, Absätze, Zeichenläufe, Formatvorlagen, Felder, Kopf- und
Fußbereiche, Tabellen, Fußnoten und eingebettete Objekte. Noch nicht
implementierte Eigenschaften müssen als Fähigkeiten ausgewiesen werden.

**PFL-MOD-003 (MUSS):** Für Rastergrafiken existiert ein Modell für
Abmessungen, Farbmodell, Palette, Pixeldaten, Auflösung, Bildfolgen und
Metadaten.

**PFL-MOD-004 (MUSS):** Für Vektor- und Metafile-Formate existiert ein Modell
für Koordinatensystem, Einheiten, Zeichenoperationen, Pfade, Farben, Schriften,
Rastereinbettungen und Ressourcen.

**PFL-MOD-005 (SOLL):** Chunk-basierte Medien erhalten ein gemeinsames
Container- und Chunk-Modell, sofern mehrere Formate davon profitieren.

**PFL-MOD-006 (MUSS):** Quellformatspezifische Informationen dürfen in einem
kontrollierten Erweiterungsbereich erhalten werden. Sie dürfen die gemeinsamen
semantischen Felder nicht ersetzen.

**PFL-MOD-007 (MUSS):** Jede Eigenschaft muss ihre Herkunft und ihren
Erhaltungsstatus abbilden können: exakt, normalisiert, angenähert, verworfen,
unbekannt oder ungültig.

## 8. Anforderungen an Formatwissen und Quellen

**PFL-SRC-001 (MUSS):** Jede technische Behauptung in einer Spezifikation
enthält mindestens eine Quellenangabe oder eine Kennzeichnung als
experimentelle Erkenntnis beziehungsweise begründete Annahme.

**PFL-SRC-002 (MUSS):** Quellen werden mit genauer Ausgabe, Revision,
Seitenbereich und Zugriffsstatus dokumentiert.

**PFL-SRC-003 (MUSS):** Widersprechen sich Quellen, darf keine davon
stillschweigend bevorzugt werden. Der Konflikt und die Entscheidung werden
dokumentiert.

**PFL-SRC-004 (MUSS):** Informationen aus späteren Auflagen dürfen nicht ohne
Nachweis einer früheren Gültigkeit einer 1990-Version zugeschrieben werden.

**PFL-SRC-005 (MUSS):** Scans, längere Textübernahmen, Tabellen,
Programm-Listings und Disketteninhalte der Bücher werden nicht in das
Repository aufgenommen, sofern keine eigenständige Erlaubnis vorliegt.

**PFL-SRC-006 (SOLL):** Wo verfügbar, werden Herstellerunterlagen oder
veröffentlichte Standards als Primärquellen herangezogen.

**PFL-SRC-007 (MUSS):** Testdateien enthalten Provenienz, Lizenz-/Freigabestatus
und kryptografischen Hash.

**PFL-SRC-008 (MUSS):** Eine private Forschungsdatei darf lokal verwendet
werden, aber nicht versehentlich durch Tests, Artefakte oder Logs veröffentlicht
werden.

## 9. Formatregister und Erkennung

**PFL-DET-001 (MUSS):** Ein zentrales Formatregister verwaltet Familien,
Versionen, Profile, Dateiendungen, Signaturen, Fähigkeiten und Status.

**PFL-DET-002 (MUSS):** Die Erkennung darf eine Dateiendung nur als schwaches
Indiz behandeln.

**PFL-DET-003 (MUSS):** Eine Probe liefert mindestens Kandidat, erkannte
Version, Sicherheit, verwendete Indizien und widersprechende Indizien.

**PFL-DET-004 (MUSS):** Mehrdeutige Erkennung wird als mehrdeutig gemeldet und
nicht willkürlich aufgelöst.

**PFL-DET-005 (MUSS):** Die Probe liest nur eine begrenzte Datenmenge und
beachtet alle Ressourcenlimits.

**PFL-DET-006 (SOLL):** Formatfamilien können eine vertiefte Probe anbieten,
wenn die Basiserkennung nicht genügt.

**PFL-DET-007 (MUSS):** Ein vom Nutzer erzwungenes Quellformat wird weiterhin
gegen die Eingabe geprüft; Widersprüche werden gemeldet.

## 10. Lesen, Validieren, Recovery und Schreiben

### 10.1 Reader

**PFL-REA-001 (MUSS):** Jeder Reader prüft sämtliche Längen-, Offset- und
Indexberechnungen vor dem Zugriff.

**PFL-REA-002 (MUSS):** Reader arbeiten stromorientiert, sofern das Format
keinen zwingenden wahlfreien Zugriff verlangt.

**PFL-REA-003 (MUSS):** Ein Reader unterscheidet Dateiende, abgeschnittene
Struktur, ungültigen Wert, nicht unterstützte Funktion und Ressourcenlimit.

**PFL-REA-004 (MUSS):** Zeichenkodierung, Zeilenenden, Datumsdarstellung,
Zahlenformat und Byte-Reihenfolge werden explizit behandelt.

**PFL-REA-005 (SOLL):** Unbekannte, aber sicher überspringbare Records oder
Chunks können zur späteren Ausgabe erhalten werden.

### 10.2 Validator

**PFL-VAL-001 (MUSS):** Strukturprüfung und semantische Prüfung sind getrennt
auswertbar.

**PFL-VAL-002 (MUSS):** Eine Diagnose enthält Code, Schweregrad,
Dateiposition, Kontext, verständliche Meldung und – soweit möglich –
Behebungshinweis.

**PFL-VAL-003 (MUSS):** Validierung verändert die Eingabedatei niemals.

**PFL-VAL-004 (MUSS):** Der strikte Modus akzeptiert nur die dokumentierten
Regeln der erkannten Version beziehungsweise des gewählten Profils.

### 10.3 Recovery

**PFL-REC-001 (MUSS):** Recovery ist ein ausdrücklich gewählter Betriebsmodus.

**PFL-REC-002 (MUSS):** Recovery darf beschädigte Eingaben nicht als gültig
ausgeben.

**PFL-REC-003 (MUSS):** Jede ausgelassene, ersetzte oder rekonstruierte
Datenmenge erzeugt eine Diagnose.

**PFL-REC-004 (MUSS):** Recovery unterliegt denselben Sicherheits- und
Ressourcengrenzen wie der strikte Modus.

### 10.4 Writer

**PFL-WRI-001 (MUSS):** Ein Writer verlangt eine konkrete Zielversion oder ein
eindeutig konfiguriertes Standardprofil.

**PFL-WRI-002 (MUSS):** Ein Writer darf keine neuere Formaterweiterung
stillschweigend in eine historische Zieldatei schreiben.

**PFL-WRI-003 (MUSS):** Die Ausgabe ist bei identischem Modell und identischen
Optionen deterministisch, sofern das Format dies zulässt.

**PFL-WRI-004 (MUSS):** Nicht darstellbare Eigenschaften werden vor dem
Schreiben gemeldet.

**PFL-WRI-005 (MUSS):** Dateien werden zunächst in eine temporäre Zieldatei
geschrieben und erst nach erfolgreichem Abschluss ersetzt. Bestehende Dateien
werden ohne ausdrückliche Freigabe nicht überschrieben.

**PFL-WRI-006 (SOLL):** Writer unterstützen ein kanonisches Ausgabeprofil und,
soweit sinnvoll, ein quellenorientiertes Erhaltungsprofil.

## 11. Konvertierung

**PFL-CON-001 (MUSS):** Vor jeder Konvertierung wird ein Konvertierungsplan
erstellt.

**PFL-CON-002 (MUSS):** Der Plan vergleicht Quellfähigkeiten, Modellinhalt und
Zielfähigkeiten.

**PFL-CON-003 (MUSS):** Datenverluste werden vor Erzeugung der Zieldatei
klassifiziert und gemeldet.

**PFL-CON-004 (MUSS):** Standardmäßig wird eine verlustbehaftete Konvertierung
abgebrochen.

**PFL-CON-005 (MUSS):** Der Nutzer kann Verlust mit einer ausdrücklichen Option
akzeptieren. Die Diagnose bleibt Bestandteil des Ergebnisses.

**PFL-CON-006 (MUSS):** Ein direkter Byte-zu-Byte-Konverter darf nur als
begründete, dokumentierte Ausnahme existieren.

**PFL-CON-007 (SOLL):** Konvertierungen sollen reproduzierbar sein und keine
zeitabhängigen Werte einfügen, sofern dies nicht ausdrücklich gewünscht wird.

**PFL-CON-008 (MUSS):** Die Bibliothek stellt Konvertierungsdiagnosen
strukturiert bereit; der CLI-Konverter bietet menschen- und
maschinenlesbare Ausgabe.

## 12. C-/C++-Sprach- und Compilerstrategie

### 12.1 Epoche 1990

**PFL-LNG-001 (MUSS):** Der gemeinsame portable Kern der 1990-Epoche wird in
ANSI C89/ISO C90 geschrieben.

**PFL-LNG-002 (MUSS):** Der Kern muss ohne C99-Funktionen, Variable Length
Arrays, `//`-Kommentare, `stdint.h` und andere spätere Sprachmerkmale
auskommen.

**PFL-LNG-003 (MUSS):** Fehlende feste Ganzzahltypen werden in einer
zentralen, größenverifizierten Kompatibilitätsschicht definiert.

**PFL-LNG-004 (MUSS):** Der Kern wird mindestens mit einem aktuellen GCC im
strikten C90-Modus automatisiert gebaut und getestet.

**PFL-LNG-005 (SOLL):** Der Kern wird zusätzlich mit einer festgelegten
Turbo-C-/Turbo-C++-Version und Microsoft C 6.0 unter DOS beziehungsweise OS/2
gebaut. Die genaue Werkzeugmatrix wird in ADR-0002 fixiert.

**PFL-LNG-006 (MUSS):** Der Konverter ist ein C++-Programm. Für die
1990-Epoche benutzt er nur den nach ADR-0002 festgelegten, gemeinsam
unterstützten Teil früher C++-Compiler.

**PFL-LNG-007 (MUSS):** Kann ein 1990er Microsoft-C-Compiler den C++-Konverter
nicht übersetzen, bleibt er verbindliches Ziel für den C89-Kern. Ein passender
Microsoft-C++-Compiler wird erst ab seiner historisch korrekten Epoche
aufgenommen.

**PFL-LNG-008 (MUSS):** Proprietäre Compiler werden weder eingecheckt noch von
öffentlichen CI-Jobs heruntergeladen. Build-Anleitungen und lokale
Prüfskripte dürfen bereitgestellt werden.

**PFL-LNG-009 (MUSS):** 16-Bit-DOS-Unterstützung darf keine einzelne
dynamische Allokation voraussetzen, die nicht im festgelegten Speichermodell
darstellbar ist. Große Dateien werden block-, zeilen-, record- oder
chunkweise verarbeitet.

**PFL-LNG-010 (SOLL):** Für DOS wird ein reproduzierbares Quellpaket mit
8.3-kompatiblen Dateinamen und einer Zuordnung zum kanonischen Repositorypfad
erzeugt. Das Hauptrepository muss nicht auf 8.3-Namen beschränkt werden.

### 12.2 Bedingte Übersetzung

**PFL-LNG-020 (MUSS):** Compilererkennung und Erweiterungen werden unter
`platform/` beziehungsweise in dedizierten Compatibility-Headern gebündelt.

**PFL-LNG-021 (MUSS):** Projektmakros beginnen mit `MOSCHUS_`.

**PFL-LNG-022 (MUSS):** Compilerzweige besitzen eine dokumentierte
Fallback- oder Fehlerstrategie.

**PFL-LNG-023 (MUSS):** Ein unbekannter Compiler darf nicht stillschweigend
mit ungeprüften Annahmen übersetzen.

**PFL-LNG-024 (SOLL):** Formatcodec-Dateien enthalten keine
Compilererkennung, sofern dies nicht technisch unvermeidbar und in einem ADR
begründet ist.

### 12.3 Spätere C++-Epochen

**PFL-LNG-030 (MUSS):** Nach Abnahme der 1990-Epoche wird der reproduzierbare
Stand getaggt, bevor die Mindestanforderung auf C++98 angehoben wird.

**PFL-LNG-031 (MUSS):** Die vorgesehenen Sprachstufen sind C++98, C++03,
C++11, C++14, C++17 und C++20. Keine Stufe wird ohne eigenen Migrations- und
Abnahmeschritt übersprungen.

**PFL-LNG-032 (MUSS):** Alte Formatversionen bleiben auch nach einer
Sprachmigration unterstützt und durch Regressionstests geschützt.

**PFL-LNG-033 (MUSS):** Sprachmodernisierung und Aufnahme neuer Formate werden
in getrennten Commits und möglichst getrennten Meilensteinen durchgeführt.

**PFL-LNG-034 (SOLL):** Ein historischer Wartungszweig kann für kritische
Korrekturen erhalten bleiben; maßgeblich für die weitere Entwicklung ist
`main`.

**PFL-LNG-035 (MUSS):** C#- und Java-Implementierungen sind nicht Teil der
1990-Abnahme. Ihr Einstieg und ihre jeweilige Mindestversion werden in
späteren ADRs festgelegt.

## 13. Öffentliche Bibliotheks-APIs

**PFL-API-001 (MUSS):** Jede Sprachimplementierung bietet äquivalente
Formatkennungen, Diagnoseschweregrade, Fähigkeitsabfragen und Ergebniszustände.

**PFL-API-002 (MUSS):** Öffentliche APIs dürfen keine ungeprüften rohen
Zeiger, internen Dateihandles oder compilerabhängigen Strukturen offenlegen.

**PFL-API-003 (MUSS):** Parsing-Ergebnis, Diagnosen und Abbruchursache müssen
voneinander unterscheidbar sein.

**PFL-API-004 (MUSS):** Ein Aufrufer kann Ressourcenlimits pro Operation
vorgeben.

**PFL-API-005 (SOLL):** Reader und Writer akzeptieren Streams beziehungsweise
Callbacks, damit große Dateien und nicht-dateibasierte Quellen möglich sind.

**PFL-API-006 (MUSS):** ABI-Stabilität wird erst ab einem ausdrücklich
gekennzeichneten stabilen Release zugesagt.

**PFL-API-007 (MUSS):** Jede öffentliche Funktion und jeder öffentliche Typ
wird dokumentiert.

**PFL-API-008 (SOLL):** APIs folgen den Konventionen ihrer Sprache und müssen
nicht syntaktisch identisch sein.

## 14. Kommandozeilenkonverter

Der Programmname lautet `moschus`.

### 14.1 Befehle

**PFL-CLI-001 (MUSS):** `moschus formats` listet bekannte Familien,
Versionen, Profile und Fähigkeiten.

**PFL-CLI-002 (MUSS):** `moschus info <datei>` erkennt Format und Version und
gibt Struktur-, Metadaten- und Erkennungsinformationen aus.

**PFL-CLI-003 (MUSS):** `moschus validate <datei>` führt strukturierte
Validierung aus.

**PFL-CLI-004 (MUSS):** `moschus convert <quelle> --to <format:version>
--output <ziel>` konvertiert über ein neutrales Modell.

**PFL-CLI-005 (SOLL):** `moschus probe <datei>` zeigt alle
Erkennungskandidaten und Indizien.

**PFL-CLI-006 (KANN):** `moschus recover` kann nach Stabilisierung des
Recovery-Vertrags als eigener Befehl ergänzt werden.

### 14.2 Globale Eigenschaften

**PFL-CLI-010 (MUSS):** Textausgabe ist für Menschen lesbar; `--json` liefert
eine stabile, versionierte Maschinenstruktur.

**PFL-CLI-011 (MUSS):** Ohne `--force` wird keine bestehende Zieldatei
überschrieben.

**PFL-CLI-012 (MUSS):** Verlustpolitik ist über
`--loss-policy=fail|warn|allow` steuerbar; Standard ist `fail`.

**PFL-CLI-013 (MUSS):** Strikter Modus ist Standard. Recovery muss ausdrücklich
aktiviert werden.

**PFL-CLI-014 (MUSS):** Pfade, Dateinamen und Diagnoseausgaben behandeln die
jeweilige Plattformkodierung nachvollziehbar.

**PFL-CLI-015 (MUSS):** Folgende Exit-Code-Klassen werden stabil definiert:

| Code | Bedeutung |
|---:|---|
| 0 | erfolgreich |
| 1 | ungültige Kommandozeile |
| 2 | unbekanntes oder nicht unterstütztes Format |
| 3 | ungültige oder beschädigte Eingabe |
| 4 | abgelehnter Datenverlust |
| 5 | Ein-/Ausgabefehler |
| 6 | Ressourcen- oder Sicherheitsgrenze |
| 7 | interner Fehler |

Historische Plattformen dürfen technisch bedingt Codes zusammenfassen; diese
Abweichung muss dokumentiert sein.

## 15. Geplanter Formatumfang der Epoche 1990

Die endgültige Aufnahme erfolgt ausschließlich über die
Formatabdeckungsmatrix. Folgende Familien bilden den Forschungskandidatenraum:

### 15.1 Tabellen und Austausch

- ASCII DELIMITED;
- SDF;
- zeitgenössische CSV-Profile;
- DIF;
- SDI und SIF, sofern ausreichend spezifizierbar;
- SYLK einschließlich klar abgegrenzter Erweiterungen;
- Lotus WKS/WK1 und nachweislich zeitgerechte 1-2-3-Varianten;
- weitere in den Referenzen belegte Austauschformate.

### 15.2 Datenbanken

- dBASE II DBF und bekannte Begleitdateien;
- dBASE III und III Plus DBF, DBT, NDX und belegte Varianten;
- dBASE-IV-Versionen bis zum Stichtag;
- Clipper-Varianten nur mit eigener Kennung und ausreichenden Testdaten.

### 15.3 Text und Dokumente

- Microsoft Word 3.0, 4.0 und 5.0, soweit Struktur und Version sicher
  unterscheidbar sind;
- WordStar-Varianten bis zum Stichtag;
- WordPerfect-Varianten bis zum Stichtag;
- RTF 1.0;
- DCA/RFT;
- SGML-Profile nur bei klarer Abgrenzung von Parser, DTD und
  Anwendungskonvention.

### 15.4 Rastergrafik und Chunk-Formate

- PCX;
- GEM IMG;
- IFF-Unterformate bis zum Stichtag, beispielsweise ILBM, wenn verifiziert;
- GIF87a und GIF89a;
- TIFF-Revisionen bis zum Stichtag;
- frühe Windows- und OS/2-Bitmap- beziehungsweise Icon-Formate.

### 15.5 Vektor, Metafile und Druck

- GEM Metafile;
- zeitgerechte CGM-Profile;
- WPG;
- DXF und DXB;
- frühe WMF-Profile;
- HP-GL;
- zeitgerechte PCL-Profile;
- EPS/PostScript-Profile ohne Ausführung eingebetteter Programme.

**PFL-FMT-001 (MUSS):** Jede materiell unterschiedliche On-Disk-Version erhält
eine eigene Zeile in der Abdeckungsmatrix.

**PFL-FMT-002 (MUSS):** Der Status wird getrennt für Spezifikation, Lesen,
Schreiben, Round-trip, Konvertierung und Stabilität geführt.

**PFL-FMT-003 (MUSS):** „Unterstützt“ darf nur verwendet werden, wenn alle im
jeweiligen Status geforderten Nachweise vorhanden sind.

**PFL-FMT-004 (MUSS):** Nicht belegbare oder nicht zuverlässig testbare
Varianten werden zurückgestellt statt erraten.

## 16. Zeichenkodierungen und historische Darstellung

**PFL-ENC-001 (MUSS):** Interne Textrepräsentation und externe historische
Kodierung werden getrennt behandelt.

**PFL-ENC-002 (MUSS):** Die Quelle einer Kodierungsannahme wird dokumentiert:
explizites Feld, Formatversion, Programmprofil, Nutzerangabe oder Heuristik.

**PFL-ENC-003 (MUSS):** Eine Heuristik darf nie als sichere Erkennung
ausgegeben werden.

**PFL-ENC-004 (MUSS):** Nicht darstellbare Zeichen erzeugen vor dem Schreiben
eine Diagnose.

**PFL-ENC-005 (SOLL):** Häufige DOS-Codepages und zeitgenössische
Anwendungstabellen werden als versionierte Zuordnungen gepflegt.

**PFL-ENC-006 (MUSS):** Zeilenenden, Ersatzzeichen und Normalisierung werden
nicht stillschweigend verändert.

## 17. Sicherheitsanforderungen

Alle Eingaben gelten als nicht vertrauenswürdig.

**PFL-SEC-001 (MUSS):** Ganzzahlüberläufe bei Länge, Offset, Anzahl,
Multiplikation und Addition werden vor der Operation verhindert.

**PFL-SEC-002 (MUSS):** Speicher-, Record-, Chunk-, Bildgrößen-, Rekursions-,
Verweis- und Dekompressionsgrenzen sind konfigurierbar und besitzen sichere
Standardwerte.

**PFL-SEC-003 (MUSS):** Kein Codec führt Makros, Skripte, Druckerbefehle,
externe Programme oder eingebettete Binärdateien aus.

**PFL-SEC-004 (MUSS):** Diagnose- und JSON-Ausgabe maskieren Steuerzeichen und
dürfen Terminalsequenzen aus Eingabedaten nicht ungeprüft ausgeben.

**PFL-SEC-005 (MUSS):** Temporäre Dateien werden sicher erzeugt und bei
Fehlschlag nach Möglichkeit entfernt.

**PFL-SEC-006 (MUSS):** Der Converter folgt keinen in Dokumenten enthaltenen
externen Verweisen ohne ausdrückliche zukünftige Funktion und Sicherheitsregel.

**PFL-SEC-007 (SOLL):** Moderne Builds werden regelmäßig mit Sanitizern,
statischer Analyse und Fuzzing geprüft.

**PFL-SEC-008 (MUSS):** Ein Fund aus Fuzzing oder Sicherheitsanalyse erhält
einen dauerhaften Regressionstest, soweit die Datei rechtmäßig eingebracht
werden kann.

## 18. Nichtfunktionale Anforderungen

### 18.1 Portabilität

**PFL-NFR-001 (MUSS):** Der C89-Kern vermeidet Annahmen über die Größe von
`char`, `short`, `int`, `long`, Zeigern und Dateioffsets.

**PFL-NFR-002 (MUSS):** Byte-Reihenfolge und Datenlayout werden explizit
kodiert; Dateistrukturen werden nicht durch ungeprüftes Casting auf
Compiler-Structs gelesen.

**PFL-NFR-003 (MUSS):** Compilerpacking darf nur in isolierten Tests oder
Adapterstrukturen verwendet werden, niemals als alleinige Beschreibung eines
Dateiformats.

**PFL-NFR-004 (SOLL):** Moderne Builds unterstützen mindestens Linux und
Windows. macOS und BSD-Systeme werden aufgenommen, sobald der Buildkern stabil
ist.

### 18.2 Speicher und Leistung

**PFL-NFR-010 (MUSS):** Die Speicherkomplexität ist pro Codec dokumentiert.

**PFL-NFR-011 (MUSS):** Dateien, Tabellen und Bilder werden nicht allein wegen
ihrer Gesamtgröße vollständig geladen, wenn eine Streaming-Lösung möglich ist.

**PFL-NFR-012 (SOLL):** Das DOS16-Profil begrenzt reguläre Arbeitsblöcke auf
einen in ADR-0002 festgelegten sicheren Wert unterhalb der Segmentgrenze.

**PFL-NFR-013 (SOLL):** Für moderne Systeme wird ein reproduzierbarer
Benchmarkkorpus eingerichtet; Optimierung darf Korrektheit und
Nachvollziehbarkeit nicht verschlechtern.

### 18.3 Wartbarkeit

**PFL-NFR-020 (MUSS):** Codeänderungen sind klein, überprüfbar und bauen auf
dem jeweiligen Branch vollständig.

**PFL-NFR-021 (MUSS):** Nicht offensichtliche Format-, Sicherheits- und
Kompatibilitätsentscheidungen werden im Code ausführlich auf Englisch
kommentiert.

**PFL-NFR-022 (MUSS):** Öffentliche Typen und Funktionen erhalten
API-Dokumentation.

**PFL-NFR-023 (MUSS):** Compilerwarnungen werden für unterstützte moderne
Toolchains als Fehler behandelt. Historische Compilerabweichungen werden
dokumentiert.

**PFL-NFR-024 (SOLL):** Formatfamilien folgen einer wiedererkennbaren
Verzeichnis- und Dateistruktur.

### 18.4 Reproduzierbarkeit

**PFL-NFR-030 (MUSS):** Releasequellen, generierte DOS-Quellpakete,
Konformitätsmanifeste und Testkorpusstände erhalten Hashes.

**PFL-NFR-031 (MUSS):** Generierte Dateien werden aus nachvollziehbaren
Skripten erzeugt und nicht manuell nachbearbeitet.

**PFL-NFR-032 (SOLL):** Builds derselben Toolchain und Konfiguration sollen
reproduzierbare Binärdateien erzeugen, soweit Zeitstempel und historische
Werkzeuge dies erlauben.

## 19. Test- und Qualitätssicherung

### 19.1 Testarten

**PFL-TST-001 (MUSS):** Jeder Codec besitzt Unit-Tests für Primitive,
Header, Records, Grenzen und Fehlerfälle.

**PFL-TST-002 (MUSS):** Die sprachneutrale Konformitätssuite prüft alle
Bibliotheksimplementierungen gegen dieselben semantischen Erwartungen.

**PFL-TST-003 (MUSS):** Für jede unterstützte Version existieren mindestens:

- eine minimale gültige Datei;
- eine repräsentative gültige Datei;
- Grenzwertfälle;
- eine abgeschnittene Datei;
- eine strukturell ungültige Datei;
- eine Datei mit unbekannter, aber sicher überspringbarer Struktur, sofern das
  Format dies erlaubt;
- definierte Round-trip-Erwartungen.

**PFL-TST-004 (MUSS):** Reader und Writer werden getrennt sowie gemeinsam im
Round-trip getestet.

**PFL-TST-005 (MUSS):** Round-trip bedeutet nicht automatisch
Byteidentität. Die zu erhaltenden Eigenschaften werden pro Test ausdrücklich
definiert.

**PFL-TST-006 (SOLL):** Moderne Parserbuilds werden kontinuierlich gefuzzt.

**PFL-TST-007 (SOLL):** Wo rechtlich und technisch möglich, werden Dateien mit
Originalanwendungen unter Emulatoren erzeugt und anschließend geprüft.

**PFL-TST-008 (MUSS):** Tests dürfen keine proprietären Compiler oder
Anwendungsprogramme aus dem Internet nachladen.

### 19.2 Compiler- und Plattformmatrix der 1990-Epoche

| Ziel | Automatisierung | Abnahmestatus |
|---|---|---|
| aktueller GCC, striktes C90 | öffentliche CI | MUSS |
| aktueller GCC/G++, begrenztes frühes C++-Profil | öffentliche CI oder Kompatibilitätsbuild | MUSS |
| Turbo C oder Turbo C++ unter DOS | lokale/emulierte Prüfung | SOLL, vor 1990-Vollabnahme möglichst MUSS nach ADR |
| Microsoft C 6.0 unter DOS/OS/2 | lokale/emulierte Prüfung | SOLL, vor 1990-Vollabnahme möglichst MUSS nach ADR |
| moderne Sanitizer-Toolchain | öffentliche CI | MUSS für Hosttests |

**PFL-TST-020 (MUSS):** Manuelle Retro-Builds werden mit Werkzeugversion,
Befehlen, Umgebung und Ergebnis protokolliert.

**PFL-TST-021 (MUSS):** Eine nicht verfügbare proprietäre Toolchain darf
moderne CI nicht blockieren, verhindert aber den entsprechenden
Kompatibilitätsnachweis.

### 19.3 Qualitätsgrenzen

**PFL-TST-030 (MUSS):** Auf `main` dürfen keine bekannten fehlschlagenden
Pflichttests vorhanden sein.

**PFL-TST-031 (MUSS):** Kein Release erfolgt mit bekannten kritischen oder
hohen, ausnutzbaren Parserfehlern.

**PFL-TST-032 (MUSS):** Jede behobene Regression erhält einen Test.

**PFL-TST-033 (SOLL):** Abdeckung wird gemessen, aber nicht durch eine einzelne
Prozentzahl ersetzt. Kritische Parserpfade benötigen vollständige
Grenzfalltests.

## 20. Build, Pakete und Repositorystruktur

Die Zielstruktur lautet:

```text
SASD-Moschus/
├── libraries/
│   ├── c89/                 portabler Kern der Epoche 1990
│   ├── cpp/                 wachsende C++-API und spätere Referenzbibliothek
│   ├── csharp/              spätere native .NET-Implementierung
│   └── java/                spätere native Java-Implementierung
├── platform/                zentrale Compiler-, OS- und DOS-Kompatibilität
├── tools/
│   └── converter-cpp/       alleiniger offizieller CLI-Konverter
├── specifications/          sprachneutrale Formatspezifikationen
├── tests/
│   ├── conformance/
│   └── corpus/
├── examples/
├── docs/
│   ├── sources/
│   └── format-coverage.md
├── ARCHITECTURE.md
├── ROADMAP.md
└── PFLICHTENHEFT.md
```

**PFL-BLD-001 (MUSS):** Moderne Builds erhalten eine dokumentierte
Ein-Befehl-Konfiguration und einen Ein-Befehl-Testlauf.

**PFL-BLD-002 (MUSS):** Historische Builds erhalten getrennte, einfache
Builddateien und dürfen moderne Buildsysteme nicht voraussetzen.

**PFL-BLD-003 (SOLL):** CMake wird für moderne C-/C++-Builds verwendet.
Historische DOS-Builds können Makefiles oder Compilerskripte verwenden.

**PFL-BLD-004 (MUSS):** Generierte 8.3-Quellpakete enthalten eine
Zuordnungsdatei und dürfen nicht zur zweiten, manuell gepflegten Codebasis
werden.

**PFL-BLD-005 (MUSS):** Compiler- und Plattformfähigkeiten werden durch
Konfigurationstests oder explizite Profile bestimmt, nicht allein anhand
ungeprüfter Versionsnummern.

## 21. Dokumentation

**PFL-DOC-001 (MUSS):** README und öffentliche Entwicklerdokumentation sind
auf Englisch. Das Pflichtenheft darf als maßgebliche deutsche
Projektbeschreibung geführt werden.

**PFL-DOC-002 (MUSS):** Jede Formatversion erhält Dokumentation zu Erkennung,
Struktur, unterstützten Eigenschaften, Einschränkungen, Quellen und
Testnachweisen.

**PFL-DOC-003 (MUSS):** Jede CLI-Option wird mit Beispiel, Standardwert,
Fehlerverhalten und Seiteneffekten beschrieben.

**PFL-DOC-004 (MUSS):** Jede Sprachepoche erhält eine Migrationsnotiz mit neu
verwendeten Sprachmitteln, entfallenen Compilern und Kompatibilitätsfolgen.

**PFL-DOC-005 (MUSS):** Architekturentscheidungen werden als nummerierte ADRs
unter `docs/adr/` geführt.

**PFL-DOC-006 (SOLL):** Benutzerhandbuch und Formatdokumentation sollen später
in deutscher und englischer Sprache verfügbar sein.

## 22. Versionierung und Releases

**PFL-REL-001 (MUSS):** Produktversion, Format-Horizont und Sprachepoche werden
getrennt ausgewiesen.

Beispiel:

```text
Moschus 0.9.0
Format horizon: 1990-12-31
Language epoch: C89 / pre-standard C++
```

**PFL-REL-002 (MUSS):** Öffentliche Bibliotheksversionen folgen Semantic
Versioning, sobald die jeweilige API als stabil erklärt wurde.

**PFL-REL-003 (MUSS):** Formatkennungen sind stabil und werden nicht für eine
andere Bedeutung wiederverwendet.

**PFL-REL-004 (MUSS):** Historische Abnahmepunkte erhalten signierte oder
nachvollziehbar erzeugte Git-Tags, beispielsweise:

- `format-era-1990`;
- `language-era-cpp98`;
- `language-era-cpp03`;
- `language-era-cpp11`;
- `language-era-cpp14`;
- `language-era-cpp17`;
- `language-era-cpp20`.

**PFL-REL-005 (MUSS):** Ein Release enthält Quellcode, Prüfsummen,
Supportmatrix, bekannte Einschränkungen, Buildanleitung und Release Notes.

## 23. Meilensteine

Die Zahlen sind Planwerte für kleine, überprüfbare Commits.

| Meilenstein | Inhalt | Kumulierte Größenordnung |
|---|---|---:|
| M0 | Pflichtenheft, ADRs, Quellen- und Formatmatrix | 35–50 |
| M1 | C89/C90-Kern, Compilerabstraktion, DOS16-Profil | 90–130 |
| M2 | ASCII DELIMITED, SDF, CSV und tabellarisches Modell | 140–190 |
| M3 | dBASE II–IV einschließlich priorisierter Begleitdateien | 230–300 |
| M4 | DIF, SYLK und Lotus-Formate | 310–390 |
| M5 | Word, WordStar, WordPerfect, RTF und DCA/RFT | 430–540 |
| M6 | PCX, IMG, IFF, GIF, TIFF, BMP und ICO | 540–670 |
| M7 | GEM, CGM, WPG, DXF/DXB, WMF, HP-GL, PCL und EPS | 650–780 |
| M8 | Converter-Vollständigkeit, Retro-Builds, Fuzzing und 1990-Abnahme | 750–900 |
| M9 | kontrollierte Migration auf C++98 | nach 1990-Abnahme |
| M10+ | C++03 bis C++20 und spätere Formatepochen | separate Planung |

## 24. Liefergegenstände der 1990-Abnahme

Die Epoche 1990 gilt nur dann als abgeschlossen, wenn folgende Gegenstände
vorliegen:

1. freigegebene Format- und Versionsmatrix;
2. dokumentierte Quellenlage je unterstützter Version;
3. sprachneutrale Spezifikationen;
4. portabler C89/C90-Kern;
5. C++-Konverter mit den Pflichtbefehlen;
6. mindestens der verbindlich festgelegte Satz stabiler Reader und Writer;
7. Validatoren und strukturierte Diagnosen;
8. Konvertierungs- und Verlustanalyse;
9. gemeinsamer, lizenzrechtlich sauberer Testkorpus;
10. Konformitätsmanifeste und bestandene Pflichttests;
11. dokumentierte GCC- und Retro-Compilerergebnisse gemäß ADR-0002;
12. Sicherheits- und Fuzzingbericht für moderne Builds;
13. Benutzer-, API-, Format- und Builddokumentation;
14. Release Notes, Prüfsummen und Tag `format-era-1990`.

## 25. Abnahmekriterien

**PFL-ACC-001:** Jede als „Stable“ gekennzeichnete Formatversion erfüllt ihre
Spezifikation, Reader-, Writer-, Validierungs-, Round-trip- und
Konvertierungstests.

**PFL-ACC-002:** Eine Datei mit unbekanntem oder mehrdeutigem Format wird nicht
als sicher erkannt ausgegeben.

**PFL-ACC-003:** Kein Pflicht-Writer erzeugt unbemerkt Eigenschaften einer
späteren Formatversion.

**PFL-ACC-004:** Verlustbehaftete Konvertierungen scheitern ohne ausdrückliche
Freigabe.

**PFL-ACC-005:** Fehlerhafte Längen, Offsets, Zähler und
Dekompressionsangaben führen zu einer kontrollierten Diagnose, nicht zu
Speicherfehlern oder unkontrollierter Laufzeit.

**PFL-ACC-006:** Der moderne GCC-C90-Build und alle Host-Pflichttests laufen
erfolgreich.

**PFL-ACC-007:** Die in ADR-0002 als verbindlich eingestuften Retro-Compiler
bauen die dafür vorgesehenen Ziele erfolgreich oder die Abnahme wird
ausdrücklich mit dokumentierter Scope-Anpassung verschoben.

**PFL-ACC-008:** Alle öffentlichen APIs und CLI-Befehle sind dokumentiert.

**PFL-ACC-009:** Der Release enthält keine unzulässig kopierten Buchseiten,
Listings, proprietären Programme oder unklar lizenzierten Testdateien.

**PFL-ACC-010:** README, Architektur, Roadmap, Pflichtenheft,
Formatabdeckungsmatrix und tatsächlicher Stand widersprechen einander nicht.

## 26. Definition of Done für einen Codec

Ein Codec gilt erst als abgeschlossen, wenn:

- Familie, Version und Profil eindeutig benannt sind;
- Quellen und offene Widersprüche dokumentiert sind;
- Probe, Reader, Validator und Writer implementiert sind;
- Ressourcenlimits und Fehlerpfade implementiert sind;
- gültige, ungültige, abgeschnittene und Grenzwertdateien getestet sind;
- Round-trip-Eigenschaften ausdrücklich definiert und bestanden sind;
- Konvertierungsfähigkeiten und Datenverluste dokumentiert sind;
- sprachneutrale Konformitätsfälle vorhanden sind;
- API- und Formatdokumentation vollständig sind;
- Supportmatrix und Changelog aktualisiert sind;
- alle relevanten CI- und Retro-Builds erfolgreich sind.

Ein reiner Reader kann als Zwischenstand „Read“ erreichen, aber nicht als
vollständiger Codec oder „Stable“ bezeichnet werden.

## 27. Risiken und Gegenmaßnahmen

| Risiko | Auswirkung | Gegenmaßnahme |
|---|---|---|
| widersprüchliche oder fehlerhafte Literatur | inkompatible Dateien | Quellenvergleich, Originaldateien, explizite Annahmen |
| fehlende Testdateien | Scheinsicherheit | Status nicht hochstufen, gezielte Fixture-Erzeugung |
| proprietäre Retro-Compiler | nicht reproduzierbare öffentliche CI | lokale dokumentierte Builds, keine Distribution der Compiler |
| 16-Bit-Speichergrenzen | zusätzliche Komplexität | Streaming, kleine Arbeitsblöcke, isolierte Plattformschicht |
| zu viele Formatvarianten | Scope-Ausweitung | harte Versionseinträge und priorisierte Abdeckungsmatrix |
| urheberrechtlich problematische Quellen | Veröffentlichungsrisiko | nur eigene Formulierungen und rechtmäßig verteilbare Fixtures |
| Datenverlust bei Konvertierung | falsches Vertrauen | Fail-by-default und strukturierte Verlustdiagnosen |
| schädliche Eingabedateien | Sicherheitslücken | Grenzen, Fuzzing, Sanitizer, keine Ausführung eingebetteter Inhalte |
| Sprachmigration beschädigt alte Codecs | Regression | Tags, Konformitätssuite und getrennte Migrationscommits |
| bedingte Übersetzung zerfasert den Code | Wartungsproblem | zentrale Compatibility-Schicht und ADR-Pflicht |

## 28. Offene Entscheidungen

Folgende Punkte müssen in eigenen ADRs entschieden werden:

1. **ADR-0001:** endgültige Schichten, Modulgrenzen und öffentliche
   Fehler-/Diagnosemodelle;
2. **ADR-0002:** exakte 1990-Compiler, Versionen, Speichermodelle und
   verbindliche Retro-Abnahmematrix;
3. **ADR-0003:** neutrale tabellarische Datenstruktur und Null-/Leersemantik;
4. **ADR-0004:** Formatkennungsschema und maschinenlesbare
   Spezifikationsstruktur;
5. **ADR-0005:** Testkorpusmanifest, Hashverfahren und Provenienzschema;
6. **ADR-0006:** CLI-JSON-Schema und dessen Versionierung;
7. **ADR-0007:** Zeitpunkt und Mindestversionen der Java- und
   C#-Implementierungen;
8. **ADR-0008:** Umgang mit unbekannten Records/Chunks beim
   Read-modify-write-Round-trip.

Offene Entscheidungen heben keine bereits eindeutige MUSS-Anforderung auf.

## 29. Änderungsverfahren

1. Neue oder geänderte Anforderungen erhalten eine stabile Kennung.
2. Auswirkungen auf Architektur, Tests, Formatmatrix und Roadmap werden
   gemeinsam geprüft.
3. Grundsatzänderungen benötigen ein ADR.
4. Pflichtenheftänderungen werden in einem eigenen, klar benannten Commit
   vorgenommen.
5. Kein nachträglicher Scope wird stillschweigend einer bereits abgenommenen
   historischen Epoche zugeschrieben.

## 30. Nächste verbindliche Schritte

1. ADR-0001 und ADR-0002 erstellen.
2. Verzeichnis `libraries/c89/` und `platform/` technisch ausformen.
3. C89/C90-GCC-Build mit strengem Warnprofil einrichten.
4. verfügbaren Turbo- und Microsoft-Compilerbestand erfassen;
5. 8.3-Quellpaketkonzept festlegen;
6. Kussmann Seiten 29–60 und das Inhaltsverzeichnis der Born-Ausgabe
   quellenkritisch indexieren;
7. Formatabdeckungsmatrix um konkrete Versionskennungen und Prioritäten
   erweitern;
8. erstes tabellarisches Modell und SDF-Profil spezifizieren;
9. anschließend erst die erste öffentliche C-API implementieren.
