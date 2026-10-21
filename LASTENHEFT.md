# Lastenheft — SASD Moschus

| Merkmal | Inhalt |
|---|---|
| Dokument | Fachliches Lastenheft |
| Projekt | SASD Moschus |
| Auftraggeber und Product Owner | Robin Goerlach / SASD-GmbH |
| Repository | https://github.com/Robin-Goerlach/SASD-Moschus |
| Version | 0.1 |
| Stand | 21. Oktober 2026 |
| Status | Verbindliche fachliche Arbeitsgrundlage; offene Entscheidungen sind gekennzeichnet |
| Projektlizenz | MIT |
| Erste Zielmarke | Nachweisbar unterstützte Dateiformate und Werkzeuge bis einschließlich 31. Dezember 1990 |
| Zugehöriges Pflichtenheft | [PFLICHTENHEFT.md](PFLICHTENHEFT.md) |

## 1. Zweck und Geltungsbereich

Dieses Lastenheft beschreibt aus Sicht des Auftraggebers, **was** SASD Moschus
leisten soll und **warum** diese Leistungen benötigt werden. Es definiert den
fachlichen Bedarf, die Produktgrenzen, die erwarteten Ergebnisse und die
Abnahmebedingungen. Das zugehörige Pflichtenheft beschreibt, **wie** diese
Anforderungen technisch und organisatorisch umgesetzt werden.

Das Lastenheft gilt für:

- die sprachunabhängige Sammlung verifizierten Formatwissens;
- die geplanten Bibliotheken zum Erkennen, Lesen, Prüfen und Schreiben von
  Dateien;
- den in C++ zu entwickelnden Kommandozeilen-Konverter;
- gemeinsame Testdaten, Konformitätsregeln und Dokumentation;
- die erste historische Produktepoche bis Ende 1990 sowie die Grundlage für
  spätere Epochen.

Es beschreibt keine Detailarchitektur, keine konkreten Klassenhierarchien und
keine interne Speicherorganisation. Solche Festlegungen gehören in das
Pflichtenheft oder in Architekturentscheidungen (ADRs).

### 1.1 Verbindlichkeit

Die Schlüsselwörter werden wie folgt verwendet:

- **MUSS**: zwingend für die betreffende Abnahme;
- **SOLL**: grundsätzlich erforderlich; eine Abweichung braucht eine
  dokumentierte und genehmigte Begründung;
- **KANN**: erwünschte, aber nicht abnahmeentscheidende Erweiterung;
- **NICHT**: ausdrücklich ausgeschlossen oder in eine spätere Epoche
  verschoben.

Jede nummerierte Anforderung besitzt eine dauerhafte Kennung. Änderungen
werden über die Versionsgeschichte und nachvollziehbare Commits geführt.

| ID | Anforderung |
|---|---|
| LAS-DOK-001 | Dieses Lastenheft MUSS die fachliche Referenz für Umfang, Priorität und Abnahme des Projekts sein. |
| LAS-DOK-002 | Das Pflichtenheft MUSS jede technische Umsetzung auf Anforderungen dieses Lastenhefts zurückführen können. |
| LAS-DOK-003 | Offene Punkte DÜRFEN NICHT als bereits vereinbarte Leistung dargestellt werden. |
| LAS-DOK-004 | Änderungen an Umfang oder Abnahmekriterien MÜSSEN versioniert, begründet und vom Auftraggeber bestätigt werden. |

## 2. Ausgangssituation und Problemstellung

Historische Dateien sind häufig nur mit nicht mehr unterstützten Anwendungen,
Betriebssystemen oder proprietären Konvertern zugänglich. Eine bekannte
Dateiendung genügt nicht: Formate unterscheiden sich je nach Version,
Hersteller, Plattform, Zeichensatz und eingesetzten Erweiterungen. Bestehende
Werkzeuge konzentrieren sich oft entweder auf moderne Formate oder auf einen
einzelnen Medientyp. Sie geben zudem nicht immer nachvollziehbar an, welche
Informationen bei einer Konvertierung verloren gehen.

Zwei gedruckte Referenzen bilden den Ausgangspunkt der Recherche:

- Ralf Kussmann, *Dateiformate und Konvertierung*, DATA BECKER, 1989;
- Günter Born, *Referenzhandbuch Dateiformate: Grafik, Text, Datenbanken,
  Tabellenkalkulation*, Addison-Wesley, Ausgabe 1992.

Die Bücher sollen kombiniert, kritisch abgeglichen und durch öffentlich
zugängliche Standards, Herstellerdokumentation und rechtmäßig nutzbare
Testdateien ergänzt werden. Sie sind Quellen, aber nicht automatisch die
alleinige Wahrheit. Widersprüche und spätere Ergänzungen müssen sichtbar
bleiben.

| ID | Anforderung |
|---|---|
| LAS-AUS-001 | Moschus MUSS den Zugang zu historischen Dateien ohne Abhängigkeit von der ursprünglichen Anwendung erleichtern. |
| LAS-AUS-002 | Moschus MUSS Formatname, Variante und Version getrennt betrachten, soweit dies fachlich möglich ist. |
| LAS-AUS-003 | Moschus MUSS Unsicherheit kenntlich machen, statt eine nicht belegte Interpretation als Tatsache auszugeben. |
| LAS-AUS-004 | Moschus MUSS fachliche Verluste und Annahmen einer Konvertierung offenlegen. |
| LAS-AUS-005 | Moschus SOLL verstreutes Formatwissen in einer langfristig pflegbaren, prüfbaren Form bündeln. |
| LAS-AUS-006 | Moschus DARF den Besitz historischer Originalsoftware für seine normale Nutzung NICHT voraussetzen. |

## 3. Produktvision und Nutzen

SASD Moschus soll eine offene, langfristig nutzbare Werkzeugfamilie für
historische Dateiformate werden. Eine Datei soll nicht nur „irgendwie“ geöffnet
werden. Nutzer sollen erkennen können, was sie vor sich haben, wie sicher die
Erkennung ist, ob die Datei regelkonform ist, was sich erhalten lässt und
welche Änderungen eine Konvertierung verursacht.

Der Projektname bezeichnet das Gesamtvorhaben. Die Bibliotheken liefern die
wiederverwendbaren Fähigkeiten; der Konverter macht sie unmittelbar auf der
Kommandozeile nutzbar. Gemeinsame Spezifikationen und Konformitätstests sorgen
dafür, dass Implementierungen in verschiedenen Programmiersprachen dasselbe
fachliche Verhalten anstreben.

| ID | Ziel | Erfolgshinweis |
|---|---|---|
| LAS-ZIE-001 | Historische Daten zugänglich erhalten | Unterstützte Dateien lassen sich ohne Originalanwendung untersuchen und auslesen. |
| LAS-ZIE-002 | Konvertierungen vertrauenswürdig machen | Verluste, Ersetzungen, Annahmen und Fehler werden maschinen- und menschenlesbar gemeldet. |
| LAS-ZIE-003 | Historische Unterschiede bewahren | Versionen und Herstellerabweichungen werden nicht unter einem pauschalen Formatnamen versteckt. |
| LAS-ZIE-004 | Wiederverwendung ermöglichen | Anwendungen können die Fähigkeiten als Bibliothek statt nur als Prozessaufruf nutzen. |
| LAS-ZIE-005 | Sprachübergreifende Verlässlichkeit schaffen | Gemeinsame Prüffälle beschreiben dasselbe erwartete Verhalten für alle Bibliotheken. |
| LAS-ZIE-006 | Forschung nachvollziehbar machen | Technische Aussagen sind mit Herkunft, Unsicherheit und Prüfnachweis dokumentiert. |
| LAS-ZIE-007 | Chronologische Weiterentwicklung erlauben | Nach 1990 können Formate und Sprachstandards in klar getrennten Epochen ergänzt werden. |
| LAS-ZIE-008 | Langfristige Wartbarkeit sichern | Umfang, Status und bekannte Grenzen bleiben öffentlich und eindeutig dokumentiert. |

