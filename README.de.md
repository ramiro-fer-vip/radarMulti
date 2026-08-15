# Radar Multi – Benutzerdefiniertes Power-BI-Visual

Benutzerdefiniertes Radar- bzw. Spinnennetzdiagramm mit Unterstützung für mehrere Segmente und Messwerte.

### Gesamtanzahl der Punkte nach Kategorie

![Gesamtanzahl der Punkte nach Kategorie](Radar/Total%20Points%20-%20Category.png)

## Hauptfunktionen

- **Interaktives Radardiagramm** mit kategorialen Achsen und konfigurierbaren Rasterebenen
- **Unterstützung mehrerer Segmente**: Mehrere Reihen im selben Diagramm vergleichen
- **Mehrere Messwerte**: Mehrere Messwerte gleichzeitig mit automatisch erzeugter Legende anzeigen
- **Segmentleiste**: Unterer Selektor zum Filtern nach einem einzelnen Segment
- **Native Power-BI-Tooltips** mit konfigurierbarer Werteformatierung
- **Kreuzauswahl** kompatibel mit anderen Berichtvisuals
- **Hoher Kontrast** und vollständige Barrierefreiheit
- **Lokalisierung**: Spanisch, Englisch, Italienisch, Französisch und Deutsch

## Erforderliche Datenfelder

| Feld | Typ | Beschreibung |
|------|------|-------------|
| **Kategorie** | Kategorie | Radarachsen, z. B. Monate oder Produktkategorien |
| **Segment** (optional) | Kategorie | Zu vergleichende Reihen, z. B. Jahre oder Regionen |
| **Messwert** | Wert | Numerischer Wert für die Darstellung |
| **Bezeichnung** (optional) | Kategorie | Benutzerdefinierte Bezeichnung für Segmente |

## Formateinstellungen

### Karte „Radar“

- **Rasterebenen**: Anzahl der konzentrischen Ringe (1-10)
- **Rasterlinienbreite**: Stärke der Rasterlinien
- **Rasterfarbe/-transparenz**: Visuelle Anpassung
- **Füll-/Rahmenfarbe**: Standardfarben für den Einzelmodus
- **Wertebezeichnungen anzeigen**: Werte an den Eckpunkten ein- oder ausblenden
- **Segmentbezeichnung verwenden**: Beschreibenden Namen anstelle des technischen Schlüssels verwenden
- **Balkenposition**: Unten / Oben / Ausgeblendet

### Karte „Legende“

- **Legende anzeigen**: Ein/Aus
- **Position**: Oben / Unten / Links / Rechts

### Karte „Bezeichnungen“

- **Schriftgröße für Kategorie/Wert**: 8-24 px
- **Eckpunkt-Radius**: Größe der Punkte im Polygon
- **Werteformat**: Allgemein / Ganzzahl / 1 Dezimalstelle / 2 Dezimalstellen

## Auswahlverhalten

- **Klick auf die Segmentleiste**: Filtert das Diagramm nach dem Segment und überträgt die Auswahl auf andere Visuals
- **Klick auf das aktive Segment**: Löscht die Auswahl und kehrt zur vollständigen Ansicht zurück
- **Externes Kreuzfiltern**: Berücksichtigt Filter anderer Visuals, ohne die interne Auswahl dauerhaft zu speichern
- **Mehrere Instanzen**: Jedes Visual verwaltet seinen eigenen Auswahlstatus

## Installation

1. Laden Sie die `.pbiviz`-Datei herunter.
2. Wählen Sie in Power BI Desktop `Einfügen` → `Benutzerdefiniertes Visual` → `Aus Datei importieren`.
3. Wählen Sie die heruntergeladene `.pbiviz`-Datei aus.

## Versionsverlauf

### v1.0.0.18 (2026-08-13)

- **Korrektur der Lokalisierung von Dropdowns**: Die Werte für `Balkenposition`, `Legendenposition` und `Werteformat` werden jetzt über `localizationManager` korrekt übersetzt.
- **Robustheit**: `null as any` beim Rendern von Polygonen mit mehreren Segmenten entfernt.
- **Korrektur von dataReductionAlgorithm**: Die Zeilenbegrenzung `top`, die Segmentdaten in großen Datensätzen abschneiden konnte, wurde entfernt.
- **Highlight-Unterstützung**: `supportsHighlight` für Cross-Highlighting zwischen Messwerten aktiviert.

### v1.0.0.17 (2026-08-13)

- **Lokalisierungskorrektur**: Ressourcen nach `stringResources/<locale>/resources.resjson` verschoben und korrekt in die `.pbiviz`-Datei eingebunden.
- **Korrektur des Formatbereichs**: Karten und Eigenschaften verwenden `displayNameKey` für die native Übersetzung des Formatbereichs.
- **Übergabe von localizationManager** an `FormattingSettingsService`.

### v1.0.0.16 (2026-08-13)

- **Kritische Auswahlkorrektur**: Automatische Auswahl beim Empfang gefilterter Daten durch Kreuzfilterung entfernt.
- **Korrektur der Persistenz**: Die interne Auswahl wird nur noch durch Benutzerinteraktion per Klick geändert.
- **Korrektur der Segmentleiste**: Die Leiste ist nun auch bei einem einzelnen Segment zur visuellen Identifizierung sichtbar.
- **Korrektur der Darstellung**: Vollständige Ansicht (`renderAllSegments`), wenn keine interne Auswahl aktiv ist.
- **Aktualisierung der Metadaten**: Quell-URL auf OpenCode aktualisiert.

### v1.0.0.15

- Mehrsprachige Unterstützung (ES, EN, IT, FR, DE)
- Verbesserungen beim hohen Kontrast
- Optimierung der Tooltips

### v1.0.0.14

- Basisversion mit vollständiger Radar-Funktionalität für mehrere Segmente

## Lizenz

MIT-Lizenz – Einzelheiten finden Sie in der Datei [LICENSE](LICENSE).

## Autor

**Ramiro Mosquera**  
- GitHub: [@ramirito_fer](https://github.com/ramirito_fer)
- Support: [Instagram](https://www.instagram.com/ramirito_fer)

---

*Erstellt mit [OpenCode](https://opencode.ai)*