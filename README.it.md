# Radar Multi - Power BI Custom Visual

*Leggi questo documento in [Español](README.md) | [English](README.en.md) | [Deutsch](README.de.md) | [Français](README.fr.md)*

Oggetto visivo personalizzato di grafico radar (spider chart) con supporto per più segmenti e misure.

### Punti totali per categoria

![Punti totali per categoria](Radar/Total%20Points%20-%20Category.png)


### Punti totali per categoria – Segmento selezionato

![Punti totali per categoria](Radar/Total%20Points%20-%20Selected.png)

## Funzionalità principali

- **Grafico radar interattivo** con assi categorici e livelli di griglia configurabili
- **Supporto multi-segmento**: confronta più serie (segmenti) nello stesso grafico
- **Multi-misura**: visualizza più misure contemporaneamente con legenda automatica
- **Barra dei segmenti**: selettore inferiore per filtrare per singolo segmento
- **Tooltip nativi** di Power BI con formato valori configurabile
- **Filtro incrociato** (cross-filtering) compatibile con gli altri oggetti visivi del report
- **Contrasto elevato** e accessibilità completa
- **Localizzazione**: Spagnolo, Inglese, Italiano, Francese, Tedesco

## Campi dati richiesti

| Campo | Tipo | Descrizione |
|------|------|-------------|
| **Categoria** | Categoria | Assi del radar (es. Mesi, Categorie di prodotto) |
| **Segmento** (facoltativo) | Categoria | Serie da confrontare (es. Anni, Regioni) |
| **Misura** | Valore | Valore numerico da tracciare |
| **Etichetta** (facoltativo) | Categoria | Etichetta personalizzata per i segmenti |

## Impostazioni di formato

### Scheda Radar
- **Livelli griglia**: numero di anelli concentrici (1-20)
- **Larghezza linea griglia**: spessore delle linee di griglia (0.1-10)
- **Colore/opacità griglia**: personalizzazione visiva
- **Colore riempimento/bordo**: colori predefiniti per la modalità singola
- **Mostra etichette valore**: mostra/nascondi i valori sui vertici
- **Usa etichetta segmento**: usa il nome descrittivo invece della chiave tecnica
- **Posizione barra**: In basso / In alto / A sinistra / A destra / Nascosto

### Scheda Legenda
- **Mostra legenda**: Sì/No
- **Posizione**: In alto / In basso / A sinistra / A destra

### Scheda Etichette
- **Dimensione carattere categoria/valore**: 6-72px
- **Raggio vertice**: dimensione dei punti sul poligono (0.5-30)
- **Formato valore**: Generale / Intero / 1 decimale / 2 decimali

## Comportamento di selezione

- **Clic sulla barra dei segmenti**: filtra il grafico su quel segmento e propaga la selezione agli altri oggetti visivi
- **Clic sul segmento attivo**: cancella la selezione (torna alla vista completa)
- **Filtro incrociato esterno**: rispetta i filtri degli altri oggetti visivi senza mantenere la selezione interna
- **Istanze multiple**: ogni oggetto visivo mantiene il proprio stato di selezione indipendente

## Installazione