## 4. Interessengruppen und Nutzer

| Rolle | Bedarf | Erwarteter Nutzen |
|---|---|---|
| Auftraggeber / Product Owner | Verlässlicher Umfang, Fortschritt und Abnahme | Steuerbares, nachvollziehbares Produkt |
| Archivierende Personen und Institutionen | Bestandsanalyse, Validierung und Migration | Erhaltung und kontrollierter Export historischer Daten |
| Anwender mit Altbeständen | Einfache Untersuchung und Umwandlung einzelner Dateien | Zugriff ohne historische Originalumgebung |
| Softwareentwickler | Stabile Bibliotheksverträge und klare Fehlerbilder | Einbindung von Formatunterstützung in eigene Programme |
| Forschende und Digital-Humanities-Projekte | Reproduzierbare Interpretation und Quellenlage | Zitier- und überprüfbare Ergebnisse |
| Format- und Retrocomputing-Community | Erweiterbare Spezifikationen und echte Altwerkzeug-Tests | Gemeinsame Pflege historischen Wissens |
| Sicherheitsprüfer | Begrenztes Verhalten bei schadhaften Eingaben | Belastbare Analyse unbekannter Dateien |
| Paketbetreuer | Reproduzierbare Builds, Versionierung und Lizenzklarheit | Verteilbare, wartbare Pakete |

| ID | Anforderung |
|---|---|
| LAS-NUT-001 | Die Kommandozeilenfunktionen MÜSSEN ohne Programmierkenntnisse für grundlegende Prüf- und Konvertierungsaufgaben nutzbar sein. |
| LAS-NUT-002 | Die Bibliotheken MÜSSEN Entwicklern strukturierte Ergebnisse statt ausschließlich formatierten Text liefern. |
| LAS-NUT-003 | Forschungsergebnisse MÜSSEN für fachkundige Dritte nachprüfbar dokumentiert sein. |
| LAS-NUT-004 | Fehler- und Warnmeldungen SOLLEN sowohl Handlungshinweise als auch eine stabile maschinenlesbare Kennung enthalten. |
| LAS-NUT-005 | Unterschiedliche Nutzergruppen DÜRFEN NICHT durch stillschweigende Standardannahmen zu fachlich falschen Ergebnissen geführt werden. |

## 5. Fachlicher Produktumfang

### 5.1 Produktbestandteile

| Bestandteil | Erwartete Leistung | Priorität 1990 |
|---|---|---|
| Formatkatalog | Versionierte Übersicht über Formate, Varianten, Fähigkeiten und Beleglage | MUSS |
| Formatbeschreibungen | Sprachunabhängige, prüfbare Beschreibung der unterstützten Strukturen und Regeln | MUSS |
| Portable Kernbibliothek | Grundlegende Fähigkeiten für die historische Baseline | MUSS |
| C++-Bibliothek | C++-gerechte Nutzung der gemeinsamen Fähigkeiten | MUSS, Umfang gemäß Pflichtenheft |
| Weitere Sprachbibliotheken | Eigenständige Implementierungen gemeinsamer Verträge | SOLL, schrittweise |
| C++-Konverter | Erkennen, untersuchen, validieren und konvertieren | MUSS |
| Konformitätssuite | Gemeinsame positive, negative und Grenzfalltests | MUSS |
| Testkorpus | Rechtmäßig nutzbare Dateien samt Provenienz und Erwartung | MUSS |
| Dokumentation | Nutzung, Grenzen, Quellen und Entscheidungen | MUSS |

| ID | Anforderung |
|---|---|
| LAS-SCP-001 | Bibliothek, Konverter, Spezifikationen und Konformitätstests MÜSSEN als zusammengehöriges Produkt gepflegt werden. |
| LAS-SCP-002 | Der Konverter MUSS dieselben fachlichen Regeln wie die Bibliothek verwenden. |
| LAS-SCP-003 | Formatwissen MUSS unabhängig von einer einzelnen Programmiersprache dokumentiert sein. |
| LAS-SCP-004 | Neue Sprachimplementierungen MÜSSEN anhand gemeinsamer Konformitätserwartungen vergleichbar sein. |
| LAS-SCP-005 | Jeder Produktbestandteil MUSS einen dokumentierten Reife- und Unterstützungsstand besitzen. |

### 5.2 Abgrenzung der ersten Produktepoche

Die erste Epoche endet fachlich am **31. Dezember 1990**. Maßgeblich ist nicht,
wann eine heutige Beschreibung veröffentlicht wurde, sondern ob die konkrete
Formatvariante oder Funktion bis zu diesem Stichtag verfügbar und belegt war.

| ID | Anforderung |
|---|---|
| LAS-EPO-001 | Die 1990-Abnahme MUSS nur Varianten umfassen, deren historische Verfügbarkeit bis zum Stichtag belegt ist. |
| LAS-EPO-002 | Spätere Erweiterungen eines älteren Formats DÜRFEN NICHT stillschweigend Teil der 1990-Kompatibilität werden. |
| LAS-EPO-003 | Unklare Einführungsdaten MÜSSEN als Forschungsbedarf gekennzeichnet werden. |
| LAS-EPO-004 | Die Freigabe MUSS den genauen Stand jedes Formats und jeder Fähigkeit ausweisen. |
| LAS-EPO-005 | Spätere Epochen MÜSSEN die reproduzierbare Nutzung des abgeschlossenen 1990-Stands erhalten. |
| LAS-EPO-006 | Microsoft Access und JPEG gehören NICHT zur 1990-Abnahme; sie sind Ziele späterer Epochen. |

### 5.3 Ausdrücklich nicht geschuldete Leistungen

- pixel- oder layoutidentische Wiedergabe jeder historischen Anwendung;
- Emulation vollständiger Betriebssysteme oder Anwendungsprogramme;
- Umgehung von Passwörtern, Verschlüsselung oder Kopierschutz;
- Reparatur jeder beliebig beschädigten Datei;
- Konvertierbarkeit jedes Formats in jedes andere Format;
- Übernahme proprietärer Quelltexte, Buchtexte, Disketteninhalte oder
  Testdateien ohne geklärte Rechte;
- Unterstützung moderner Cloud-, Kollaborations- oder Makroausführungsmodelle
  innerhalb der 1990-Epoche;
- Garantie, dass fremde Programme jede formal gültige Ausgabedatei identisch
  darstellen.

| ID | Anforderung |
|---|---|
| LAS-NOT-001 | Moschus MUSS eine nicht sinnvolle Konvertierungsroute ablehnen dürfen und den Grund nennen. |
| LAS-NOT-002 | Moschus DARF keine Vollständigkeit behaupten, wenn nur ein Teil einer Formatvariante unterstützt wird. |
| LAS-NOT-003 | Moschus DARF eingebetteten aktiven Inhalt NICHT automatisch ausführen. |
| LAS-NOT-004 | Ein Recovery-Ergebnis DARF NICHT als verlustfreie oder normgerechte Rekonstruktion ausgegeben werden. |

## 6. Formatumfang der 1990-Epoche

Die folgende Liste ist der fachliche Untersuchungs- und Planungsumfang. Ein
Eintrag bedeutet nicht automatisch fertige Unterstützung. Die verbindliche
Fähigkeit pro Version wird in `docs/format-coverage.md` geführt und erst durch
Spezifikation, Implementierung und Tests erworben.

### 6.1 Tabellarische Daten und Austauschformate

- ASCII DELIMITED und historisch belegte Trennzeichenprofile;
- ASCII SDF (System Data Format / feste Feldbreiten im jeweiligen Kontext);
- CSV-Varianten, sofern für die Epoche belegt;
- DIF (Data Interchange Format);
- SDI und SIF, soweit Quellenlage und Prüfdaten eine eindeutige Spezifikation
  erlauben;
