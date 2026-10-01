# Radar Multi - Power BI Custom Visual

*Leer este documento en [English](README.en.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | [Italiano](README.it.md)*

Visual personalizado de gráfico de radar (spider chart) con soporte para múltiples segmentos y medidas.

### Total de puntos por categoría

![Total de puntos por categoría](Radar/Total%20Points%20-%20Category.png)


### Total de puntos por categoría - Segmento seleccionado

![Total de puntos por categoría](Radar/Total%20Points%20-%20Selected.png)

## Características principales

- **Gráfico de radar interactivo** con ejes categóricos y niveles de grilla configurables
- **Soporte multi-segmento**: Permite comparar múltiples series (segmentos) en el mismo gráfico
- **Multi-medida**: Visualiza varias medidas simultáneamente con leyenda automática
- **Barra de segmentos**: Selector inferior para filtrar por segmento individual
- **Tooltips nativos** de Power BI con formato de valores configurable
- **Selección cruzada** (cross-filtering) compatible con otros visuales del informe
- **Alto contraste** y accesibilidad completa
- **Localización**: Español, Inglés, Italiano, Francés, Alemán

## Campos de datos requeridos

| Pozo | Tipo | Descripción |
|------|------|-------------|
| **Categoría** | Categoría | Ejes del radar (ej. Meses, Categorías de producto) |
| **Segmento** (opcional) | Categoría | Series a comparar (ej. Años, Regiones) |
| **Medida** | Valor | Valor numérico a graficar |
| **Etiqueta** (opcional) | Categoría | Etiqueta personalizada para segmentos |

## Configuración de formato

### Tarjeta Radar
- **Niveles de grilla**: Número de anillos concéntricos (1-20)
- **Ancho de trazo grilla**: Grosor de líneas de grilla (0.1-10)
- **Color/Opacidad grilla**: Personalización visual
- **Colorear por**: Segmento (defecto) o Medida; por medida los segmentos se distinguen por forma (círculo, cuadrado, triángulo, rombo)
- **Color de relleno/borde**: Colores por defecto para modo single
- **Auto-ajuste proporcional**: El centro y el radio se calculan según las etiquetas visibles para ocupar el área sin recortes
- **Mostrar etiquetas de valor**: Toggle valores en vértices
- **Usar etiqueta de segmento**: Usa nombre descriptivo vs clave técnica
- **Posición barra**: Bottom / Top / Left / Right / Hidden

### Tarjeta Leyenda
- **Mostrar leyenda**: On/Off
- **Posición**: Top / Bottom / Left / Right
- **Filtro por medida**: Click en la leyenda filtra el gráfico a esa medida (multi-medida; segundo click limpia)

### Tarjeta Etiquetas
- **Tamaño fuente categoría/valor**: 6-72px
- **Radio de vértice**: Tamaño puntos en polígono (0.5-30)
- **Formato valor**: General / Entero / 1 decimal / 2 decimales

## Comportamiento de selección

- **Click en barra de segmentos**: Filtra el gráfico a ese segmento y propaga selección a otros visuales
- **Click en segmento activo**: Limpia selección (vuelve a vista completa)
- **Cross-filtering externo**: Respeta filtros de otros visuales sin persistir selección interna
- **Múltiples instancias**: Cada visual mantiene su estado de selección independiente

## Instalación

1. Descargar el archivo `.pbiviz` desde [Releases](https://github.com/tu-usuario/radarMulti/releases)
2. En Power BI Desktop: `Insertar` → `Visual personalizado` → `Importar desde archivo`
3. Seleccionar el archivo `.pbiviz` descargado

## Localización

Los recursos de idioma viven en la carpeta `stringResources/<locale>/resources.resjson` y se referencian
en el array `stringResources` de `pbiviz.json`. Cada archivo es un mapa `{ clave: texto traducido }` en UTF-8.

```
stringResources/
  en-US/resources.resjson
  es-ES/resources.resjson
  it-IT/resources.resjson
  fr-FR/resources.resjson
  de-DE/resources.resjson
```

- Las tarjetas y propiedades del panel de formato se traducen con `displayNameKey` (`settings.ts` + `capabilities.json`).
- Los valores de los dropdowns (`Enum_*`) se resuelven con `localizationManager.getDisplayName()` en `visual.ts`.
- El inglés (`en-US`) es la base técnica; no debe cambiarse.

Para ver los cambios de idioma en Power BI: importa el `.pbiviz`, cambia el idioma de la app, reinicia
Power BI y reemplaza el visual en el lienzo.

## Desarrollo

```bash
# Instalar dependencias
npm install

# Desarrollo con live reload
npm start

# Compilar para producción
npm run package

# Linting
npm run lint
```

## Historial de versiones

### v1.0.0.26 (2026-09-30)
- **Barra solo con segmentos**: ya no combina segmento-medida; clic filtra el segmento en todas las medidas
- **Nuevo switch Colorear por**: Segmento (defecto, colores actuales) o Medida (mismo color por medida y forma distinta por segmento: círculo, cuadrado, triángulo, rombo)

### v1.0.0.25 (2026-09-30)
- **Fix leyenda multi-medida**: Show Legend muestra un registro único por Measure Data (antes uno por segmento × medida); clic en la medida filtra el gráfico a esa dimensión, segundo clic limpia el filtro

### v1.0.0.24 (2026-09-30)
- **Auto-ajuste proporcional**: eliminado el slider manual de zoom; el centro y el radio se calculan por vista (todos los segmentos o segmento seleccionado) maximizando el tamaño con las etiquetas siempre dentro del área, sin espacios en blanco innecesarios

### v1.0.0.23 (2026-09-30)
- **Nuevo control Zoom del radar**: slider en tarjeta Radar (20-400%, 180% por defecto) que escala el radio sobre el tamaño auto-ajustado; permite agrandar el gráfico cuando el ajuste automático lo deja pequeño

### v1.0.0.22 (2026-09-30)
- **Fix gráfico pequeño**: el padding ahora se calcula con medición real del texto (canvas `measureText`) en lugar de estimación por caracteres, y se redujeron los espacios fijos; con etiquetas cortas el radar vuelve a ocupar el área disponible

### v1.0.0.21 (2026-09-30)
- **Fix etiquetas largas**: las etiquetas de categoría se ajustan en hasta 3 líneas (word-wrap, sin cortar palabras) y el padding del gráfico se calcula dinámicamente según el texto, para que no se salgan del área del diagrama
- **Fix valores por defecto**: `localizeDropdownItems()` ahora también traduce el `value` actual de los dropdowns (`Formato de valor`, `Posición de barra`, `Posición de leyenda`); antes el panel no encontraba el valor seleccionado y mostraba el campo en blanco

### v1.0.0.20 (2026-09-26)
- **Fix cross-filtering a otros controles**: las identidades de selección del segmento ahora tienen alcance a la columna de segmento (sin medida). Antes eran por punto de dato con `withMeasure`, lo que solo filtraba otros radarMulti con la misma medida; ahora cualquier visual ligado a la columna de segmento se filtra al hacer clic en la barra
- **Localización**: tooltip de segmento y mensaje de estado vacío ("asociar campos") ahora se traducen vía `Tooltip_Segment` y `Msg_Bind_Fields`
- **Pulido FR/IT**: preposiciones en francés ("Données de catégorie", "Couleur de remplissage", …) y posiciones en italiano ("In basso", "A sinistra", …)
- **Deuda técnica**: API actualizada a 5.11.1 (`powerbi-visuals-api`, `formattingmodel` 7.1.0), ESLint 10

### v1.0.0.18 (2026-08-13)
- **Fix localización dropdowns**: Los valores de `Posición de barra`, `Posición de leyenda` y `Formato de valor` ahora se traducen correctamente (resolución de `Enum_*` vía `localizationManager`)
- **Robustez**: Eliminado `null as any` en render de polígonos multi-segmento
- **Fix dataReductionAlgorithm**: Eliminado el límite de filas `top` que podía cortar datos de segmentos en datasets grandes
- **Fix cross-filtering**: Restaurada la propagación de selección entre instancias de radarMulti. Se descartó `supportsHighlight` porque cambia la selección a cross-highlight (que el visual no renderiza), rompiendo el filtrado cruzado por segmento

### v1.0.0.17 (2026-08-13)
- **Fix localización**: Recursos movidos a `stringResources/<locale>/resources.resjson` y empaquetados correctamente en el `.pbiviz`
- **Fix panel de formato**: Tarjetas y propiedades usan `displayNameKey` para traducción nativa del panel
- **Passing localizationManager** al `FormattingSettingsService`

### v1.0.0.16 (2026-08-13)
- **Fix crítico selección**: Eliminada auto-selección al recibir datos filtrados (cross-filtering)
- **Fix persistencia**: La selección interna solo cambia por interacción del usuario (click)
- **Fix barra segmentos**: Ahora visible con 1 solo segmento para identificación visual
- **Fix renderizado**: Vista completa (`renderAllSegments`) cuando no hay selección interna
- **Actualización metadatos**: Source URL actualizada a OpenCode

### v1.0.0.15
- Soporte multi-idioma (ES, EN, IT, FR, DE)
- Mejoras en alto contraste
- Optimización de tooltips

### v1.0.0.14
- Versión base con funcionalidad completa radar multi-segmento

## Licencia

MIT License - Ver archivo [LICENSE](LICENSE) para detalles.

## Autor

**Ramiro Mosquera**  
- GitHub: [@ramirito_fer](https://github.com/ramirito_fer)  
- Soporte: [Instagram](https://www.instagram.com/ramirito_fer)

---

*Generado con [OpenCode](https://opencode.ai)*