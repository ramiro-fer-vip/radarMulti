# Radar Multi - Visual personalizzato Power BI

Visual personalizzato di grafico radar (spider chart) con supporto per più segmenti e misure.

### Totale dei punti per categoria

![Totale dei punti per categoria](Radar/Total%20Points%20-%20Category.png)

## Funzionalità principali

- **Grafico radar interattivo** con assi categoriali e livelli della griglia configurabili
- **Supporto multi-segmento**: consente di confrontare più serie nello stesso grafico
- **Più misure**: visualizza più misure contemporaneamente con legenda automatica
- **Barra dei segmenti**: selettore inferiore per filtrare un singolo segmento
- **Tooltip nativi di Power BI** con formattazione dei valori configurabile
- **Selezione incrociata** compatibile con gli altri oggetti visivi del report
- **Alto contrasto** e accessibilità completa
- **Localizzazione**: spagnolo, inglese, italiano, francese e tedesco

## Campi dati richiesti

| Campo | Tipo | Descrizione |
|------|------|-------------|
| **Categoria** | Categoria | Assi del radar, ad esempio mesi o categorie di prodotto |
| **Segmento** (facoltativo) | Categoria | Serie da confrontare, ad esempio anni o regioni |
| **Misura** | Valore | Valore numerico da rappresentare |
| **Etichetta** (facoltativa) | Categoria | Etichetta personalizzata per i segmenti |

## Configurazione del formato

### Scheda Radar

- **Livelli della griglia**: numero di anelli concentrici (1-10)
- **Spessore delle linee della griglia**: spessore delle linee della griglia
- **Colore/opacità della griglia**: personalizzazione visiva
- **Colore di riempimento/bordo**: colori predefiniti per la modalità singola
- **Mostra etichette dei valori**: mostra o nasconde i valori nei vertici
- **Usa etichetta del segmento**: utilizza un nome descrittivo invece della chiave tecnica
- **Posizione della barra**: In basso / In alto / Nascosta

### Scheda Legenda

- **Mostra legenda**: Attivata/Disattivata
- **Posizione**: In alto / In basso / A sinistra / A destra

### Scheda Etichette

- **Dimensione carattere categoria/valore**: 8-24 px
- **Raggio del vertice**: dimensione dei punti del poligono
- **Formato del valore**: Generale / Intero / 1 decimale / 2 decimali

## Comportamento della selezione

- **Clic sulla barra dei segmenti**: filtra il grafico sul segmento selezionato e propaga la selezione agli altri oggetti visivi
- **Clic sul segmento attivo**: cancella la selezione e torna alla visualizzazione completa
- **Cross-filtering esterno**: rispetta i filtri degli altri oggetti visivi senza mantenere la selezione interna
- **Più istanze**: ogni visual mantiene il proprio stato di selezione

## Installazione

1. Scaricare il file `.pbiviz`.
2. In Power BI Desktop, selezionare `Inserisci` → `Visual personalizzato` → `Importa da file`.
3. Selezionare il file `.pbiviz` scaricato.

## Cronologia delle versioni

### v1.0.0.18 (2026-08-13)

- **Correzione della localizzazione dei menu a discesa**: i valori di `Posizione della barra`, `Posizione della legenda` e `Formato del valore` vengono ora tradotti correttamente tramite `localizationManager`.
- **Robustezza**: rimosso `null as any` dal rendering dei poligoni multi-segmento.
- **Correzione di dataReductionAlgorithm**: rimosso il limite di righe `top` che poteva troncare i dati dei segmenti nei dataset di grandi dimensioni.
- **Supporto all’evidenziazione**: abilitato `supportsHighlight` per il cross-highlighting tra le misure.

### v1.0.0.17 (2026-08-13)

- **Correzione della localizzazione**: risorse spostate in `stringResources/<locale>/resources.resjson` e incluse correttamente nel file `.pbiviz`.
- **Correzione del riquadro del formato**: schede e proprietà utilizzano `displayNameKey` per la traduzione nativa del riquadro del formato.
- **Passaggio di localizationManager** a `FormattingSettingsService`.

### v1.0.0.16 (2026-08-13)

- **Correzione critica della selezione**: rimossa la selezione automatica alla ricezione di dati filtrati tramite cross-filtering.
- **Correzione della persistenza**: la selezione interna cambia solo in seguito all’interazione dell’utente tramite clic.
- **Correzione della barra dei segmenti**: ora è visibile anche con un solo segmento per facilitarne l’identificazione visiva.
- **Correzione del rendering**: mostra la visualizzazione completa (`renderAllSegments`) quando non è presente una selezione interna.
- **Aggiornamento dei metadati**: URL della fonte aggiornata a OpenCode.

### v1.0.0.15

- Supporto multilingue (ES, EN, IT, FR, DE)
- Miglioramenti dell’alto contrasto
- Ottimizzazione dei tooltip

### v1.0.0.14

- Versione di base con funzionalità completa del radar multi-segmento

## Licenza

Licenza MIT - Consultare il file [LICENSE](LICENSE) per i dettagli.

## Autore

**Ramiro Mosquera**  
- GitHub: [@ramirito_fer](https://github.com/ramirito_fer)
- Supporto: [Instagram](https://www.instagram.com/ramirito_fer)

---

*Generato con [OpenCode](https://opencode.ai)*