- SYLK;
- frühe Lotus-1-2-3-Formate und fachlich zugehörige Austauschwege;
- relevante Multiplan- und frühe Excel-Austauschformate, soweit bis 1990
  verfügbar und rechtssicher prüfbar.

### 6.2 Datenbanken

- dBASE II;
- dBASE III und dBASE III Plus;
- dBASE IV einschließlich fachlich relevanter Begleitdateien;
- Feldtypen, Datensätze, Löschmarkierungen, Zeichensätze und Memo-Inhalte der
  jeweils bestätigten Varianten;
- Index- und weitere Begleitdateien nur in dem Umfang, in dem sie zuverlässig
  spezifiziert und getestet werden können.

### 6.3 Dokumente, Text und Auszeichnung

- ASCII- und zeichenkodierte Textdateien;
- frühe Microsoft-Word-Formate, insbesondere belegte Versionen 3 bis 5;
- WordStar-Varianten der Epoche;
- WordPerfect-Varianten der Epoche;
- RTF 1.0 und weitere bis zum Stichtag belegte Varianten;
- DCA/RFT;
- IBM Text 4, soweit eindeutig spezifizierbar;
- SGML-Profile, wenn ein konkretes, prüfbares Profil benannt wird;
- Austauschbeziehungen zu PageMaker und Ventura nur für belegte, fachlich
  sinnvolle Inhalte.

### 6.4 Rastergrafik

- PCX;
- GEM IMG;
- IFF/ILBM und einschlägige Untervarianten;
- GIF87a und GIF89a;
- TIFF-Varianten bis zum Stichtag;
- frühe Windows- und OS/2-Bitmapvarianten sowie ICO, soweit belegt.

### 6.5 Vektor-, Metadatei-, CAD- und Druckformate

- GEM-Metadateien;
- CGM;
- WPG;
- DXF und DXB der belegten Versionen;
- frühe WMF-Varianten;
- HP-GL;
- PCL der Epoche;
- EPS/PostScript-Ausschnitte, soweit sicher analysierbar und ohne Ausführung
  fremden Programmcodes behandelbar.

| ID | Anforderung |
|---|---|
| LAS-FMT-001 | Jede unterstützte Formatfamilie MUSS in konkrete Versionen oder Profile zerlegt werden. |
| LAS-FMT-002 | Jede Version MUSS ihren Fähigkeitsstand getrennt für Erkennen, Lesen, Prüfen, Schreiben, Round-trip und Konvertieren ausweisen. |
| LAS-FMT-003 | Begleitdateien MÜSSEN getrennt benannt und ihr Einfluss auf die Vollständigkeit erklärt werden. |
| LAS-FMT-004 | Zeichensatz, Byte-Reihenfolge, Plattformvariante und Zahlenrepräsentation MÜSSEN berücksichtigt werden, wenn sie das Ergebnis verändern. |
| LAS-FMT-005 | Herstellererweiterungen MÜSSEN von dokumentierten Basisvarianten unterscheidbar sein. |
| LAS-FMT-006 | Der Formatkatalog MUSS für jeden Eintrag Quellenlage, Status, Einschränkungen und Prüfnachweise anzeigen. |
| LAS-FMT-007 | Ein Format DARF erst als „Stable“ gelten, wenn die festgelegten Abnahmekriterien vollständig erfüllt sind. |
| LAS-FMT-008 | Nicht belegbare oder nicht testbare Kandidaten DÜRFEN mit Begründung aus der 1990-Freigabe zurückgestellt werden. |

## 7. Fachliche Funktionen

### 7.1 Erkennen und Untersuchen

| ID | Anforderung |
|---|---|
| LAS-ERK-001 | Moschus MUSS unterstützte Dateien anhand ihres Inhalts untersuchen können. |
| LAS-ERK-002 | Eine Dateiendung DARF nur als Hinweis und NICHT als alleiniger Nachweis gelten. |
| LAS-ERK-003 | Das Erkennungsergebnis MUSS Formatfamilie, wahrscheinliche Variante, Konfidenz und Begründungen ausgeben. |
| LAS-ERK-004 | Mehrdeutige Erkennung MUSS alle fachlich plausiblen Kandidaten sichtbar machen. |
| LAS-ERK-005 | Nutzer MÜSSEN bei Bedarf eine konkrete Interpretation vorgeben können. |
| LAS-ERK-006 | Die Untersuchung SOLL wesentliche Metadaten, Strukturgrößen, verwendete Funktionen und erkannte Begleitdateien berichten. |
| LAS-ERK-007 | Unbekannte Erweiterungen innerhalb eines sonst lesbaren Formats MÜSSEN gemeldet werden. |

### 7.2 Lesen und Öffnen

| ID | Anforderung |
|---|---|
| LAS-LES-001 | Moschus MUSS als „Read“ gekennzeichnete Versionen vollständig innerhalb des dokumentierten Funktionsumfangs lesen können. |
| LAS-LES-002 | Gelesene Inhalte MÜSSEN in fachlich geeigneten Strukturen bereitgestellt werden. |
| LAS-LES-003 | Rohinformationen MÜSSEN erhalten oder referenzierbar bleiben, wenn dies für Diagnose oder Round-trip zugesagt ist. |
| LAS-LES-004 | Nicht unterstützte Bestandteile MÜSSEN mit Position und Auswirkung gemeldet werden. |
| LAS-LES-005 | Nutzer MÜSSEN zwischen striktem Lesen und ausdrücklich gewählter Wiederherstellung unterscheiden können. |
| LAS-LES-006 | Ein Leseerfolg DARF NICHT gemeldet werden, wenn abnahmeentscheidende Inhalte unbemerkt fehlen. |

### 7.3 Validieren

| ID | Anforderung |
|---|---|
| LAS-VAL-001 | Moschus MUSS Dateien gegen die Regeln der ausgewählten Formatversion prüfen können. |
| LAS-VAL-002 | Prüfergebnisse MÜSSEN Fehler, Warnungen und Hinweise unterscheiden. |
| LAS-VAL-003 | Jede Feststellung MUSS nach Möglichkeit Ort, verletzte Regel und Bedeutung nennen. |
| LAS-VAL-004 | Die Validierung MUSS zwischen formaler Gültigkeit und bloßer Lesbarkeit unterscheiden. |
| LAS-VAL-005 | Ein maschinenlesbarer Prüfbericht MUSS für Stapelverarbeitung verfügbar sein. |
| LAS-VAL-006 | Der Prozessstatus MUSS Erfolg, Warnungen, ungültige Eingabe und Bedienfehler unterscheidbar machen. |

### 7.4 Schreiben und Speichern

| ID | Anforderung |
|---|---|
| LAS-SCH-001 | Moschus MUSS als „Write“ gekennzeichnete Zielversionen explizit auswählen können. |
| LAS-SCH-002 | Eine erzeugte Datei MUSS die Grenzen der gewählten historischen Version einhalten. |
| LAS-SCH-003 | Spätere Felder oder Erweiterungen DÜRFEN NICHT ohne ausdrückliche Wahl in ein historisches Ziel gelangen. |
| LAS-SCH-004 | Gleiche Inhalte und Optionen SOLLEN, soweit das Format es erlaubt, reproduzierbare Ausgaben erzeugen. |
| LAS-SCH-005 | Vor dem Schreiben MUSS erkennbar sein, welche Inhalte im Zielformat nicht darstellbar sind. |
| LAS-SCH-006 | Schreibvorgänge DÜRFEN bestehende Dateien nur nach ausdrücklicher Freigabe überschreiben. |
| LAS-SCH-007 | Ein fehlgeschlagener Schreibvorgang DARF keine scheinbar erfolgreiche Zieldatei zurücklassen. |

