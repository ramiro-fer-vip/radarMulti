# Radar Multi - Power BI Custom Visual

*Lire ce document en [Español](README.md) | [English](README.en.md) | [Deutsch](README.de.md) | [Italiano](README.it.md)*

Visuel personnalisé de graphique radar (spider chart) prenant en charge plusieurs segments et mesures.

### Total des points par catégorie

![Total des points par catégorie](Radar/Total%20Points%20-%20Category.png)


### Total des points par catégorie – Segment sélectionné

![Total des points par catégorie](Radar/Total%20Points%20-%20Selected.png)

## Fonctionnalités principales

- **Graphique radar interactif** avec axes catégoriels et niveaux de grille configurables
- **Prise en charge multi-segment** : comparer plusieurs séries (segments) dans le même graphique
- **Multi-mesure** : afficher plusieurs mesures simultanément avec légende automatique
- **Barre de segments** : sélecteur inférieur pour filtrer par segment individuel
- **Info-bulles natives** de Power BI avec format de valeurs configurable
- **Filtrage croisé** (cross-filtering) compatible avec les autres visuels du rapport
- **Contraste élevé** et accessibilité complète
- **Localisation** : Espagnol, Anglais, Italien, Français, Allemand

## Champs de données requis

| Champ | Type | Description |
|------|------|-------------|
| **Catégorie** | Catégorie | Axes du radar (ex. Mois, Catégories de produits) |
| **Segment** (facultatif) | Catégorie | Séries à comparer (ex. Années, Régions) |
| **Mesure** | Valeur | Valeur numérique à tracer |
| **Étiquette** (facultatif) | Catégorie | Étiquette personnalisée pour les segments |

## Paramètres de format

### Carte Radar
- **Niveaux de grille** : nombre d'anneaux concentriques (1-20)
- **Largeur de ligne de grille** : épaisseur des lignes de grille (0.1-10)
- **Couleur/opacité de grille** : personnalisation visuelle
- **Colorer par** : Segment (défaut) ou Mesure ; par mesure, les segments se distinguent par la forme (cercle, carré, triangle, losange)
- **Couleur de remplissage/contour** : couleurs par défaut pour le mode unique
- **Ajustement proportionnel auto** : le centre et le rayon s'adaptent aux étiquettes visibles pour remplir la zone sans rognage
- **Afficher les étiquettes de valeur** : afficher/masquer les valeurs aux sommets
- **Utiliser l'étiquette de segment** : utilise le nom descriptif plutôt que la clé technique
- **Position de barre** : Bas / Haut / Gauche / Droite / Masqué

### Carte Légende
- **Afficher la légende** : Oui/Non
- **Position** : Haut / Bas / Gauche / Droite
- **Filtrer par mesure** : un clic sur la légende filtre le graphique sur cette mesure (multi-mesure ; second clic efface)

### Carte Étiquettes
- **Taille de police catégorie/valeur** : 6-72px
- **Rayon de sommet** : taille des points sur le polygone (0.5-30)
- **Format de valeur** : Général / Entier / 1 décimale / 2 décimales

## Comportement de sélection

- **Clic sur la barre de segments** : filtre le graphique sur ce segment et propage la sélection aux autres visuels
- **Clic sur le segment actif** : efface la sélection (retour à la vue complète)
- **Filtrage croisé externe** : respecte les filtres des autres visuels sans conserver de sélection interne
- **Instances multiples** : chaque visuel conserve son propre état de sélection indépendant

## Installation