1. Scarica il file `.pbiviz` da [Releases](https://github.com/tu-usuario/radarMulti/releases)
2. In Power BI Desktop: `Inserisci` → `Oggetto visivo personalizzato` → `Importa da file`
3. Seleziona il file `.pbiviz` scaricato

## Localizzazione

Le risorse di lingua si trovano nella cartella `stringResources/<locale>/resources.resjson` e sono referenziate
nell'array `stringResources` di `pbiviz.json`. Ogni file è una mappa `{ chiave: testo tradotto }` in UTF-8.

```
stringResources/
  en-US/resources.resjson
  es-ES/resources.resjson
  it-IT/resources.resjson
  fr-FR/resources.resjson
  de-DE/resources.resjson
```

- Le schede e le proprietà del riquadro di formato sono tradotte con `displayNameKey` (`settings.ts` + `capabilities.json`).
- I valori dei menu a discesa (`Enum_*`) sono risolti con `localizationManager.getDisplayName()` in `visual.ts`.
- L'inglese (`en-US`) è la base tecnica; non deve essere modificato.

Per vedere i cambi di lingua in Power BI: importa il `.pbiviz`, cambia la lingua dell'app, riavvia
Power BI e sostituisci l'oggetto visivo nell'area di disegno.

## Sviluppo

```bash
# Installa le dipendenze
npm install

# Sviluppo con ricaricamento live
npm start

# Compila per la produzione
npm run package

# Linting
npm run lint
```

## Cronologia delle versioni

### v1.0.0.20 (2026-09-26)
- **Fix filtro incrociato verso altri controlli**: le identità di selezione del segmento ora sono limitate alla colonna di segmento (senza misura). Prima erano per punto dati con `withMeasure`, il che filtrava solo le altre istanze radarMulti con la stessa misura; ora qualsiasi oggetto visivo legato alla colonna di segmento viene filtrato al clic sulla barra
- **Localizzazione**: il tooltip del segmento e il messaggio di stato vuoto («associa i campi») ora sono tradotti via `Tooltip_Segment` e `Msg_Bind_Fields`
- **Rifiniture FR/IT**: preposizioni francesi («Données de catégorie», «Couleur de remplissage», …) e posizioni italiane («In basso», «A sinistra», …)
- **Tecnica**: API aggiornata a 5.11.1 (`powerbi-visuals-api`, `formattingmodel` 7.1.0), ESLint 10

### v1.0.0.18 (2026-08-13)
- **Fix localizzazione menu a discesa**: i valori di `Posizione barra`, `Posizione legenda` e `Formato valore` ora sono tradotti correttamente (risoluzione `Enum_*` via `localizationManager`)
- **Robustezza**: rimosso `null as any` nel rendering dei poligoni multi-segmento
- **Fix dataReductionAlgorithm**: rimosso il limite di righe `top` che poteva troncare i dati dei segmenti nei dataset grandi
- **Fix filtro incrociato**: ripristinata la propagazione della selezione tra istanze radarMulti. `supportsHighlight` è stato scartato perché commuta la selezione in evidenziazione incrociata (che l'oggetto visivo non renderizza), rompendo il filtro incrociato per segmento

### v1.0.0.17 (2026-08-13)
- **Fix localizzazione**: risorse spostate in `stringResources/<locale>/resources.resjson` e impacchettate correttamente nel `.pbiviz`
- **Fix riquadro di formato**: schede e proprietà usano `displayNameKey` per la traduzione nativa del riquadro
- **Passaggio di localizationManager** al `FormattingSettingsService`

### v1.0.0.16 (2026-08-13)
- **Fix critico di selezione**: rimossa l'auto-selezione alla ricezione di dati filtrati (filtro incrociato)
- **Fix persistenza**: la selezione interna cambia solo per interazione dell'utente (clic)
- **Fix barra dei segmenti**: ora visibile anche con un solo segmento per l'identificazione visiva
- **Fix rendering**: vista completa (`renderAllSegments`) quando non c'è selezione interna
- **Aggiornamento metadati**: URL sorgente aggiornato a OpenCode

### v1.0.0.15
- Supporto multilingua (ES, EN, IT, FR, DE)
- Miglioramenti del contrasto elevato
- Ottimizzazione dei tooltip

### v1.0.0.14
- Versione base con funzionalità radar multi-segmento completa

## Licenza

Licenza MIT – Vedi il file [LICENSE](LICENSE) per i dettagli.

## Autore

**Ramiro Mosquera**  
- GitHub: [@ramirito_fer](https://github.com/ramirito_fer)  
- Supporto: [Instagram](https://www.instagram.com/ramirito_fer)

---

*Generato con [OpenCode](https://opencode.ai)*