### 7.5 Konvertieren

| ID | Anforderung |
|---|---|
| LAS-KON-001 | Moschus MUSS fachlich sinnvolle Konvertierungen zwischen unterstützten Quell- und Zielversionen anbieten. |
| LAS-KON-002 | Eine Konvertierung MUSS über den erwarteten Informationsverlust informieren, bevor eine bestehende Datei ersetzt wird. |
| LAS-KON-003 | Tatsächlich eingetretene Verluste, Ersetzungen, Annahmen und verworfene Inhalte MÜSSEN im Ergebnisbericht stehen. |
| LAS-KON-004 | Verlustfreie, strukturerhaltende und nur visuell angenäherte Konvertierungen MÜSSEN unterscheidbar sein. |
| LAS-KON-005 | Die Abwesenheit eines sinnvollen gemeinsamen Datenmodells MUSS zur Ablehnung statt zu irreführender Ausgabe führen. |
| LAS-KON-006 | Stapelkonvertierung SOLL mehrere Eingaben mit getrennten Ergebnissen und einer Zusammenfassung verarbeiten können. |
| LAS-KON-007 | Nutzer MÜSSEN Fehlerstrategie und Überschreibverhalten für Stapelläufe festlegen können. |
| LAS-KON-008 | dBASE-Daten MÜSSEN in der 1990-Epoche mindestens in ein geeignetes neutrales Tabellen- oder Austauschformat überführt werden können. |
| LAS-KON-009 | Die direkte Konvertierung dBASE ↔ Microsoft Access ist eine spätere Leistung und NICHT Teil der 1990-Abnahme. |

### 7.6 Wiederherstellung beschädigter Dateien

| ID | Anforderung |
|---|---|
| LAS-REC-001 | Ein Wiederherstellungsmodus MUSS ausdrücklich aktiviert werden. |
| LAS-REC-002 | Der Wiederherstellungsmodus MUSS jede Abweichung von regulärer Interpretation protokollieren. |
| LAS-REC-003 | Wiedergewonnene, ersetzte und nicht wiedergewinnbare Bereiche MÜSSEN unterscheidbar sein. |
| LAS-REC-004 | Das Original MUSS unverändert bleiben, sofern der Nutzer nicht ausdrücklich ein anderes Ziel bestimmt. |
| LAS-REC-005 | Wiederherstellung DARF Sicherheits- und Ressourcenbegrenzungen NICHT außer Kraft setzen. |

### 7.7 Kommandozeilenprodukt

| ID | Anforderung |
|---|---|
| LAS-CLI-001 | Der C++-Konverter MUSS Funktionen zum Erkennen, Untersuchen, Validieren und Konvertieren bereitstellen. |
| LAS-CLI-002 | Der Konverter MUSS verfügbare Formate, Versionen, Fähigkeiten und Einschränkungen auflisten können. |
| LAS-CLI-003 | Menschenlesbare Standardausgabe und eine stabile maschinenlesbare Ausgabe MÜSSEN verfügbar sein. |
| LAS-CLI-004 | Hilfe, Versionsangabe und verständliche Beispiele MÜSSEN ohne externe Dokumentensuche erreichbar sein. |
| LAS-CLI-005 | Automatisierte Nutzung MUSS ohne interaktive Rückfragen möglich sein, wenn alle Entscheidungen als Optionen vorliegen. |
| LAS-CLI-006 | Ein Trockenlauf SOLL geplante Route, Annahmen und Verluste ohne Erzeugung der Zieldatei zeigen. |
| LAS-CLI-007 | Der Konverter MUSS Dateinamen, Pfade und Text in den dokumentierten Grenzen der jeweiligen Plattform behandeln. |

### 7.8 Bibliotheksnutzung und mehrere Sprachen

| ID | Anforderung |
|---|---|
| LAS-API-001 | Wiederverwendbare Formatfunktionen MÜSSEN als Bibliothek verfügbar sein. |
| LAS-API-002 | Die Bibliothek MUSS Erkennung, Lesen, Validierung, Schreiben und Konvertierungsdiagnostik getrennt nutzbar machen. |
| LAS-API-003 | C/C++ bilden die erste ausführbare Referenz für die 1990-Epoche. |
| LAS-API-004 | C#- und Java-Bibliotheken SOLLEN später als eigenständig nutzbare, idiomatische Implementierungen entstehen. |
| LAS-API-005 | Weitere Sprachen KÖNNEN ergänzt werden, wenn sie Spezifikation und Konformitätssuite einhalten. |
| LAS-API-006 | Eine Sprachbibliothek DARF Unterstützung NICHT allein deshalb behaupten, weil sie einen externen Konverterprozess startet. |
| LAS-API-007 | Fachlich gleiche Operationen SOLLEN sprachübergreifend vergleichbare Ergebnisse und Diagnosekennungen liefern. |
| LAS-API-008 | Öffentliche Verträge MÜSSEN versioniert und Änderungen nachvollziehbar dokumentiert werden. |

## 8. Nutzungsszenarien

### 8.1 Unbekannte Datei bestimmen

1. Ein Nutzer übergibt eine Datei ohne verlässliche Endung.
2. Moschus untersucht Signaturen, Struktur und Plausibilität.
3. Das Ergebnis nennt Kandidaten, Konfidenz, Gründe und Einschränkungen.
4. Der Nutzer kann eine Variante zur weiteren Untersuchung wählen.

**Erfolg:** Es wird kein falscher eindeutiger Befund vorgetäuscht; die
Entscheidungsgrundlage ist nachvollziehbar.

### 8.2 Archivbestand prüfen

1. Eine Institution verarbeitet viele Dateien ohne Veränderung der Originale.
2. Für jede Datei werden Erkennung, Validität, Metadaten und Auffälligkeiten
   protokolliert.
3. Die Ergebnisse können maschinell ausgewertet und später reproduziert werden.

**Erfolg:** Jeder Bericht ist einer Eingabe, Moschus-Version und Regelbasis
zuordenbar.

### 8.3 dBASE-Daten migrieren

1. Eine konkrete dBASE-Version und gegebenenfalls ihre Begleitdateien werden
   erkannt.
2. Felder, Datensätze, Löschzustände, Memo-Inhalte und Zeichensatzannahmen
   werden geprüft.
3. Der Nutzer wählt ein unterstütztes Tabellen- oder Austauschformat.
4. Moschus weist vorab auf nicht darstellbare Eigenschaften hin.
5. Ausgabe und Verlustbericht werden gemeinsam erzeugt.

**Erfolg:** Datensatzanzahl und übertragene Werte sind prüfbar; jede Abweichung
ist erklärt. Access wird erst in einer späteren Epoche Ziel oder Quelle.

### 8.4 Beschädigte Datei untersuchen

1. Striktes Lesen lehnt die ungültige Datei mit konkreten Befunden ab.
2. Der Nutzer aktiviert bewusst den Wiederherstellungsmodus.
3. Moschus gewinnt nur plausibel begründbare Inhalte und protokolliert Lücken.
4. Das Original bleibt unverändert.

**Erfolg:** Das Ergebnis ist eindeutig als Recovery gekennzeichnet und nicht
mit einer validen Rekonstruktion zu verwechseln.

### 8.5 Bibliothek integrieren

1. Ein Entwickler wählt eine verfügbare Sprachbibliothek.
2. Er liest Format- und Versionsfähigkeiten zur Laufzeit oder Dokumentation aus.
3. Seine Anwendung verarbeitet strukturierte Ergebnisse und Diagnosen.
4. Gemeinsame Konformitätsfälle erlauben den Abgleich mit anderen Sprachen.

**Erfolg:** Die Integration benötigt weder Bildschirmausgaben zu parsen noch
historische Originalsoftware aufzurufen.

### 8.6 Neues Format oder neue Variante beitragen

