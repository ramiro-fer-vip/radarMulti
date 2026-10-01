# Radar Multi - Power BI Custom Visual

*Dieses Dokument lesen auf [Español](README.md) | [English](README.en.md) | [Français](README.fr.md) | [Italiano](README.it.md)*

Benutzerdefiniertes Radar-Diagramm (Spider-Chart) mit Unterstützung für mehrere Segmente und Measures.

### Gesamtpunkte pro Kategorie

![Gesamtpunkte pro Kategorie](Radar/Total%20Points%20-%20Category.png)


### Gesamtpunkte pro Kategorie – Ausgewähltes Segment

![Gesamtpunkte pro Kategorie](Radar/Total%20Points%20-%20Selected.png)

## Hauptmerkmale

- **Interaktives Radar-Diagramm** mit kategorischen Achsen und konfigurierbaren Gitterebenen
- **Multi-Segment-Unterstützung**: Mehrere Reihen (Segmente) im selben Diagramm vergleichen
- **Multi-Measure**: Mehrere Measures gleichzeitig mit automatischer Legende anzeigen
- **Segmentleiste**: Unterer Selektor zum Filtern nach einzelnem Segment
- **Native Power BI-Tooltips** mit konfigurierbarer Wertformatierung
- **Kreuzfilterung** (Cross-Filtering) kompatibel mit anderen Visuals im Bericht
- **Hoher Kontrast** und vollständige Barrierefreiheit
- **Lokalisierung**: Spanisch, Englisch, Italienisch, Französisch, Deutsch

## Erforderliche Datenfelder

| Feld | Typ | Beschreibung |
|------|------|-------------|
| **Kategorie** | Kategorie | Radar-Achsen (z. B. Monate, Produktkategorien) |
| **Segment** (optional) | Kategorie | Zu vergleichende Reihen (z. B. Jahre, Regionen) |
| **Messwert** | Wert | Zu plottender Zahlenwert |
| **Bezeichnung** (optional) | Kategorie | Benutzerdefinierte Bezeichnung für Segmente |

## Formateinstellungen

### Radar-Karte
- **Gitterebenen**: Anzahl konzentrischer Ringe (1-20)
- **Gitterlinienbreite**: Linienstärke des Gitters (0.1-10)
- **Gitterfarbe/-deckkraft**: Visuelle Anpassung
- **Färben nach**: Segment (Standard) oder Messwert; nach Messwert werden Segmente durch Form unterschieden (Kreis, Quadrat, Dreieck, Raute)
- **Füll-/Randfarbe**: Standardfarben für den Einzelmodus
- **Proportionale Auto-Anpassung**: Mittelpunkt und Radius passen sich an die sichtbaren Beschriftungen an und füllen die Fläche ohne Abschneiden
- **Wertebeschriftungen anzeigen**: Werte an Eckpunkten ein-/ausblenden
- **Segmentbeschriftung verwenden**: Beschreibenden Namen vs. technischen Schlüssel verwenden
- **Leistenposition**: Unten / Oben / Links / Rechts / Ausgeblendet

### Legenden-Karte
- **Legende anzeigen**: Ein/Aus
- **Position**: Oben / Unten / Links / Rechts
- **Nach Measure filtern**: Klick auf die Legende filtert das Diagramm auf dieses Measure (Multi-Measure; zweiter Klick hebt auf)

### Beschriftungs-Karte
- **Kategorie-/Werteschriftgröße**: 6-72px
- **Eckenradius**: Punktgröße auf dem Polygon (0.5-30)
- **Wertformat**: Allgemein / Ganzzahl / 1 Dezimalstelle / 2 Dezimalstellen

## Auswahlverhalten

