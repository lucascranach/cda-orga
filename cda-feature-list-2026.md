---
tags:
  - projekt
status: aktiv
date: 2026-08-25
---

# Feature-Liste: Alle Features, die in der letzten Förderphase implementiert wurden

Vollständige Liste aller Features, sortiert nach Komponente und chronologisch. Zweck: Kontext- und Nachschlagewerk, nicht für den direkten Abdruck im Bericht gedacht, sondern als Grundlage, um Berichtstexte zu schreiben und zu prüfen, ob etwas Relevantes fehlt. Format pro Eintrag: **Feature (Zeitraum)**, dann technische Umsetzung, dann Projektrelevanz (Bezug zu den Zielen dieser Förderphase, Antrag 2022, Teil I Erschließung/Digitalisierung/Vernetzung, Teil II interdisziplinäre Erforschung/Vermittlung).

Grundlegendes zur Architektur selbst (Importer-Neubau, Aufsplittung in Services) steht separat in [[Microservices-Architektur]], hier nur die Features darauf aufbauend.

## Importer

- **Zeichnungen als eigene Werkgattung** (Juli 2024). Neues Modul src/Modules/Drawings/, ca. 4.500 Zeilen, eigene Datenstruktur, Bildanbindung, Suchlogik. Kernziel der Phase: Aufnahme der neuen Werkgattung Zeichnungen neben Gemälden, Grafik, Archivalien.
- **Werkbeziehungen systematisch erfasst** (2024). ReferenceDivider.php, Beziehungstypen (Gegenstück, Serie, Wasserzeichen etc.), Dublettenbereinigung. Antragsziel Vernetzung: Werke als Netz statt isolierter Datensätze lesbar.
- **Terminologische Präzisierungen** (2024). Begriffsvereinheitlichung in Filterlisten (Anonyme → Unbekannte Meister etc.). Einheitliche Fachterminologie im gesamten Bestand.
- **Druckzustand/Auflagennummer als eigene Merkmale** (2024). Feld editionNumber, sortierbar. Zentral für die im Antrag beschriebene Erschließungslogik der Druckgrafik (Motiv/Zustand/Abzug/Auflage).
- **Laufende Sammlungspflege** (2024). Neue Standorte (Heidelberg, Bomann-Museum Celle, Berkeley u. a.), Korrekturen. Vollständigkeit des Bestands.
- **Restaurierungsdokumentation als eigener Datenstrang** (2025). Modul src/Modules/Restorations/, auch für Zeichnungen. Antragsziel: kunsttechnologische Befunde strukturiert integrieren, nicht nur als Anhang.
- **Neue Editionsstruktur bei Grafik** (Juli 2025). Fachliche Zuordnungstabelle Auflage.txt, ca. 2.000 Einträge. Präzisierung Druckzustand/Auflage, Kernthema Druckgrafik-Erschließung.
- **Zeichnungen fertiggestellt** (2025). Anbindung Suchindex, Filterwerte, Bildzuordnung. Abschluss der neuen Werkgattung.
- **Downloadangebot pro Bild** (2025). Rechtestatus pro Abbildung mitgeführt. Differenzierte, korrekte Rechteausweisung statt pauschal.
- **Selektiver Import + automatisierte Indexübergabe** (2025). elastic-import.sh. Betriebsfähigkeit: Redaktionszyklen von Stunden auf Minuten verkürzt.
- **TMS-Sprachfeld-Fix** (Aug./Nov. 2025). Reaktion auf zwei Änderungen der TMS-Exportstruktur. Datenqualität, Robustheit gegenüber externen Systemänderungen.
- **Redaktionelle Publikationssteuerung** (2026). ExcludeByInventoryNumberPrefix.php. Kuratorische Kontrolle direkt aus der Quelldatenbank, ohne technischen Eingriff.
- **Schlagwort-Hierarchien** (2026). KeywordParentTermExtender.php, Vererbung von Abzug auf Werk. Recherchequalität, Vernetzung von Ober-/Unterbegriffen.
- **Referenzexemplare** (2026). Merkmal isBestOf. Auswahl eines Referenzabzugs pro Motiv.
- **Neue Rolle „Officin"** (2026). Beteiligtenzuordnung erweitert. Erschließungstiefe Druckgrafik (Antragsziel).
- **Weitere Sammlungserschließung inkl. Verlustkategorie** (Mai 2026). Neue Standorte (u. a. Dresden), Kategorie „nicht erhalten". Vollständigkeit, Sichtbarkeit von Kriegs-/Sammlungsverlusten.
- **Bereinigungen Inventarnummern/Sortierung** (2026). Technische Präfixe entfernt, Sprachverweis-Fehler behoben. Datenqualität.