1. Ein Beitrag dokumentiert Quellen, historische Einordnung und Rechte.
2. Die Formatbeschreibung benennt Grenzen und offene Fragen.
3. Testdateien und erwartete Ergebnisse werden ergänzt.
4. Fähigkeiten werden erst nach bestandener Prüfung hochgestuft.

**Erfolg:** Der öffentliche Status entspricht dem tatsächlich nachgewiesenen
Umfang.

| ID | Anforderung |
|---|---|
| LAS-USE-001 | Alle sechs Kernszenarien MÜSSEN durch Dokumentation und nachvollziehbare Beispiele abgedeckt werden. |
| LAS-USE-002 | Für jedes als stabil bezeichnete Format MUSS mindestens ein positiver und ein negativer End-to-End-Fall vorliegen. |
| LAS-USE-003 | Für jede freigegebene Konvertierungsroute MUSS ein Fall mit Verlustbewertung vorliegen. |

## 9. Qualitätsanforderungen

### 9.1 Korrektheit und Transparenz

| ID | Anforderung |
|---|---|
| LAS-QUA-001 | Korrektheit und nachvollziehbare Grenzen haben Vorrang vor einer hohen Zahl nominell unterstützter Formate. |
| LAS-QUA-002 | Öffentliche Unterstützungsangaben MÜSSEN durch automatisierte Tests belegbar sein. |
| LAS-QUA-003 | Ein erfolgreicher Round-trip MUSS anhand formatspezifischer Erhaltungskriterien definiert sein. |
| LAS-QUA-004 | Bytegleichheit DARF nur dann verlangt oder versprochen werden, wenn sie fachlich sinnvoll und ausdrücklich definiert ist. |
| LAS-QUA-005 | Bekannte Abweichungen zwischen Quellen oder Referenzprogrammen MÜSSEN dokumentiert werden. |
| LAS-QUA-006 | Diagnoseergebnisse MÜSSEN reproduzierbar und einer Regelversion zuordenbar sein. |

### 9.2 Sicherheit und Robustheit

Historische Dateien sind nicht vertrauenswürdig. Fehlerhafte Längen, Offsets,
Kompressionsdaten, Verkettungen und rekursive Strukturen dürfen weder den
Rechner gefährden noch unkontrolliert Ressourcen verbrauchen.

| ID | Anforderung |
|---|---|
| LAS-SEC-001 | Alle Eingaben MÜSSEN grundsätzlich als nicht vertrauenswürdig behandelt werden. |
| LAS-SEC-002 | Verarbeitung MUSS mit dokumentierten Grenzen für Speicher, Ausgabegröße, Verschachtelung und Arbeitsaufwand möglich sein. |
| LAS-SEC-003 | Grenzüberschreitungen MÜSSEN kontrolliert und mit Diagnose beendet werden. |
| LAS-SEC-004 | Eingebettete Makros, Programme, Druckerbefehle oder externe Verweise DÜRFEN NICHT automatisch ausgeführt oder abgerufen werden. |
| LAS-SEC-005 | Pfadangaben aus Archiven oder Dokumenten DÜRFEN NICHT unkontrolliert außerhalb des gewählten Zielbereichs schreiben. |
| LAS-SEC-006 | Geheime oder personenbezogene Dateiinhalte DÜRFEN NICHT ungefragt in Telemetrie oder externe Dienste übertragen werden. |
| LAS-SEC-007 | Sicherheitsrelevante Fehler MÜSSEN nach einem dokumentierten Verfahren gemeldet und behoben werden können. |
| LAS-SEC-008 | Recovery MUSS denselben Sicherheitsgrenzen wie reguläre Verarbeitung unterliegen. |

### 9.3 Portabilität und historische Werkzeugketten

Die erste Epoche soll nicht nur historische Daten verstehen, sondern ihre
portable Kernfunktion mit einem zur Epoche passenden Sprachumfang aufbauen.
Das ist ein Produktziel, keine Verpflichtung, moderne Sicherheits- oder
Testwerkzeuge abzulehnen.

| ID | Anforderung |
|---|---|
| LAS-POR-001 | Der portable Kern der 1990-Epoche MUSS den vereinbarten ANSI-C89-/ISO-C90-Sprachumfang einhalten. |
| LAS-POR-002 | Der C++-Konverter MUSS für die 1990-Epoche mit dem im Pflichtenheft festgelegten frühen, portablen C++-Umfang auskommen. |
| LAS-POR-003 | GCC im strikten C90-Modus MUSS als frei verfügbare Referenzwerkzeugkette unterstützt werden. |
| LAS-POR-004 | Builds mit ausgewählten Versionen von Turbo C/Turbo C++ und Microsoft C/C++ SOLLEN, soweit rechtlich und praktisch möglich, nachweisbar sein. |
| LAS-POR-005 | Proprietäre Compiler und SDKs DÜRFEN NICHT ohne entsprechende Rechte verteilt werden. |
| LAS-POR-006 | Plattformspezifische Grenzen MÜSSEN dokumentiert werden und DÜRFEN nicht als allgemeine Formatgrenzen erscheinen. |
| LAS-POR-007 | Moderne Prüfbauten SOLLEN zusätzlich eingesetzt werden, ohne die historische Baseline zu verfälschen. |
| LAS-POR-008 | Nach Abschluss der 1990-Epoche MUSS die C++-Entwicklung kontrolliert über C++98, C++03, C++11, C++14 und C++17 bis C++20 fortgeführt werden können. |
| LAS-POR-009 | Jede neue Sprachepoche MUSS ihren Mindeststandard, Werkzeugketten und Kompatibilitätsbruch klar benennen. |
| LAS-POR-010 | Abgeschlossene historische Releases MÜSSEN aus dem Repository reproduzierbar referenzierbar bleiben. |

### 9.4 Leistung und Skalierbarkeit

Es werden bewusst keine unbelegten absoluten Zeitwerte festgeschrieben. Die
Abnahme betrachtet stattdessen Begrenzbarkeit, Fortschritt und sinnvolle
Verarbeitung großer Dateien.

| ID | Anforderung |
|---|---|
| LAS-LEI-001 | Verarbeitung SOLL, soweit das Format es erlaubt, ohne vollständiges Laden der Datei in den Arbeitsspeicher möglich sein. |
| LAS-LEI-002 | Nutzer MÜSSEN Ressourcenlimits vorgeben können oder verlässliche Standardlimits erhalten. |
| LAS-LEI-003 | Lange Stapelläufe SOLLEN Fortschritt und den aktuell bearbeiteten Gegenstand ausgeben können. |
| LAS-LEI-004 | Leistungsregressionen MÜSSEN für repräsentative Referenzdateien erkennbar sein. |
| LAS-LEI-005 | Optimierungen DÜRFEN Korrektheit, Sicherheit oder Diagnosequalität NICHT verschlechtern. |

### 9.5 Bedienbarkeit und Barrierearmut

| ID | Anforderung |
|---|---|
| LAS-BED-001 | Meldungen MÜSSEN klar zwischen Ursache, Auswirkung und möglicher Handlung unterscheiden. |
| LAS-BED-002 | Standardabläufe SOLLEN mit wenigen, vorhersehbaren Optionen möglich sein. |
| LAS-BED-003 | Gefährliche oder verlustbehaftete Vorgänge MÜSSEN ausdrücklich erkennbar sein. |
| LAS-BED-004 | Dokumentation und Textausgaben SOLLEN mit üblichen Bildschirmlesern und rein textbasierten Arbeitsabläufen nutzbar sein. |
| LAS-BED-005 | Farbcodierung DARF NICHT der einzige Träger einer Bedeutung sein. |
| LAS-BED-006 | Fachbegriffe und historische Produktnamen MÜSSEN in einem Glossar oder verlinkten Kontext erläutert werden. |

### 9.6 Wartbarkeit und Nachhaltigkeit

