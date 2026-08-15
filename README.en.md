# Radar Multi - Power BI Custom Visual

Custom radar chart (spider chart) visual with support for multiple segments and measures.

### Total Points by Category

![Total Points by Category](Radar/Total%20Points%20-%20Category.png)

## Main Features

- **Interactive radar chart** with categorical axes and configurable grid levels
- **Multi-segment support**: Compare multiple series (segments) in the same chart
- **Multiple measures**: Display several measures simultaneously with an automatic legend
- **Segment bar**: Bottom selector to filter by individual segment
- **Native Power BI tooltips** with configurable value formatting
- **Cross-selection** compatible with other report visuals
- **High contrast** and full accessibility support
- **Localization**: Spanish, English, Italian, French, and German

## Required Data Fields

| Field | Type | Description |
|------|------|-------------|
| **Category** | Category | Radar axes, such as months or product categories |
| **Segment** (optional) | Category | Series to compare, such as years or regions |
| **Measure** | Value | Numeric value to plot |
| **Label** (optional) | Category | Custom label for segments |

## Format Configuration

### Radar Card

- **Grid levels**: Number of concentric rings (1-10)
- **Grid stroke width**: Thickness of grid lines
- **Grid color/opacity**: Visual customization
- **Fill/border color**: Default colors for single mode
- **Show value labels**: Toggle values at vertices
- **Use segment label**: Use a descriptive name instead of the technical key
- **Bar position**: Bottom / Top / Hidden

### Legend Card

- **Show legend**: On/Off
- **Position**: Top / Bottom / Left / Right

### Labels Card

- **Category/value font size**: 8-24px
- **Vertex radius**: Point size in the polygon
- **Value format**: General / Integer / 1 decimal / 2 decimals

## Selection Behavior

- **Click the segment bar**: Filters the chart to that segment and propagates the selection to other visuals
- **Click the active segment**: Clears the selection and returns to the complete view
- **External cross-filtering**: Respects filters from other visuals without persisting the internal selection
- **Multiple instances**: Each visual maintains its own selection state

## Installation

1. Download the `.pbiviz` file.
2. In Power BI Desktop, select `Insert` → `Custom visual` → `Import from file`.
3. Select the downloaded `.pbiviz` file.

## Version History

### v1.0.0.18 (2026-08-13)

- **Dropdown localization fix**: Values for `Bar position`, `Legend position`, and `Value format` are now translated correctly through `localizationManager`.
- **Robustness**: Removed `null as any` from multi-segment polygon rendering.
- **dataReductionAlgorithm fix**: Removed the `top` row limit that could truncate segment data in large datasets.
- **Highlight support**: Enabled `supportsHighlight` for cross-highlighting between measures.

### v1.0.0.17 (2026-08-13)

- **Localization fix**: Resources moved to `stringResources/<locale>/resources.resjson` and correctly packaged in the `.pbiviz` file.
- **Format pane fix**: Cards and properties use `displayNameKey` for native format pane translation.
- **Passing localizationManager** to `FormattingSettingsService`.

### v1.0.0.16 (2026-08-13)

- **Critical selection fix**: Removed automatic selection when receiving filtered data through cross-filtering.
- **Persistence fix**: Internal selection now changes only through user interaction by clicking.
- **Segment bar fix**: The bar is now visible with a single segment for visual identification.
- **Rendering fix**: Displays the complete view (`renderAllSegments`) when there is no internal selection.
- **Metadata update**: Source URL updated to OpenCode.

### v1.0.0.15

- Multi-language support (ES, EN, IT, FR, DE)
- High-contrast improvements
- Tooltip optimization

### v1.0.0.14

- Base version with complete multi-segment radar functionality

## License

MIT License - See the [LICENSE](LICENSE) file for details.

## Author

**Ramiro Mosquera**  
- GitHub: [@ramirito_fer](https://github.com/ramirito_fer)  
- Support: [Instagram](https://www.instagram.com/ramirito_fer)

---

*Generated with [OpenCode](https://opencode.ai)*