## Cranach API

- **Eigener Zugang für Zeichnungen** (2024). Endpunkt /drawings, Objekttyp DRAWING. Neue Werkgattung gattungsspezifisch recherchierbar.
- **Geodaten-Endpunkt** (2024). /geodata, GeoJSON-Standard. Grundlage für das im Antrag genannte „Geographical Mapping".
- **Caching/Kompression** (2024). Zwischenspeicherung häufiger Abfragen. Performance, wichtig für internationale Nutzung.
- **Kuratorische Steuerung der Auslieferung** (2024). Objekte gezielt von Auslieferung ausnehmbar (Rechte/Leihgeber). Rechtekonforme Veröffentlichung ohne Datenverlust.
- **Datierung in Freitextsuche** (2024). Suchindex erweitert. Recherchequalität.
- **Betriebsüberwachung** (2025). Prometheus-Monitoring: Auslastung, Antwortzeit, Fehlerhäufigkeit. Nachhaltige Betriebsfähigkeit, Voraussetzung für Langzeitangebot.
- **Fehlerbehandlung bei Suchindex-Ausfall** (2025). Kontrollierte Antworten, Cache-Fix gegen fehlerhafte Zwischenspeicherung. Datenqualität, Verlässlichkeit.
- **Verknüpfung Werk zu Nachdrucken** (2025). Neues Datenmodell-Element. Erschließungstiefe Druckgrafik, Rezeptionsaspekt.
- **Feldkorrektur Besitzer/Institution** (2025). Trennung Besitzer vs. bewahrende Institution (repository). Fachliche Korrektheit.
- **Transkriptionen/Kommentare bei Archivalien** (2026, bis April). Volltext über API abrufbar und durchsuchbar. Antragsziel Vermittlung: Quellenarbeit auf Volltextebene statt nur Metadaten.
- **Aggregation Nachdrucke-Zahl** (2026). Gesamtzahl zu beliebiger Auswahl abrufbar. Neue quantitative Auswertungsform (Antragsziel).
- **Korrektur Filter naturwissenschaftliche Untersuchungsdaten** (2026). Fix examination_analysis, leere Kategorien ausgeblendet. Kunsttechnologische Daten korrekt zugänglich.

## Cranach Search

- **CDA-Logo-Integration, Sprachauszeichnung** (Feb. 2024). Barrierefreiheits-Fix (Screenreader-Sprache). Zugänglichkeit.
- **Terminologie Klassifikation → Medium** (2024). Umbenennung durchgängig. Einheitliche Fachterminologie zwischen Suche und Datenbestand.
- **Nutzungsstatistik** (April 2024). Matomo, datenschutzfreundlich. Empirischer Nutzungsnachweis für DFG-Bericht.
- **Automatisierte Veröffentlichung** (Juli 2024). Release-Pipeline. Betriebsfähigkeit.
- **Barrierefreiheits-Durchgang** (Aug. 2025). Volle Tastaturbedienbarkeit, Fokusmarkierung der Filter-Seitenleiste. Zugänglichkeit für öffentlich gefördertes Archiv.
- **Filter für Zeichnungen** (2025). Neue Filterkategorie. Neue Werkgattung nutzbar gemacht.
- **Nachdrucke/Versionen-Anzeige** (Jan.–Aug. 2026). Trefferanzahl in Kachel-, Listen-, Zeitleistenansicht. Überlieferungsdichte auf einen Blick sichtbar (Erschließungstiefe Druckgrafik).
- **Mobile Navigation** (Mai 2026). Einklappbares Menü, responsives Layout. Nutzbarkeit unterwegs/im Depot.
- **Umgang mit unbekannten Personen** (Mai 2026). Saubere Kennzeichnung statt Leerstelle. Datenqualität bei Werkstattproduktion.
- **Getrennte Umgebungen, Versionierung 1.0.0** (Mai–Aug. 2026). Vorschau/Produktiv getrennt, vollautomatischer Deploy. Betriebsreife.