| ID | Anforderung |
|---|---|
| LAS-WAR-001 | Eine Formatvariante SOLL ergänzt werden können, ohne fachlich unabhängige Formate ändern zu müssen. |
| LAS-WAR-002 | Unterstützungsstatus, Spezifikation, Tests und Implementierung MÜSSEN konsistent gehalten werden. |
| LAS-WAR-003 | Öffentliche Änderungen MÜSSEN über Versionshinweise nachvollziehbar sein. |
| LAS-WAR-004 | Veraltete Schnittstellen MÜSSEN vor Entfernung gekennzeichnet und mit einem Migrationshinweis versehen werden. |
| LAS-WAR-005 | Kritische Formatlogik MUSS durch automatisierte Regressionstests geschützt sein. |
| LAS-WAR-006 | Das Projekt SOLL ohne einzelne geheime Wissens- oder Infrastrukturquelle fortführbar sein. |

## 10. Quellen, Provenienz und Rechte

| ID | Anforderung |
|---|---|
| LAS-QUE-001 | Jede wesentliche Formataussage MUSS mindestens einer nachvollziehbaren Quelle oder einem dokumentierten empirischen Befund zugeordnet werden. |
| LAS-QUE-002 | Primärquellen und offizielle Standards SOLLEN, sofern verfügbar, gegenüber Sekundärbeschreibungen bevorzugt werden. |
| LAS-QUE-003 | Widersprüche zwischen Kussmann, Born und weiteren Quellen MÜSSEN sichtbar dokumentiert und durch Tests untersucht werden. |
| LAS-QUE-004 | Buchtexte, Abbildungen und Programmlistings DÜRFEN NICHT ohne eigene Rechtsgrundlage übernommen werden. |
| LAS-QUE-005 | Die mit Büchern gelieferten Disketten DÜRFEN NICHT automatisch als frei verteilbar gelten. |
| LAS-QUE-006 | Jede Testdatei MUSS Herkunft, Lizenz- oder Nutzungslage und erwartete Eigenschaft dokumentieren. |
| LAS-QUE-007 | Nicht verteilbare Testdateien DÜRFEN NICHT in das öffentliche Repository aufgenommen werden. |
| LAS-QUE-008 | Für nicht verteilbare lokale Prüfdaten SOLL eine Metadaten- und Hashreferenz ohne Offenlegung des Inhalts möglich sein. |
| LAS-QUE-009 | Reverse Engineering MUSS im jeweils zulässigen rechtlichen Rahmen erfolgen; Unsicherheiten sind vor Veröffentlichung zu klären. |
| LAS-QUE-010 | Projektcode und eigenständige Projektdokumentation MÜSSEN mit der ausgewiesenen MIT-Lizenz vereinbar sein. |

## 11. Dokumentation und Nachvollziehbarkeit

| ID | Anforderung |
|---|---|
| LAS-DOC-001 | Für jede unterstützte Version MUSS eine Formatbeschreibung mit Geltungsbereich und bekannten Grenzen vorliegen. |
| LAS-DOC-002 | Für jede Bibliothek MUSS es Installations-, Build- und mindestens ein Nutzungsbeispiel geben. |
| LAS-DOC-003 | Für den Konverter MUSS eine Referenz aller Befehle, Optionen, Statuscodes und Berichtsformate vorliegen. |
| LAS-DOC-004 | Die Coverage-Matrix MUSS den tatsächlich geprüften Stand widerspiegeln. |
| LAS-DOC-005 | Entscheidungen mit langfristiger technischer oder fachlicher Wirkung MÜSSEN als ADR dokumentiert werden. |
| LAS-DOC-006 | Release Notes MÜSSEN neue Fähigkeiten, Änderungen, Fehlerbehebungen und bekannte Einschränkungen nennen. |
| LAS-DOC-007 | Ein Glossar SOLL mehrdeutige Begriffe wie „Format“, „Version“, „Profil“, „Round-trip“ und „verlustfrei“ definieren. |
| LAS-DOC-008 | Beispiele DÜRFEN keine Rechte oder Datenschutzinteressen Dritter verletzen. |
| LAS-DOC-009 | Die Dokumentation SOLL in Deutsch oder Englisch verfasst sein; zentrale öffentliche Bedienhinweise SOLLEN langfristig in beiden Sprachen verfügbar werden. |

## 12. Liefergegenstände

### 12.1 Für jede freigegebene Formatversion

1. Eintrag im Formatkatalog einschließlich historischer Einordnung;
2. sprachunabhängige Formatbeschreibung;
3. dokumentierte Quellen und offene Fragen;
4. Erkennungs- und Validierungsregeln;
5. die zugesagten Lese- und/oder Schreibfähigkeiten;
6. positive, negative, abgeschnittene und Grenzfall-Testdaten;
7. erwartete strukturierte Ergebnisse und Diagnosekennungen;
8. gegebenenfalls Round-trip- und Konvertierungsfälle;
9. Nutzerhinweise zu Einschränkungen und Informationsverlusten.

### 12.2 Für die 1990-Gesamtfreigabe

| ID | Liefergegenstand | Abnahmeform |
|---|---|---|
| LAS-LIE-001 | Versionierter Quellcode der freigegebenen Bibliotheken | signiertes oder eindeutig bezeichnetes Release/Tag |
| LAS-LIE-002 | C++-Kommandozeilenkonverter | reproduzierbare Builds für festgelegte Referenzumgebungen |
| LAS-LIE-003 | Formatkatalog und Spezifikationen | geprüfte Dokumentation im Release |
| LAS-LIE-004 | Konformitätssuite und öffentlich verteilbarer Testkorpus | automatisierter, dokumentierter Testlauf |
| LAS-LIE-005 | Berichte historischer Werkzeugketten | protokollierte Ergebnisse und bekannte Abweichungen |
| LAS-LIE-006 | Anwender- und Entwicklerdokumentation | reviewbare Dokumente und Beispiele |
| LAS-LIE-007 | Lizenz-, Herkunfts- und Drittkomponentenübersicht | vollständige Release-Unterlagen |
| LAS-LIE-008 | Änderungs- und Einschränkungsübersicht | Release Notes |
| LAS-LIE-009 | Abnahmebericht | Zuordnung aller MUSS-Anforderungen zu Nachweisen |

## 13. Priorisierung

Die Reihenfolge folgt Risiko und Wiederverwendbarkeit, nicht allein der
Bekanntheit eines Formats.

| Priorität | Bedeutung | Typische Inhalte |
|---|---|---|
| MUSS | Ohne Erfüllung keine 1990-Gesamtfreigabe | Katalog, Spezifikationen, sichere Parser, transparente Verluste, Konformität, Kern-CLI |
| SOLL | Hoher Nutzen; Abweichung nur begründet | zusätzliche historische Toolchains, Streaming, mehrere Sprachbibliotheken, zweisprachige Kerndokumentation |
| KANN | Erweiterung nach gesicherter Basis | Komfortfunktionen, zusätzliche Sprachen und weitere Ausgabeprofile |
| SPÄTER | Bewusst außerhalb der Epoche | Access, JPEG, moderne Office- und Webformate, spätere C++-Standards |

Für die Umsetzung gilt folgende fachliche Staffelung:

1. Projektregeln, Quellenmodell, Coverage-Matrix und Konformitätsrahmen;
2. einfache Text- und Tabellenaustauschformate;
3. dBASE-Familie samt relevanten Begleitdaten;
4. Tabellenkalkulationsformate;
5. Dokumentformate;
6. Rastergrafik;
7. Vektor-, CAD-, Metadatei- und Druckformate;
8. breite Konvertierungsrouten, Härtung und Gesamtfreigabe.

