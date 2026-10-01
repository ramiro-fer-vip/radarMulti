# Radar Multi - Power BI Custom Visual

*Read this document in [Español](README.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | [Italiano](README.it.md)*

Custom radar chart (spider chart) visual with support for multiple segments and measures.

### Total points by category

![Total points by category](Radar/Total%20Points%20-%20Category.png)


### Total points by category - Selected segment

![Total points by category](Radar/Total%20Points%20-%20Selected.png)

## Key features

- **Interactive radar chart** with categorical axes and configurable grid levels
- **Multi-segment support**: Compare multiple series (segments) in the same chart
- **Multi-measure**: Display several measures simultaneously with automatic legend
- **Segment bar**: Bottom selector to filter by individual segment
- **Native Power BI tooltips** with configurable value formatting
- **Cross-filtering** compatible with other visuals in the report
- **High contrast** and full accessibility
- **Localization**: Spanish, English, Italian, French, German

## Required data fields

| Field | Type | Description |
|------|------|-------------|
| **Category** | Category | Radar axes (e.g. Months, Product categories) |
| **Segment** (optional) | Category | Series to compare (e.g. Years, Regions) |
| **Measure** | Value | Numeric value to plot |
| **Label** (optional) | Category | Custom label for segments |

## Format settings

### Radar card
- **Grid levels**: Number of concentric rings (1-20)
- **Grid stroke width**: Grid line thickness (0.1-10)
- **Grid color/opacity**: Visual customization
- **Color by**: Segment (default) or Measure; by measure, segments are distinguished by shape (circle, square, triangle, diamond)
- **Fill/border color**: Default colors for single mode
- **Proportional auto-fit**: Center and radius adapt to visible labels to fill the area without clipping
- **Show value labels**: Toggle values on vertices
- **Use segment label**: Uses descriptive name vs technical key
- **Bar position**: Bottom / Top / Left / Right / Hidden

### Legend card
- **Show legend**: On/Off
- **Position**: Top / Bottom / Left / Right
- **Filter by measure**: Clicking the legend filters the chart to that measure (multi-measure; second click clears)

### Labels card
- **Category/value font size**: 6-72px
- **Vertex radius**: Point size on polygon (0.5-30)
- **Value format**: General / Integer / 1 decimal / 2 decimals

## Selection behavior

- **Click on segment bar**: Filters the chart to that segment and propagates selection to other visuals
- **Click on active segment**: Clears selection (back to full view)
- **External cross-filtering**: Respects filters from other visuals without persisting internal selection
- **Multiple instances**: Each visual keeps its own independent selection state

## Installation

1. Download the `.pbiviz` file from [Releases](https://github.com/tu-usuario/radarMulti/releases)
2. In Power BI Desktop: `Insert` → `Custom visual` → `Import from file`
3. Select the downloaded `.pbiviz` file

## Localization

Language resources live in the `stringResources/<locale>/resources.resjson` folder and are referenced
in the `stringResources` array of `pbiviz.json`. Each file is a `{ key: translated text }` map in UTF-8.

```
stringResources/
  en-US/resources.resjson
  es-ES/resources.resjson
  it-IT/resources.resjson
  fr-FR/resources.resjson
  de-DE/resources.resjson
```

- Format pane cards and properties are translated with `displayNameKey` (`settings.ts` + `capabilities.json`).
- Dropdown values (`Enum_*`) are resolved with `localizationManager.getDisplayName()` in `visual.ts`.
- English (`en-US`) is the technical base; it must not be changed.

To see language changes in Power BI: import the `.pbiviz`, change the app language, restart
Power BI and replace the visual on the canvas.

## Development

```bash
# Install dependencies
npm install

# Development with live reload
npm start

# Build for production
npm run package

# Linting
npm run lint
```

## Version history

### v1.0.0.26 (2026-09-30)
- **Segments-only bar**: no longer combines segment-measure; clicking filters the segment across all measures
- **New Color by switch**: Segment (default, current colors) or Measure (same color per measure with distinct shape per segment: circle, square, triangle, diamond)

### v1.0.0.25 (2026-09-30)
- **Fix multi-measure legend**: Show Legend shows a single entry per Measure Data (previously one per segment × measure); clicking the measure filters the chart to that dimension, second click clears the filter

### v1.0.0.24 (2026-09-30)
- **Proportional auto-fit**: manual zoom slider removed; center and radius are computed per view (all segments or selected segment) maximizing size with labels always inside the area, no unnecessary whitespace

### v1.0.0.23 (2026-09-30)
- **New Radar zoom control**: slider on the Radar card (20-400%, 180% by default) scaling the radius over the auto-fitted size; lets you enlarge the chart when auto-fit leaves it small

### v1.0.0.22 (2026-09-30)
- **Fix small chart**: padding is now computed from real text measurement (canvas `measureText`) instead of per-character estimation, and fixed gaps were reduced; with short labels the radar fills the available area again

### v1.0.0.21 (2026-09-30)
- **Fix long labels**: category labels wrap into up to 3 lines (word-wrap, never splitting words) and the chart padding is computed dynamically from the text, so labels stay inside the diagram area
- **Fix default values**: `localizeDropdownItems()` now also translates the current `value` of dropdowns (`Value format`, `Bar position`, `Legend position`); the pane previously could not match the selected value and showed the field blank

### v1.0.0.20 (2026-09-26)
- **Fix cross-filtering to other controls**: segment selection identities are now scoped to the segment column (no measure). They used to be per data point with `withMeasure`, which only filtered other radarMulti instances sharing the same measure; now any visual bound to the segment column is filtered when clicking the bar
- **Localization**: segment tooltip and empty-state message ("bind fields") are now translated via `Tooltip_Segment` and `Msg_Bind_Fields`
- **FR/IT polish**: French prepositions ("Données de catégorie", "Couleur de remplissage", …) and Italian positions ("In basso", "A sinistra", …)
- **Tech debt**: API updated to 5.11.1 (`powerbi-visuals-api`, `formattingmodel` 7.1.0), ESLint 10

### v1.0.0.18 (2026-08-13)
- **Fix dropdown localization**: `Bar position`, `Legend position` and `Value format` values now translate correctly (`Enum_*` resolution via `localizationManager`)
- **Robustness**: Removed `null as any` in multi-segment polygon rendering
- **Fix dataReductionAlgorithm**: Removed the `top` row limit that could cut segment data in large datasets
- **Fix cross-filtering**: Restored selection propagation between radarMulti instances. `supportsHighlight` was discarded because it switches selection to cross-highlight (which the visual does not render), breaking cross-filtering by segment

### v1.0.0.17 (2026-08-13)
- **Fix localization**: Resources moved to `stringResources/<locale>/resources.resjson` and correctly packaged into the `.pbiviz`
- **Fix format pane**: Cards and properties use `displayNameKey` for native pane translation
- **Passing localizationManager** to the `FormattingSettingsService`

### v1.0.0.16 (2026-08-13)
- **Critical selection fix**: Removed auto-selection when receiving filtered data (cross-filtering)
- **Fix persistence**: Internal selection only changes on user interaction (click)
- **Fix segment bar**: Now visible with a single segment for visual identification
- **Fix rendering**: Full view (`renderAllSegments`) when there is no internal selection
- **Metadata update**: Source URL updated to OpenCode

### v1.0.0.15
- Multi-language support (ES, EN, IT, FR, DE)
- High contrast improvements
- Tooltip optimization

### v1.0.0.14
- Base version with full multi-segment radar functionality

## License

MIT License - See [LICENSE](LICENSE) file for details.

## Author

**Ramiro Mosquera**  
- GitHub: [@ramirito_fer](https://github.com/ramirito_fer)  
- Support: [Instagram](https://www.instagram.com/ramirito_fer)

---

*Generated with [OpenCode](https://opencode.ai)*