## Cranach Artifacts

- **Automatische Auslieferungskette** (2024). Interner + öffentlicher Deploy, geschützter Vorschaubereich. Redaktionelle Prüfung vor Veröffentlichung, Betriebsfähigkeit.
- **Gesamtübersicht („Overall Overview")** (2024). Neue Übersichtsansicht pro Objekt. Bessere Objektdarstellung.
- **Verwandte Werke bei Grafiken** (2024). Bezüge zwischen Abzügen dargestellt. Grafik im Werkzusammenhang statt als Einzelblatt.
- **Officin als eigenes Feld** (2024). Eigenständige Angabe. Erschließungstiefe Druckgrafik.
- **Freigabesteuerung isPublished** (2024). Objektstatus. Kontrolle über unpublizierte Forschungsdaten.
- **Bildbeschriftungs-Werkzeug** (2024). Admin-Tool zur Erzeugung von Bildunterschriften. Redaktionseffizienz.
- **Nutzungsstatistik** (2024). Matomo. Nutzungsnachweis.
- **Trennung Inschriften/Bezeichnungen** (2025). Eigene Abschnitte, auch für Grafiken. Kunsthistorische Präzision (Signatur ≠ spätere Beschriftung).
- **GND-Einbindung** (2025). Normdatenverknüpfung im Frontend sichtbar. Antragsziel Vernetzung mit bibliothekarischer/musealer Datenwelt.
- **Evolving-Edition-Integration** (2025). Überarbeitete Zustands-/Auflagendarstellung. Kernthema Druckgrafik-Erschließung.
- **Overlay verwandte Werke** (2025). Bezüge im Kontext aufklappbar. Nutzbarkeit der Vernetzung.
- **Bild-Download mit Größenauswahl** (2025). Auflösungsstufen wählbar. Nutzungskomfort für Forschung.
- **Material/Technik als Fließtext** (2025). Umstellung von Tabellendarstellung. Lesbarkeit.
- **EXIF-Metadatenanbindung** (2026). Live-Abruf aus Bilddatei (Fotograf, Rechteinhaber, Datum, Aufnahmeart), „Metadaten-Schubfach". Automatisch korrekte Bildnachweise statt manueller Pflege.
- **Datierung/Verwendung bei Grafiken getrennt** (März 2026). Zwei unterschiedliche Angaben statt einer. Fachlich erhebliche Präzisierung.
- **Drucker/Verleger/Officinen sichtbar** (2026). Aus Datenbank ins Frontend geholt. Erschließungstiefe Druckgrafik.
- **Fachredaktionelle Fehlerkorrekturen** (2026). Diverse, referenziert auf Ticketsystem. Datenqualität.
- **Download in voller Auflösung** (Juli 2026). Serverseitig begrenzte Maximalgröße. Nutzungskomfort, kontrollierte Ressourcennutzung.

## Cranach Map

- **Kartendarstellung mit Clustering** (Herbst 2024). React-App, automatische Gruppierung eng beieinanderliegender Werke. Setzt das im Antrag genannte „Geographical Mapping" um.
- **Standortgruppierte Trefferliste + Demo-Datensatz** (Okt. 2024). Gruppierung nach Standort statt Flachliste. Bildet museale Realität ab (Ballung in wenigen Sammlungen), Demo für Lehre/Präsentation.
- **UI-Feedback-Runde** (Ende Okt. 2024). Kartenausschnitt Mitteleuropa, Kontrastverbesserung. Fachliche Qualitätssicherung.
- **Kurznachweise in Ergebniskarten** (Nov./Dez. 2024). Abbildung, Titel, Datierung, Technik, Personen, Institution, Verlinkung ins CDA. Karte als Zugangsweg statt isoliertes Schaustück.
- **Produktivbetrieb** (Dez. 2024). Veröffentlichung unter /map. Betriebsfähigkeit.
- **Zweisprachigkeit + Einbettung** (Jan./Feb. 2025). Sprache aus URL übernommen, Kopfleiste mit Rücksprung zur Suche. Internationale Anschlussfähigkeit.
- **Feinschliff** (März 2025). Sprachbrüche, Layout-Überlappungen, Browser-Fixes behoben. Nutzbarkeit im Praxisbetrieb.
- **Nur publizierte Werke** (Juni 2026). Filter auf isPublished. Wissenschaftliche Verlässlichkeit der Darstellung.

## Cranach Timeline

- **Texture Atlas** (Aug. 2025). Alle Abbildungen in einem Bild zusammengefasst, GPU-Rendering. Performance-Grundlage, setzt „Time-Line Mapping" aus dem Antrag um.
- **Chronologische Sortierung, Obergrenze aufgehoben** (Sept. 2025). Jahresraster, gesamter Bestand darstellbar. Vollständigkeit der Darstellung.
- **Vier Ereignisstränge** (Sept. 2025). Biografie Cranach d. Ä./d. J., Luther, Zeitgeschichte parallel zur Werkleiste. Interdisziplinäre Kontextualisierung (Antragsziel Teil II).
- **Beschriftung, Farbcodierung, verwandte Ereignisse** (Okt. 2025). Anklickbare Detailkarten, Hervorhebung zusammenhängender Ereignisse. Gleichzeitigkeiten/Zusammenhänge sichtbar, die in linearer Chronik untergehen.
- **Seitenleiste mit Filter** (Okt. 2025). Objekttypfilter, Originalauflösung, Link zur Detailseite. Brücke zum bestehenden Archiv.
- **Mehrsprachigkeit + Design-Angleichung** (Nov./Dez. 2025). Alle Ereignistexte DE/EN, CDA-Erscheinungsbild übernommen. Integration in Gesamtauftritt.
- **Publikumstauglichkeit** (Jan.–März 2026). Cross-Browser, Mobile-Hinweis, Doku. Veröffentlichungsreife.
- **Zeitliche Eingrenzung, visueller Verbinder, Tastaturnavigation** (Jan.–März 2026). Werke nach 1585 ausgeblendet, Verknüpfung Ereignis↔Werkbereich. Fachlich begründete Eingrenzung, Zugänglichkeit.
- **Redaktionelle Überarbeitung** (Mai 2026). Rund 100 kuratierte Ereignisse, zweisprachig, durch Daniel Görres. Fachliche Qualitätssicherung des Ereignismaterials.

## Cranach Compare

Ursprünglich 2021/2022 entstanden, vor dieser Förderphase, aber als eigenständiger Service Teil der in dieser Phase aufgebauten Architektur und im Berichtszeitraum aktiv im Einsatz.

- **Geteilte Vergleichsfläche mit Tiefenzoom** (Juni 2021). Zwei koppelbare Tiefenzoom-Betrachter. Setzt „Image Comparison" aus dem Antrag um.
- **Adressierungslogik synchron zum Archiv** (Juni 2021). Werkkennung aus Inventarnummer + Objektbezeichnung, Unterscheidung Gemälde/Grafik. Konsistente Werkverweise archivweit.
- **Archivweiter Sammelkorb** (Mai 2022). Komponente cranach-collect, lokale Speicherung im Browser, ohne Login. Setzt „Image Annotation"/Sammelfunktion aus dem Antrag um, senkt Einstiegshürde.
- **Entfernen aus Sammlung** (Okt. 2022). Ergänzung zum Sammeln. Praktikabilität über längere Arbeitssitzungen.

## Cranach Extend Reality

Nicht im Antrag gefordert, zusätzlich entstanden.

- **Maßstabsgetreue Umrechnung** (März 2025). Maßangaben aus Archivdaten in reale Meter. Körperlichkeit der Werke räumlich erfahrbar.
- **Räumliche Anordnung nach Entstehungsdatum** (April 2025). Verworfene Alternative (Kurvenanordnung) dokumentiert in src/components/legacy/. Chronologie als abschreitbarer Weg.
- **Infotafeln, Rückseiten, individuelle Beleuchtung** (April 2025). Sich zuwendende Infotafeln, Rückseitenansicht der Tafelbilder. Rückseiten sonst in Ausstellungen praktisch nie zugänglich.
- **Vermessungsfunktion** (Mai 2025). Breite/Höhe in cm bei Zielen auf ein Werk. Kunsttechnologischer Mehrwert.
- **Teleportation/Fortbewegung** (Mai 2025). Für VR-Einsteiger überarbeitet. Zugänglichkeit für Laienpublikum.
- **Raumklang** (Mai 2025). Positionsabhängiger Klang. Immersion.
- **Abstandsabhängige Bildqualität** (Mai 2025). Auflösungsstufe wird je nach Betrachtungsabstand nachgeladen. Technische Voraussetzung für 101 gleichzeitig darstellbare Werke in hoher Qualität.
- **WebXR-Layer-Technik** (Mai 2025). Direktes Bild-Durchreichen an die Brille unter Umgehung der Standarddarstellung. Schärfere Bilddarstellung, methodisch interessantester Teil.
- **Steuerungs-Infografik, Klangkulisse** (Mai 2025). UI-Ergänzungen für Praxiseinsatz. Nutzbarkeit ohne Einweisung.
- **Technische Dokumentation** (Juli 2025). Weg „vom Archivdatensatz zum aufgehängten Bild". Nachvollziehbarkeit (Doku bislang nicht eingecheckt).

## LIDO-Export

- **Mapping am Einzelstück, GND-Verknüpfung** (Feb.–März 2026). Handgeschriebene Referenzdatensätze, Personen/Institutionen über GND. Antragsziel Vernetzung mit externen Portalen.
- **Musterdatensatz als Vorlage** (März–April 2026). Ein Holzschnitt (Schlossmuseum Coburg) vollständig durchgespielt. Konsistente Auslegung des Standards im Gesamtbestand.
- **Automatisierte Erzeugung aus der API** (April–Mai 2026). Werkzeug ruft LIDO-Datensätze direkt aus Cranach API ab. Export bleibt am Forschungsstand statt zu veralten.
- **Vereinheitlichte Werkkennungen** (Mai 2026). Präfixe bei Zeichnungen entfernt. Stabile Verweise unabhängig von Werkgattung.
- **Ein Datensatz statt Sprachdubletten** (Mai 2026). DE/EN im selben Datensatz. Kein doppeltes Anlegen bei Empfängersystemen.
- **Überführung Gesamtbestand** (Juni–Aug. 2026). Von 33 auf rund 1.700 Datensätze. Vollständigkeit des Exports.
- **Getrennter Prüf-/Produktivbestand** (ab Juli 2026). 33 Referenzdatensätze parallel geführt. Qualitätssicherung bei Mapping-Änderungen.
- **Kontrollierte Vokabulare** (durchgehend). Getty AAT, Wikidata, GND, ISIL statt freier Begriffe. Antragsziel Normdaten/Vokabulare, sammlungsübergreifende Recherche.
- **Ereignismodell Druckgrafik** (durchgehend). Entwurf/Herstellung/Publikation als getrennte Ereignisse. Zentrale Unterscheidung Entwerfer/Formschneider/Drucker/Verleger bleibt erhalten.
- **Rechtelage maschinenlesbar** (durchgehend). Lizenzangaben je Werk, Text, Bild. Voraussetzung für Übernahme durch Aggregatoren.
- **Literaturverknüpfung** (durchgehend). Rund 15.000 Nachweise verlinkt. Forschungsgeschichte bleibt an Daten gebunden.