| ID | Anforderung |
|---|---|
| LAS-PRI-001 | Sicherheit, Korrektheit und Prüfbarkeit MÜSSEN Vorrang vor zusätzlicher Formatbreite haben. |
| LAS-PRI-002 | Lesen und Validieren SOLLEN vor dem Schreiben derselben komplexen Variante stabilisiert werden. |
| LAS-PRI-003 | Eine Konvertierungsroute SOLL erst freigegeben werden, wenn Quellleser und Zielschreiber unabhängig geprüft sind. |
| LAS-PRI-004 | Eine SOLL-Abweichung MUSS im Abnahmebericht mit Auswirkung und Folgeplanung erscheinen. |

## 14. Abnahme

### 14.1 Abnahme einer einzelnen Formatversion

| ID | Kriterium |
|---|---|
| LAS-ABN-001 | Identität, historischer Zeitraum und Abgrenzung der Version MÜSSEN dokumentiert sein. |
| LAS-ABN-002 | Quellen und etwaige Widersprüche MÜSSEN dokumentiert sein. |
| LAS-ABN-003 | Der ausgewiesene Fähigkeitsstand MUSS vollständig durch automatisierte Tests belegt sein. |
| LAS-ABN-004 | Gültige, ungültige, abgeschnittene und ressourcenintensive Eingaben MÜSSEN angemessen geprüft sein. |
| LAS-ABN-005 | Nicht unterstützte Elemente und Auswirkungen MÜSSEN erkennbar sein. |
| LAS-ABN-006 | Schreibunterstützung MUSS mit unabhängigen Prüfungen oder dokumentierten Referenzprogrammen plausibilisiert sein. |
| LAS-ABN-007 | Round-trip-Kriterien MÜSSEN vor ihrer Prüfung fachlich definiert sein. |
| LAS-ABN-008 | Konvertierungen MÜSSEN Inhaltserhaltung und Verlustbericht getrennt prüfen. |
| LAS-ABN-009 | Testdatenrechte und Provenienz MÜSSEN geklärt sein. |
| LAS-ABN-010 | Dokumentation, Beispiele und Coverage-Matrix MÜSSEN mit dem gelieferten Verhalten übereinstimmen. |

### 14.2 Abnahme der 1990-Epoche

Die Gesamtfreigabe ist erreicht, wenn:

- alle für die Freigabe vereinbarten Formatversionen einzeln abgenommen sind;
- keine offene MUSS-Anforderung ohne genehmigte Änderung verbleibt;
- alle Referenzbauten und Konformitätstests dokumentiert durchlaufen;
- bekannte Sicherheitsprobleme mit hoher oder kritischer Auswirkung behoben
  oder die betroffene Funktion aus der Freigabe entfernt sind;
- Bibliotheken und Konverter dieselben veröffentlichten Formatstände melden;
- alle Liefergegenstände vorliegen;
- der Auftraggeber den Abnahmebericht bestätigt.

| ID | Kriterium |
|---|---|
| LAS-GES-001 | Der Release MUSS einen unveränderlichen Tag und eine eindeutige Versionsnummer besitzen. |
| LAS-GES-002 | Der Release MUSS den Stichtag 1990 einhalten und spätere Funktionen klar ausschließen. |
| LAS-GES-003 | Alle MUSS-Anforderungen MÜSSEN im Abnahmebericht mit Test, Dokument, Review oder begründeter Nichtanwendbarkeit verknüpft sein. |
| LAS-GES-004 | Alle im Release als stabil bezeichneten Fähigkeiten MÜSSEN die gemeinsame Konformitätssuite bestehen. |
| LAS-GES-005 | Ein Neuaufbau in den festgelegten Referenzumgebungen MUSS anhand der veröffentlichten Anleitung möglich sein. |
| LAS-GES-006 | Die Freigabe MUSS bekannte Einschränkungen, zurückgestellte Kandidaten und offene Forschungsfragen enthalten. |
| LAS-GES-007 | Eine nachfolgende Sprachepoche DARF erst beginnen, wenn der 1990-Stand referenzierbar und reproduzierbar gesichert ist. |

## 15. Erfolgsmessung

Die erste Freigabe wird nicht allein an der Zahl von Formaten gemessen. Erfolg
ist eine Kombination aus belegter Abdeckung und Vertrauenswürdigkeit.

| Kennzahl | Aussage | Ziel für eine freigegebene Fähigkeit |
|---|---|---|
| Anforderungsabdeckung | Anteil verknüpfter MUSS-Anforderungen | 100 % mit Nachweis oder genehmigter Nichtanwendbarkeit |
| Konformität | Verhalten gegenüber gemeinsamen Fällen | 100 % der für den Status verpflichtenden Fälle |
| Diagnoseabdeckung | Sichtbarkeit bekannter Verlust- und Fehlerfälle | 100 % der spezifizierten Fälle |
| Provenienzabdeckung | Rechtliche und fachliche Herkunft der Testdaten | 100 % der veröffentlichten Korpusdateien |
| Reproduzierbarkeit | Nachvollziehbarkeit eines Release-Builds | alle festgelegten Referenzumgebungen |
| Statusgenauigkeit | Übereinstimmung von Dokumentation und Verhalten | keine bekannte Übertreibung des Supportstatus |

| ID | Anforderung |
|---|---|
| LAS-MES-001 | Messwerte MÜSSEN auf versionierten Eingaben, Werkzeugen und Regeln beruhen. |
| LAS-MES-002 | Fehlende Testabdeckung DARF NICHT als erfolgreiche Unterstützung interpretiert werden. |
| LAS-MES-003 | Qualitätskennzahlen SOLLEN je Formatversion und für das Gesamtprojekt veröffentlicht werden. |

## 16. Randbedingungen und Abhängigkeiten

- Das Projekt wird öffentlich unter der MIT-Lizenz entwickelt.
- Die gedruckten Bücher stehen dem Auftraggeber zur Recherche zur Verfügung,
  werden jedoch nicht in das Repository kopiert.
- Historische Compiler können proprietär, schwer erhältlich oder nur in
  emulierten beziehungsweise virtuellen Umgebungen ausführbar sein.
- Nicht alle historischen Dateivarianten sind vollständig dokumentiert.
- Originalanwendungen und Referenzdateien können Lizenzbeschränkungen
  unterliegen.
- Git und das öffentliche Repository bilden die nachvollziehbare
  Versionsgeschichte.
- Der bisherige Aufwand für die 1990-Epoche wird grob mit 750 bis 900 kleinen,
  prüfbaren Commits veranschlagt; dies ist eine Planungshypothese, keine
  Abnahmebedingung.

| ID | Anforderung |
|---|---|
| LAS-RAN-001 | Fehlende proprietäre Werkzeuge DÜRFEN freie Referenzbauten und Kernprüfungen NICHT blockieren. |
| LAS-RAN-002 | Historische Toolchain-Nachweise MÜSSEN Version und Umgebung nennen. |
| LAS-RAN-003 | Externe Abhängigkeiten MÜSSEN inventarisiert, lizenziert und für den jeweiligen Release festgelegt sein. |
| LAS-RAN-004 | Ein Format ohne ausreichende Quellen- oder Testlage MUSS zurückgestellt werden dürfen. |

## 17. Risiken und Gegenmaßnahmen

