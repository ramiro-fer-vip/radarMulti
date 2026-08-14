# Radar Multi - Power BI Custom Visual

Visual personalizado de gráfico de radar (spider chart) con soporte para múltiples segmentos y medidas.

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
- **Niveles de grilla**: Número de anillos concéntricos (1-10)
- **Ancho de trazo grilla**: Grosor de líneas de grilla
- **Color/Opacidad grilla**: Personalización visual
- **Color de relleno/borde**: Colores por defecto para modo single
- **Mostrar etiquetas de valor**: Toggle valores en vértices
- **Usar etiqueta de segmento**: Usa nombre descriptivo vs clave técnica
- **Posición barra**: Bottom / Top / Hidden

### Tarjeta Leyenda
- **Mostrar leyenda**: On/Off
- **Posición**: Top / Bottom / Left / Right

### Tarjeta Etiquetas
- **Tamaño fuente categoría/valor**: 8-24px
- **Radio de vértice**: Tamaño puntos en polígono
- **Formato valor**: General / Entero / 1 decimal / 2 decimales

## Comportamiento de selección

- **Click en barra de segmentos**: Filtra el gráfico a ese segmento y propaga selección a otros visuales
- **Click en segmento activo**: Limpia selección (vuelve a vista completa)
- **Cross-filtering externo**: Respeta filtros de otros visuales sin persistir selección interna
- **Múltiples instancias**: Cada visual mantiene su estado de selección independiente

## Instalación

1. Descargar el archivo `.pbiviz` 
2. En Power BI Desktop: `Insertar` → `Visual personalizado` → `Importar desde archivo`
3. Seleccionar el archivo `.pbiviz` descargado

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
