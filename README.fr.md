# Radar Multi - Visuel personnalisé Power BI

Visuel personnalisé de graphique radar (diagramme en toile d’araignée) prenant en charge plusieurs segments et mesures.

### Total des points par catégorie

![Total des points par catégorie](Radar/Total%20Points%20-%20Category.png)

## Fonctionnalités principales

- **Graphique radar interactif** avec axes catégoriels et niveaux de grille configurables
- **Prise en charge de plusieurs segments** : comparaison de plusieurs séries dans le même graphique
- **Plusieurs mesures** : affichage simultané de plusieurs mesures avec légende automatique
- **Barre des segments** : sélecteur inférieur pour filtrer un segment individuel
- **Info-bulles natives Power BI** avec formatage configurable des valeurs
- **Sélection croisée** compatible avec les autres visuels du rapport
- **Contraste élevé** et accessibilité complète
- **Localisation** : espagnol, anglais, italien, français et allemand

## Champs de données requis

| Champ | Type | Description |
|------|------|-------------|
| **Catégorie** | Catégorie | Axes du radar, par exemple les mois ou les catégories de produits |
| **Segment** (facultatif) | Catégorie | Séries à comparer, par exemple les années ou les régions |
| **Mesure** | Valeur | Valeur numérique à représenter |
| **Étiquette** (facultatif) | Catégorie | Étiquette personnalisée pour les segments |

## Configuration du format

### Carte Radar

- **Niveaux de grille** : nombre d’anneaux concentriques (1-10)
- **Épaisseur des lignes de grille** : épaisseur des lignes de grille
- **Couleur/opacité de la grille** : personnalisation visuelle
- **Couleur de remplissage/bordure** : couleurs par défaut en mode simple
- **Afficher les étiquettes de valeur** : affiche ou masque les valeurs aux sommets
- **Utiliser l’étiquette du segment** : utilise un nom descriptif au lieu de la clé technique
- **Position de la barre** : Bas / Haut / Masquée

### Carte Légende

- **Afficher la légende** : Activé/Désactivé
- **Position** : Haut / Bas / Gauche / Droite

### Carte Étiquettes

- **Taille de police catégorie/valeur** : 8-24 px
- **Rayon du sommet** : taille des points du polygone
- **Format de valeur** : Général / Entier / 1 décimale / 2 décimales

## Comportement de la sélection

- **Clic sur la barre des segments** : filtre le graphique sur le segment sélectionné et propage la sélection aux autres visuels
- **Clic sur le segment actif** : efface la sélection et revient à la vue complète
- **Filtrage croisé externe** : respecte les filtres des autres visuels sans conserver la sélection interne
- **Instances multiples** : chaque visuel conserve son propre état de sélection

## Installation

1. Téléchargez le fichier `.pbiviz`.
2. Dans Power BI Desktop, sélectionnez `Insérer` → `Visuel personnalisé` → `Importer à partir d’un fichier`.
3. Sélectionnez le fichier `.pbiviz` téléchargé.

## Historique des versions

### v1.0.0.18 (2026-08-13)

- **Correction de la localisation des listes déroulantes** : les valeurs de `Position de la barre`, `Position de la légende` et `Format de valeur` sont maintenant correctement traduites via `localizationManager`.
- **Robustesse** : suppression de `null as any` lors du rendu des polygones multi-segments.
- **Correction de dataReductionAlgorithm** : suppression de la limite de lignes `top` qui pouvait tronquer les données de segments dans les grands jeux de données.
- **Prise en charge du surlignage** : activation de `supportsHighlight` pour le surlignage croisé entre les mesures.

### v1.0.0.17 (2026-08-13)

- **Correction de la localisation** : ressources déplacées vers `stringResources/<locale>/resources.resjson` et correctement incluses dans le fichier `.pbiviz`.
- **Correction du volet de format** : les cartes et propriétés utilisent `displayNameKey` pour la traduction native du volet de format.
- **Transmission de localizationManager** à `FormattingSettingsService`.

### v1.0.0.16 (2026-08-13)

- **Correction critique de la sélection** : suppression de la sélection automatique lors de la réception de données filtrées par filtrage croisé.
- **Correction de la persistance** : la sélection interne ne change désormais qu’à la suite d’une interaction de l’utilisateur.
- **Correction de la barre des segments** : elle est maintenant visible même avec un seul segment pour faciliter l’identification visuelle.
- **Correction du rendu** : affichage de la vue complète (`renderAllSegments`) lorsqu’aucune sélection interne n’est active.
- **Mise à jour des métadonnées** : URL source mise à jour vers OpenCode.

### v1.0.0.15

- Prise en charge multilingue (ES, EN, IT, FR, DE)
- Améliorations du contraste élevé
- Optimisation des info-bulles

### v1.0.0.14

- Version de base avec toutes les fonctionnalités du radar multi-segments

## Licence

Licence MIT - Consultez le fichier [LICENSE](LICENSE) pour plus de détails.

## Auteur

**Ramiro Mosquera**  
- GitHub : [@ramirito_fer](https://github.com/ramirito_fer)
- Assistance : [Instagram](https://www.instagram.com/ramirito_fer)

---

*Généré avec [OpenCode](https://opencode.ai)*