| Risiko | Auswirkung | Erwartete Gegenmaßnahme |
|---|---|---|
| Widersprüchliche Dokumentation | falsche Interpretation | mehrere Quellen, markierte Unsicherheit, Referenzdateien |
| Ungeklärte Testdatenrechte | Korpus nicht veröffentlichbar | Provenienzprüfung, synthetische oder freigegebene Dateien |
| Variantenexplosion | unüberschaubarer Umfang | versionsgenaue Coverage-Matrix und priorisierte Profile |
| Paarweise Konverterexplosion | hoher Pflegeaufwand | fachlich gemeinsame Modelle und selektive Routen |
| Beschädigte oder bösartige Eingaben | Absturz oder Ressourcenverbrauch | harte Grenzen, Negativtests, Sicherheitsreviews |
| Alte Compiler fehlen | historischer Build nicht belegbar | frei verfügbare Baseline, dokumentierte lokale Nachweise |
| Moderne Annahmen verfälschen Historie | inkompatible Ausgaben | Stichtagsregel, Referenzprogramme, versionsgebundene Writer |
| Zu frühe API-Festlegung | spätere Brüche | Reifegrade, experimentelle Kennzeichnung, ADRs |
| Umfang wächst unkontrolliert | Freigabe verzögert sich | Epochen, MUSS-Umfang und Change Control |
| Sprachimplementierungen driften auseinander | unterschiedliche Resultate | gemeinsame Spezifikation, Diagnosen und Konformitätssuite |

| ID | Anforderung |
|---|---|
| LAS-RIS-001 | Risiken MÜSSEN während der Entwicklung gepflegt und vor jeder Freigabe neu bewertet werden. |
| LAS-RIS-002 | Ein akzeptiertes Restrisiko MUSS Verantwortlichen, Begründung und Gültigkeitsdauer nennen. |
| LAS-RIS-003 | Sicherheits- oder Rechtsrisiken DÜRFEN NICHT allein aus Termin- oder Komfortgründen akzeptiert werden. |

## 18. Änderungs- und Entscheidungsverfahren

1. Änderungswunsch mit Motivation und betroffenen Anforderungen erfassen.
2. Auswirkung auf Epoche, Formate, Termine, Kompatibilität, Sicherheit und
   Rechte bewerten.
3. Entscheidung durch Auftraggeber/Product Owner dokumentieren.
4. Lastenheft bei fachlicher Änderung und Pflichtenheft bei technischer
   Auswirkung gemeinsam aktualisieren.
5. Tests, Coverage-Matrix, Roadmap und Releaseplanung nachziehen.

| ID | Anforderung |
|---|---|
| LAS-AEN-001 | Eine fachliche Umfangsänderung MUSS vor Implementierungsfreigabe bewertet werden. |
| LAS-AEN-002 | Entfernte oder verschobene MUSS-Anforderungen MÜSSEN mit Begründung in der Änderungshistorie erscheinen. |
| LAS-AEN-003 | Architekturentscheidungen DÜRFEN das fachliche Ziel nicht stillschweigend verändern. |
| LAS-AEN-004 | Abnahmekriterien MÜSSEN vor der jeweiligen Abnahme feststehen. |

## 19. Rückverfolgbarkeit zum Pflichtenheft

Das Pflichtenheft verfeinert die Anforderungen dieses Dokuments. Die folgende
Matrix definiert die primäre Beziehung; einzelne technische Anforderungen
können mehrere Lasten abdecken.

| Lastenheft-Bereich | Erwartete Konkretisierung im Pflichtenheft |
|---|---|
| LAS-DOK, LAS-AUS, LAS-ZIE | Dokumentregeln, Architekturziele, Definitionen |
| LAS-SCP, LAS-EPO, LAS-FMT | Komponenten, Epochenmodell, Coverage- und Statusmodell |
| LAS-ERK, LAS-LES, LAS-VAL | Erkennungs-, Reader- und Validatorverträge |
| LAS-SCH, LAS-KON, LAS-REC | Writer, Konvertierung, Verlustmodell und Recovery |
| LAS-CLI, LAS-API | Kommandozeilen- und Bibliotheksschnittstellen |
| LAS-QUA, LAS-SEC, LAS-LEI | Qualitäts-, Sicherheits- und Ressourcenanforderungen |
| LAS-POR | Plattformabstraktion, Compilerprofile und Sprachepochen |
| LAS-QUE, LAS-DOC | Quellenmodell, Korpusregeln und Dokumentation |
| LAS-LIE, LAS-ABN, LAS-GES | Liefer-, Prüf- und Releaseverfahren |

| ID | Anforderung |
|---|---|
| LAS-TRA-001 | Jede MUSS-Anforderung MUSS spätestens vor der Implementierung einer zugehörigen Funktion mindestens einem Pflichtenheftpunkt zugeordnet sein. |
| LAS-TRA-002 | Jeder Abnahmenachweis MUSS auf Anforderungskennung, Produktversion und Prüfergebnis verweisen. |
| LAS-TRA-003 | Eine nicht umgesetzte Anforderung MUSS im Abnahmebericht als offen, verschoben, nicht anwendbar oder abgelehnt gekennzeichnet sein. |
| LAS-TRA-004 | Automatisierbare Rückverfolgbarkeitsprüfungen SOLLEN Bestandteil der Projektqualitätssicherung sein. |

## 20. Offene fachliche Entscheidungen

Die folgenden Punkte sind noch nicht abschließend vereinbart. Sie blockieren
das Lastenheft als Zielbild nicht, müssen aber vor dem jeweils betroffenen
Meilenstein entschieden werden.

| Kennung | Offene Entscheidung | Fällig vor |
|---|---|---|
| OFF-LAS-001 | Verbindliche Mindestliste der Formatversionen für die 1990-Gesamtfreigabe statt Kandidatenliste | Abschluss Format-Inventar |
| OFF-LAS-002 | Genaue historische Compiler- und Versionsmatrix | erster Retro-Build-Meilenstein |
| OFF-LAS-003 | Priorität und Startpunkt der C#- und Java-Implementierungen | Freigabe der zweiten Sprachbibliothek |
| OFF-LAS-004 | Dauerhafte Kennzahlen und Schwellenwerte für Leistungsregressionen | Performance-Baseline |
| OFF-LAS-005 | Veröffentlichungsweg für große, rechtssichere Testkorpora | erster umfangreicher Korpus-Release |
| OFF-LAS-006 | Sprachpolitik für vollständige zweisprachige Dokumentation | erster stabiler öffentlicher Release |
| OFF-LAS-007 | Fachlicher Umfang der ersten Nachfolgeepoche, insbesondere Access und JPEG | Planung nach 1990-Abnahme |

Offene Entscheidungen sind keine stillschweigenden Zusagen. Nach ihrer Klärung
werden die betroffenen Anforderungen und Abnahmekriterien aktualisiert.

## 21. Definition des erfolgreichen 1990-Abschlusses

SASD Moschus hat die erste Epoche erfolgreich abgeschlossen, wenn ein Dritter
anhand des veröffentlichten Releases nachvollziehen kann:

1. welche bis Ende 1990 existierenden Formatversionen tatsächlich unterstützt
   werden;
2. worauf die jeweilige Interpretation beruht;
3. welche Dateien erkannt, gelesen, geprüft und geschrieben werden können;
4. welche Konvertierungen fachlich sinnvoll und geprüft sind;
5. welche Informationen bei jeder Umwandlung erhalten, angenähert oder
   verworfen werden;
6. wie sich Fehler, Mehrdeutigkeiten und beschädigte Dateien auswirken;
7. dass die zugesagten Ergebnisse die gemeinsame Konformitätssuite bestehen;
8. dass der portable Kern und der C++-Konverter in den vereinbarten
   Referenzumgebungen gebaut werden können;
9. dass Quellen, Testdatenrechte und bekannte Grenzen transparent sind;
10. dass dieser Stand auch nach Beginn späterer Format- und C++-Epochen
    reproduzierbar erhalten bleibt.

Damit ist „1990 abgeschlossen“ keine bloße Jahreszahl und keine Sammlung von
Parsern, sondern ein überprüfbarer, dokumentierter und langfristig nutzbarer
Produktstand.

## 22. Änderungshistorie

| Version | Datum | Änderung |
|---|---|---|
| 0.1 | 21. Oktober 2026 | Erstfassung des fachlichen Lastenhefts; Abgrenzung zum Pflichtenheft, 1990-Umfang, Nutzerbedarf, Qualität, Lieferungen und Abnahme |
