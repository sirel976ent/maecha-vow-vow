# PRD-02 - Contenu Structure et Renderer Statique

## Objectif

Remplacer l'edition manuelle du HTML par un rendu statique genere depuis des donnees structurees.

## Probleme

Le contenu final vit actuellement dans les fichiers HTML. Cela rend difficile :

- la maintenance des textes
- la reutilisation des structures
- la publication fiable
- la preparation d'un vrai backoffice

## Utilisateurs cibles

- editeur de contenu
- operateur de publication

## Perimetre

### In scope

- modele structure pour episodes, scenes, panels et overlays
- renderer HTML webtoon vertical
- templates HTML/CSS de sortie
- moteur de preview episode
- export statique local d'une serie ou d'un episode

### Out of scope

- editeur visuel riche
- generation IA
- workflow editorial complet

## Exigences fonctionnelles

- un episode peut etre rendu en HTML statique depuis la BDD
- les overlays sont definis comme donnees, pas comme HTML ecrit a la main
- le rendu conserve les conventions visuelles du format actuel
- les chemins d'images suivent une convention stable
- le systeme peut produire un dossier de sortie pret a etre servi

## Types d'overlay a supporter

- `bubble`
- `thought`
- `narrator`
- `sfx`
- `notification`
- `transition`
- `resources_box`

## Livrables

- schema de donnees pour overlays
- renderer HTML episode
- template CSS de sortie
- preview d'episode
- export statique sur disque
- documentation des conventions de rendu

## Criteres d'acceptation

- un episode seed peut etre rendu sans edition manuelle du HTML
- le HTML genere reste lisible et simple a servir par nginx
- les textes et positions viennent des donnees stockees
- le rendu mobile max-width est conserve
- les episodes peuvent etre exportes en dossier statique

## Dependances

- PRD-01

## Risques

- vouloir generaliser trop tot le renderer
- coupler le renderer a l'UI au lieu d'en faire un module autonome

## Decision de cadrage

Le renderer doit devenir un package autonome. Le backoffice ne doit pas reimplementer le rendu.