1. Télécharger le fichier `.pbiviz` depuis [Releases](https://github.com/tu-usuario/radarMulti/releases)
2. Dans Power BI Desktop : `Insérer` → `Visuel personnalisé` → `Importer depuis un fichier`
3. Sélectionner le fichier `.pbiviz` téléchargé

## Localisation

Les ressources de langue se trouvent dans le dossier `stringResources/<locale>/resources.resjson` et sont référencées
dans le tableau `stringResources` de `pbiviz.json`. Chaque fichier est une table `{ clé : texte traduit }` en UTF-8.

```
stringResources/
  en-US/resources.resjson
  es-ES/resources.resjson
  it-IT/resources.resjson
  fr-FR/resources.resjson
  de-DE/resources.resjson
```

- Les cartes et propriétés du volet de format sont traduites avec `displayNameKey` (`settings.ts` + `capabilities.json`).
- Les valeurs des listes déroulantes (`Enum_*`) sont résolues avec `localizationManager.getDisplayName()` dans `visual.ts`.
- L'anglais (`en-US`) est la base technique ; il ne doit pas être modifié.

Pour voir les changements de langue dans Power BI : importez le `.pbiviz`, changez la langue de l'application, redémarrez
Power BI et remplacez le visuel sur le canevas.

## Développement

```bash
# Installer les dépendances
npm install

# Développement avec rechargement en direct
npm start

# Compiler pour la production
npm run package

# Linting
npm run lint
```

## Historique des versions

### v1.0.0.26 (2026-09-30)
- **Barre segments uniquement** : plus de combinaison segment-mesure ; le clic filtre le segment sur toutes les mesures
- **Nouveau réglage Colorer par** : Segment (défaut, couleurs actuelles) ou Mesure (même couleur par mesure avec forme distincte par segment : cercle, carré, triangle, losange)

### v1.0.0.25 (2026-09-30)
- **Correctif légende multi-mesure** : Afficher la légende montre une seule entrée par données de mesure (auparavant une par segment × mesure) ; un clic sur la mesure filtre le graphique sur cette dimension, second clic efface le filtre

### v1.0.0.24 (2026-09-30)
- **Ajustement proportionnel auto** : curseur de zoom manuel supprimé ; le centre et le rayon sont calculés par vue (tous les segments ou segment sélectionné) en maximisant la taille avec les étiquettes toujours dans la zone, sans espace blanc inutile

### v1.0.0.23 (2026-09-30)
- **Nouveau contrôle Zoom du radar** : curseur sur la carte Radar (20-400 %, 180 % par défaut) qui met le rayon à l'échelle de la taille auto-ajustée ; permet d'agrandir le graphique quand l'ajustement automatique le laisse petit

### v1.0.0.22 (2026-09-30)
- **Correctif graphique petit** : la marge est désormais calculée d'après la mesure réelle du texte (canvas `measureText`) au lieu d'une estimation par caractère, et les espaces fixes ont été réduits ; avec des étiquettes courtes le radar remplit de nouveau la zone disponible

### v1.0.0.21 (2026-09-30)
- **Correctif étiquettes longues** : les étiquettes de catégorie passent sur jusqu'à 3 lignes (retour à la ligne sans couper les mots) et la marge du graphique est calculée dynamiquement d'après le texte, pour qu'elles restent dans la zone du diagramme
- **Correctif valeurs par défaut** : `localizeDropdownItems()` traduit désormais aussi le `value` actuel des listes (`Format de valeur`, `Position de barre`, `Position de légende`) ; le volet ne trouvait pas la valeur sélectionnée et affichait le champ vide

### v1.0.0.20 (2026-09-26)
- **Correctif filtrage croisé vers d'autres contrôles** : les identités de sélection du segment sont désormais limitées à la colonne de segment (sans mesure). Auparavant elles étaient par point de données avec `withMeasure`, ce qui ne filtrait que les autres instances radarMulti partageant la même mesure ; désormais tout visuel lié à la colonne de segment est filtré au clic sur la barre
- **Localisation** : l'info-bulle de segment et le message d'état vide (« associer les champs ») sont désormais traduits via `Tooltip_Segment` et `Msg_Bind_Fields`
- **Finitions FR/IT** : prépositions françaises (« Données de catégorie », « Couleur de remplissage », …) et positions italiennes (« In basso », « A sinistra », …)
- **Technique** : API mise à jour vers 5.11.1 (`powerbi-visuals-api`, `formattingmodel` 7.1.0), ESLint 10

### v1.0.0.18 (2026-08-13)
- **Correctif localisation des listes** : les valeurs de `Position de barre`, `Position de légende` et `Format de valeur` se traduisent désormais correctement (résolution `Enum_*` via `localizationManager`)
- **Robustesse** : suppression de `null as any` dans le rendu des polygones multi-segments
- **Correctif dataReductionAlgorithm** : suppression de la limite de lignes `top` qui pouvait tronquer les données de segments dans les grands jeux de données
- **Correctif filtrage croisé** : propagation de la sélection entre instances radarMulti restaurée. `supportsHighlight` a été écarté car il bascule la sélection en surbrillance croisée (que le visuel ne rend pas), rompant le filtrage croisé par segment

### v1.0.0.17 (2026-08-13)
- **Correctif localisation** : ressources déplacées vers `stringResources/<locale>/resources.resjson` et correctement empaquetées dans le `.pbiviz`
- **Correctif volet de format** : les cartes et propriétés utilisent `displayNameKey` pour la traduction native du volet
- **Passage de localizationManager** au `FormattingSettingsService`

### v1.0.0.16 (2026-08-13)
- **Correctif critique de sélection** : suppression de l'auto-sélection à la réception de données filtrées (filtrage croisé)
- **Correctif persistance** : la sélection interne ne change que par interaction utilisateur (clic)
- **Correctif barre de segments** : désormais visible même avec un seul segment pour l'identification visuelle
- **Correctif rendu** : vue complète (`renderAllSegments`) quand il n'y a pas de sélection interne
- **Mise à jour métadonnées** : URL source mise à jour vers OpenCode

### v1.0.0.15
- Prise en charge multilingue (ES, EN, IT, FR, DE)
- Améliorations du contraste élevé
- Optimisation des info-bulles

### v1.0.0.14
- Version de base avec fonctionnalité radar multi-segment complète

## Licence

Licence MIT – Voir le fichier [LICENSE](LICENSE) pour plus de détails.

## Auteur

**Ramiro Mosquera**  
- GitHub : [@ramirito_fer](https://github.com/ramirito_fer)  
- Support : [Instagram](https://www.instagram.com/ramirito_fer)

---

*Généré avec [OpenCode](https://opencode.ai)*
