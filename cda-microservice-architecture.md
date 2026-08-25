---
tags:
  - projekt
status: aktiv
date: 2026-08-25
---

# Microservices-Architektur des Cranach Digital Archive

Baustein-Übersicht für den DFG-Abschlussbericht (technischer Teil). Beschreibt die einzelnen Services, aus denen die neue Architektur besteht: erst Funktion und Nutzen, danach die technische Umsetzung.

## Datenfluss im Überblick

Der Importer ist der Ausgangspunkt der Kette. Er liest die musealen Rohdaten (TMS-XML-Exporte) ein und erzeugt daraus für jedes Werk eine eigene, archivfähige JSON-Datei. Die Cranach API indexiert diese JSON-Dateien in ElasticSearch und stellt sie über eine REST-Schnittstelle allen anderen Services bereit. Cranach Search, Cranach Artifacts, Cranach Map, Cranach Timeline, Cranach Compare und Cranach Extend Reality sind eigenständige Anwendungen, die auf diese API zugreifen. Der LIDO-Export leitet zusätzlich einen eigenen, standardkonformen Datenexport direkt aus der API ab. Jeder Baustein lässt sich unabhängig weiterentwickeln, austauschen oder ausfallen lassen, ohne dass die anderen betroffen sind.

## Importer

**Funktion und Nutzen.** Bindeglied zwischen der museumsinternen Objektdatenbank und dem öffentlichen Archiv. Prüft, ergänzt, verknüpft und sortiert die Rohdaten und erzeugt daraus die durchsuchbaren Datenbestände der Website. Jede redaktionelle Änderung an der Quelle wirkt sich über den Importer unmittelbar darauf aus, was im Archiv sichtbar ist.

**Technisch.** PHP-basiert. Verarbeitet TMS-XML-Exporte zu strukturierten, sowohl maschinen- als auch menschenlesbaren JSON-Dateien, ein Verzeichnis pro Werk, mit allen Feldern, Rollen, Datierungen und Rechtevermerken. Löst Werkbeziehungen (Serie, Gegenstück, Wasserzeichen), Schlagwort-Hierarchien und Normdaten-Verknüpfungen (GND) auf. Redaktionelle Publikationssteuerung über ein Präfix in der Inventarnummer. Die JSON-Dateien sind bewusst unabhängig vom Gesamtsystem archivfähig, damit die Forschungsdaten auch ohne laufendes CDA nachnutzbar bleiben.

## Cranach API

**Funktion und Nutzen.** Datenschnittstelle zwischen dem Bestand und allen Anwendungen, die diese Daten anzeigen: Website, Kartenansichten, externe Nutzungen. Liefert Werke, Archivalien, Literaturreferenzen und Zeichnungen als strukturierte, filter- und durchsuchbare Datensätze.

**Technisch.** Node.js, ElasticSearch als Suchindex, REST-API. Facettierte Suche mit Trefferanzahl pro Filter. Eigener Geodaten-Endpunkt liefert GeoJSON für Kartenanwendungen. Caching und Kompression für häufig aufgerufene Abfragen. Eigenes Monitoring (Prometheus): Auslastung, Antwortzeiten, Fehlerhäufigkeit, kontrollierte Fehlerbehandlung bei Ausfall des Suchindex.

## Cranach Search

**Funktion und Nutzen.** Zentrale Such- und Rechercheoberfläche des Archivs. Werke lassen sich finden, filtern und in verschiedenen Ansichten betrachten (Kacheln, Liste, Zeitleiste, Karte), letztere beiden als Einstieg in Cranach Timeline und Cranach Map.

**Technisch.** Eigenständige React-Anwendung, kommuniziert ausschließlich über die Cranach API. Mobile Navigation über einklappbares Menü. Vollständig per Tastatur bedienbar, sichtbare Fokusmarkierung, geprüft mit Screenreadern.

## Cranach Artifacts

**Funktion und Nutzen.** Objektebene des Archivs: die Einzeldarstellung eines Gemäldes oder einer Grafik mit allen zugehörigen Daten, Abbildungen und Forschungsergebnissen.

**Technisch.** Statisch generiert mit dem Static-Site-Generator 11ty, dadurch hohe Performance und gute Auffindbarkeit über Suchmaschinen. Automatische Auslieferungskette inklusive geschütztem Vorschaubereich für redaktionelle Prüfung vor Veröffentlichung. EXIF-Metadaten der Bilddateien werden live aus der Quelle abgerufen und angezeigt (Fotograf, Rechteinhaber, Aufnahmedatum, Aufnahmeart). Freigabesteuerung pro Objekt (isPublished).