- **Klick auf Segmentleiste**: Filtert das Diagramm auf dieses Segment und überträgt die Auswahl auf andere Visuals
- **Klick auf aktives Segment**: Hebt die Auswahl auf (zurück zur Gesamtansicht)
- **Externe Kreuzfilterung**: Berücksichtigt Filter anderer Visuals, ohne interne Auswahl zu speichern
- **Mehrere Instanzen**: Jedes Visual behält seinen eigenen unabhängigen Auswahlstatus

## Installation

1. Die `.pbiviz`-Datei von [Releases](https://github.com/tu-usuario/radarMulti/releases) herunterladen
2. In Power BI Desktop: `Einfügen` → `Benutzerdefiniertes Visual` → `Aus Datei importieren`
3. Die heruntergeladene `.pbiviz`-Datei auswählen

## Lokalisierung

Sprachressourcen liegen im Ordner `stringResources/<locale>/resources.resjson` und werden
im `stringResources`-Array von `pbiviz.json` referenziert. Jede Datei ist eine `{ Schlüssel: übersetzter Text }`-Map in UTF-8.

```
stringResources/
  en-US/resources.resjson
  es-ES/resources.resjson
  it-IT/resources.resjson
  fr-FR/resources.resjson
  de-DE/resources.resjson
```

- Karten und Eigenschaften des Formatbereichs werden mit `displayNameKey` übersetzt (`settings.ts` + `capabilities.json`).
- Dropdown-Werte (`Enum_*`) werden mit `localizationManager.getDisplayName()` in `visual.ts` aufgelöst.
- Englisch (`en-US`) ist die technische Basis; es darf nicht geändert werden.

Um Sprachänderungen in Power BI zu sehen: `.pbiviz` importieren, App-Sprache ändern, Power BI neu starten
und das Visual auf der Zeichenfläche ersetzen.

## Entwicklung

```bash
# Abhängigkeiten installieren
npm install

# Entwicklung mit Live-Reload
npm start

# Für Produktion kompilieren
npm run package

# Linting
npm run lint
```

## Versionsverlauf

### v1.0.0.26 (2026-09-30)
- **Leiste nur mit Segmenten**: keine Segment-Measure-Kombination mehr; Klick filtert das Segment über alle Measures
- **Neue Steuerung Färben nach**: Segment (Standard, aktuelle Farben) oder Messwert (gleiche Farbe pro Messwert mit eigener Form pro Segment: Kreis, Quadrat, Dreieck, Raute)

### v1.0.0.25 (2026-09-30)
- **Fix Multi-Measure-Legende**: Legende anzeigen zeigt einen einzigen Eintrag pro Measure-Daten (zuvor einen pro Segment × Measure); Klick auf das Measure filtert das Diagramm auf diese Dimension, zweiter Klick hebt den Filter auf

### v1.0.0.24 (2026-09-30)
- **Proportionale Auto-Anpassung**: manueller Zoom-Regler entfernt; Mittelpunkt und Radius werden pro Ansicht (alle Segmente oder gewähltes Segment) berechnet und maximieren die Größe, Beschriftungen bleiben stets in der Fläche, ohne unnötigen Leerraum

### v1.0.0.23 (2026-09-30)
- **Neue Steuerung Radarzoom**: Regler auf der Radar-Karte (20-400 %, 180 % Standard), der den Radius über die automatisch angepasste Größe skaliert; vergrößert das Diagramm, wenn die Auto-Anpassung es zu klein lässt

### v1.0.0.22 (2026-09-30)
- **Fix kleines Diagramm**: Das Padding wird jetzt aus echter Textmessung (Canvas `measureText`) statt Zeichenschätzung berechnet, und feste Abstände wurden reduziert; bei kurzen Beschriftungen füllt das Radar wieder die verfügbare Fläche

### v1.0.0.21 (2026-09-30)
- **Fix lange Beschriftungen**: Kategoriebeschriftungen werden in bis zu 3 Zeilen umbrochen (Word-Wrap, ohne Worttrennung), und das Diagramm-Padding wird dynamisch aus dem Text berechnet, sodass Beschriftungen innerhalb der Diagrammfläche bleiben
- **Fix Standardwerte**: `localizeDropdownItems()` übersetzt jetzt auch den aktuellen `value` der Dropdowns (`Wertformat`, `Leistenposition`, `Legendenposition`); zuvor konnte der Bereich den gewählten Wert nicht zuordnen und zeigte das Feld leer an

### v1.0.0.20 (2026-09-26)
- **Fix Kreuzfilterung zu anderen Steuerelementen**: Segment-Auswahlidentitäten sind jetzt auf die Segmentspalte beschränkt (ohne Measure). Zuvor waren sie pro Datenpunkt mit `withMeasure`, wodurch nur andere radarMulti-Instanzen mit demselben Measure gefiltert wurden; jetzt wird jedes an die Segmentspalte gebundene Visual beim Klicken auf die Leiste gefiltert
- **Lokalisierung**: Segment-Tooltip und Leerzustandsmeldung („Felder zuordnen") werden jetzt via `Tooltip_Segment` und `Msg_Bind_Fields` übersetzt
- **FR/IT-Feinheiten**: Französische Präpositionen („Données de catégorie", „Couleur de remplissage", …) und italienische Positionen („In basso", „A sinistra", …)
- **Technik**: API auf 5.11.1 aktualisiert (`powerbi-visuals-api`, `formattingmodel` 7.1.0), ESLint 10

### v1.0.0.18 (2026-08-13)
- **Fix Dropdown-Lokalisierung**: Die Werte für `Leistenposition`, `Legendenposition` und `Wertformat` werden jetzt korrekt übersetzt (`Enum_*`-Auflösung via `localizationManager`)
- **Robustheit**: `null as any` beim Rendern von Multi-Segment-Polygonen entfernt
- **Fix dataReductionAlgorithm**: `top`-Zeilenlimit entfernt, das Segmentdaten in großen Datasets abschneiden konnte
- **Fix Cross-Filtering**: Auswahlübertragung zwischen radarMulti-Instanzen wiederhergestellt. `supportsHighlight` wurde verworfen, da es die Auswahl auf Cross-Highlight umstellt (das das Visual nicht rendert) und damit die Kreuzfilterung nach Segment brach

### v1.0.0.17 (2026-08-13)
- **Fix Lokalisierung**: Ressourcen nach `stringResources/<locale>/resources.resjson` verschoben und korrekt in die `.pbiviz` gepackt
- **Fix Formatbereich**: Karten und Eigenschaften nutzen `displayNameKey` für native Bereichsübersetzung
- **localizationManager** an den `FormattingSettingsService` übergeben

### v1.0.0.16 (2026-08-13)
- **Kritischer Auswahl-Fix**: Automatische Auswahl beim Empfang gefilterter Daten entfernt (Cross-Filtering)
- **Fix Persistenz**: Interne Auswahl ändert sich nur durch Benutzerinteraktion (Klick)
- **Fix Segmentleiste**: Jetzt auch bei nur einem Segment sichtbar zur visuellen Identifikation
- **Fix Rendering**: Gesamtansicht (`renderAllSegments`), wenn keine interne Auswahl besteht
- **Metadaten-Update**: Quell-URL auf OpenCode aktualisiert

### v1.0.0.15
- Mehrsprachigkeit (ES, EN, IT, FR, DE)
- Verbesserungen bei hohem Kontrast
- Tooltip-Optimierung

### v1.0.0.14
- Basisversion mit vollständiger Multi-Segment-Radar-Funktionalität

## Lizenz

MIT-Lizenz – Details siehe Datei [LICENSE](LICENSE).

## Autor

**Ramiro Mosquera**  
- GitHub: [@ramirito_fer](https://github.com/ramirito_fer)  
- Support: [Instagram](https://www.instagram.com/ramirito_fer)

---

*Erstellt mit [OpenCode](https://opencode.ai)*