## Cranach Map

**Funktion und Nutzen.** Interaktive Landkarte, die den Bestand geografisch erschließt: zeigt auf einen Blick, wo Cranach-Werke heute liegen, mit direktem Sprung in den zugehörigen Archiveintrag. Ein zweiter, explorativer Zugangsweg neben Suche und Filter.

**Technisch.** React-Anwendung, eingebettet unter /map als Teil des CDA-Webauftritts. Automatische Bündelung eng beieinanderliegender Werke zu Gruppen (Clustering), die sich beim Zoomen auffächern. Ergebnisliste nach besitzenden Orten gruppiert. Lädt ausschließlich publizierte Werke. Zweisprachig, Sprache wird aus der Adresse übernommen.

## Cranach Timeline

**Funktion und Nutzen.** Zeigt das Werk Lucas Cranachs d. Ä. und d. J. erstmals als durchgehendes visuelles Kontinuum: eine Fläche, über die man von 1472 bis in die 1580er Jahre scrollt, mit jedem einzelnen Werk als Bild, chronologisch einsortiert und mit vier parallelen Ereignissträngen (Biografie Cranach d. Ä., Biografie Cranach d. J., Luther, allgemeine Zeitgeschichte) hinterlegt.

**Technisch.** WebGL-basiert. Ein „Texture Atlas" fasst alle Abbildungen in einem einzigen großen Bild zusammen, um mehrere tausend Werke flüssig im Browser darstellen zu können. Jedes Werk verlinkt per Klick direkt in den zugehörigen Cranach-Artifacts-Eintrag. Zweisprachig, an das Erscheinungsbild des Archivs angeglichen.

## Cranach Compare

**Funktion und Nutzen.** Werkzeug zum direkten visuellen Vergleich zweier Bildaufnahmen, insbesondere unterschiedlicher Aufnahmearten desselben Werks (Gesamtaufnahme, Infrarotreflektografie, UV-Licht, Röntgen, Streiflicht u. a.). Kunsttechnologischer Kern: Sichtbares gegen Unterzeichnung, Zustand vor gegen Zustand nach einer Restaurierung.

**Technisch.** Zwei gekoppelte Tiefenzoom-Betrachter nebeneinander, Zoom und Ausschnitt lassen sich synchron führen. Archivweiter Sammelkorb (Komponente cranach-collect): Abbildungen lassen sich beim Stöbern im Archiv mit einem Klick sammeln, die Sammlung wird lokal im Browser gespeichert, ohne Login. Ursprünglich 2021/2022 entstanden, seither als eigenständiger Service Teil der Architektur.

## Cranach Extend Reality

**Funktion und Nutzen.** Begehbare virtuelle Galerie mit Cranach-Meisterwerken, direkt im Browser einer VR-Brille nutzbar, ohne Installation. Gemälde erscheinen maßstabsgetreu in ihrer realen Größe und chronologisch entlang einer Zeitachse angeordnet, macht Körperlichkeit und zeitliche Entwicklung des Œuvres räumlich erfahrbar.

**Technisch.** WebXR, läuft auf Meta Quest über einen Link. Bildgrößen werden aus den Maßangaben des Archiv-Datensatzes in echte Meter umgerechnet. Abstandsabhängiges Nachladen der Bildauflösung, damit auch bei 101 gleichzeitig dargestellten Werken keine Performance-Einbrüche auftreten. Erprobung der WebXR-Layer-Technik für schärfere Bilddarstellung direkt in der Brille. Über die Antragsziele hinaus entstanden.

## LIDO-Export

**Funktion und Nutzen.** Überführt den Werkbestand in LIDO, den international abgestimmten Austauschstandard für Museumsobjektdaten. Bedingung dafür, dass die Forschungsdaten an Aggregatoren wie die Deutsche Digitale Bibliothek oder Europeana geliefert und außerhalb des eigenen Projekts nachgenutzt werden können.

**Technisch.** Wird automatisiert aus der Cranach API abgeleitet, kein manuell gepflegter Einmalexport, sondern eine wiederholbare Ableitung, die mit jedem Durchlauf den aktuellen Forschungsstand abbildet. Kontrollierte Vokabulare statt freier Begriffe (Getty AAT, Wikidata, GND, ISIL). Ereignisbasiertes Modell für die druckgrafische Differenzierung (Entwurf, Herstellung, Publikation). Produktivbestand: rund 1.700 Datensätze (Stand August 2026), deckt Druckgrafik und Zeichnungen ab, Gemälde folgen im nächsten Schritt.
