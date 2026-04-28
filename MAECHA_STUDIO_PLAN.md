# Maecha Studio - Plan d'architecture

## Objectif

Transformer le workflow actuel de production webtoon en un studio modulaire qui permet :

- de creer une nouvelle BD depuis un template
- de gerer plusieurs series sans recoder le HTML a la main
- de generer et versionner les planches IA
- d'editer les textes et les bulles dans un backoffice
- de publier ensuite en HTML statique vers le site public

## Constat sur l'existant

Le repo actuel est une sortie de production statique :

- les series sont organisees par dossiers auto-contenus
- les prompts sont disperses entre `STYLE_GUIDE.md`, `CHARACTER_SHEETS/` et `SCRIPTS/`
- le rendu final vit dans des fichiers HTML standalone
- le placement des bulles est manuel et code dans le HTML
- les images sont publiees telles quelles

Ce fonctionnement marche pour un MVP, mais il ne scale pas bien pour :

- multiplier les series
- regenerer des planches rapidement
- reutiliser des templates de personnages et de styles
- deleguer le travail editorial sans toucher au code

## Principe directeur

Ne pas transformer ce repo public en application.

Ce repo doit rester la cible de publication statique.

Le futur `maecha-studio` doit devenir la source de verite privee pour :

- l'authoring
- la generation IA
- la previsualisation
- la publication

## Architecture cible

### Separation des roles

- `maecha-studio` : produit prive d'edition
- `maecha-vow-vow` : sortie publique generee

### Blocs techniques

- `apps/studio-web`
  Backoffice web pour creer les BD, episodes, planches et overlays.
- `apps/api`
  API metier pour CRUD, workflows editoriaux et publication.
- `apps/worker`
  Jobs asynchrones pour generation IA, rendu HTML, export et publication.
- `packages/domain`
  Types partages, regles metier, compileur de prompts, guardrails.
- `packages/renderers`
  Renderer webtoon HTML, puis plus tard renderer video.

### Infrastructure

- `PostgreSQL`
  Source de verite du contenu structure.
- `S3/R2/MinIO`
  Stockage des images, variantes, thumbnails et exports.
- `Redis`
  File de jobs.
- `OpenRouter`
  Appels vers les modeles image via un service dedie.

## Workflow cible

1. Creer une serie depuis un template
2. Definir ou cloner le style guide
3. Definir les character sheets verrouillees
4. Creer les episodes
5. Creer les scenes et planches
6. Compiler le prompt
7. Generer plusieurs variantes d'image
8. Choisir une version active
9. Positionner les bulles dans l'editeur visuel
10. Verifier le preview mobile
11. Publier vers le site public

## Invariants a conserver

Les regles actuelles doivent rester vraies dans le studio :

- une serie reste auto-contenue au niveau editorial
- les blocs `PROMPT DE BASE` personnage sont verrouilles
- le bloc style obligatoire est injecte dans chaque prompt
- les regles de contenu sensible sont appliquees systematiquement
- une image n'est jamais ecrasee sans archive/version
- le rendu public final reste un HTML statique simple a servir

## Modele metier

### Objets principaux

#### `SeriesTemplate`

Modele reutilisable pour lancer une nouvelle BD.

Contient :

- structure par defaut
- sections obligatoires
- type de rendu
- styles initiaux
- schemas d'episodes

#### `Series`

Une BD concrete.

Contient :

- titre
- slug
- langue
- statut
- description
- regles de publication

#### `StyleGuide`

Equivalent structure du `STYLE_GUIDE.md`.

Contient :

- bloc style obligatoire
- palette
- references visuelles
- ancrage local
- contraintes de cadrage

#### `SafetyProfile`

Regles editoriales sensibles.

Contient :

- contenu interdit
- techniques autorisees
- niveau de gravite
- messages de prevention obligatoires

#### `CharacterSheet`

Equivalent structure des `CHARACTER_SHEETS`.

Contient :

- identite
- traits permanents verrouilles
- prompt de base verrouille
- tenues
- expressions
- poses
- contextes visuels lies

#### `Episode`

Un episode d'une serie.

Contient :

- numero
- titre
- resume
- arc emotionnel
- statut
- ordre de publication

#### `Scene`

Unite narrative intermediaire entre episode et planche.

Contient :

- intention narrative
- personnages presents
- ambiance
- decor
- contraintes de mise en scene

Cette couche prepare aussi l'avenir video.

#### `Panel`

Une planche ou image finale.

Contient :

- code panel `1_07`
- brief
- type de panel
- image active
- overlays
- statut editorial

#### `Overlay`

Texte et habillage positionnes par-dessus l'image.

Types :

- `bubble`
- `thought`
- `narrator`
- `sfx`
- `notification`
- `transition`
- `resources_box`

Contient :

- texte
- style
- coordonnees
- largeur max
- ordre d'affichage

#### `AssetVersion`

Version d'un asset genere ou importe.

Contient :

- type d'asset
- provider
- modele
- prompt exact
- prompt compile
- seed si disponible
- chemin stockage
- checksum
- metadonnees
- date

#### `GenerationJob`

Trace des generations.

Contient :

- cible
- mode
- etat
- parametres
- logs
- erreurs

#### `Publication`

Snapshot publie.

Contient :

- version de contenu
- assets references
- destination
- date
- statut

## Prompt Compiler

Le coeur du studio est un compileur de prompts.

Il doit assembler automatiquement :

- le bloc style de la serie
- les prompts de base verrouilles des personnages presents
- les expressions/poses choisies
- le brief de scene
- les contraintes sensibles
- le format de sortie

Sortie attendue :

- prompt final
- prompt systeme de garde-fous
- metadonnees de generation

## API MVP

### Series

- `POST /series`
- `GET /series`
- `GET /series/:id`
- `PATCH /series/:id`
- `POST /series/:id/from-template`

### Characters

- `POST /series/:id/characters`
- `GET /series/:id/characters`
- `PATCH /characters/:id`

### Episodes

- `POST /series/:id/episodes`
- `GET /series/:id/episodes`
- `PATCH /episodes/:id`

### Scenes

- `POST /episodes/:id/scenes`
- `PATCH /scenes/:id`

### Panels

- `POST /scenes/:id/panels`
- `GET /panels/:id`
- `PATCH /panels/:id`
- `PATCH /panels/:id/overlays`

### Generation

- `POST /panels/:id/generate`
- `POST /panels/:id/regenerate`
- `POST /panels/:id/select-asset/:assetVersionId`
- `GET /jobs/:id`

### Preview / Publish

- `POST /episodes/:id/render-preview`
- `POST /publications`
- `GET /publications/:id`

## Ecrans du backoffice

### Priorite 1

- dashboard des series
- creation d'une serie
- fiche serie
- gestion des personnages
- liste des episodes
- editeur de planche

### Priorite 2

- comparateur de variantes IA
- preview mobile de l'episode
- file de jobs
- historique des publications

### Editeur de planche

L'editeur de planche doit permettre :

- afficher l'image active
- ajouter une bulle
- deplacer une bulle en drag and drop
- modifier le texte sans toucher au HTML
- changer le type d'overlay
- previsualiser le rendu final mobile

## Publication

Le studio ne doit pas servir directement le public au debut.

Il doit produire une sortie statique :

- HTML d'episodes
- index de serie
- images publiees

Deux options de publication :

1. exporter vers un dossier de sortie surveille
2. pousser une sortie generee dans le repo public

Pour commencer, l'option la plus simple est :

- `maecha-studio` prive
- publication automatique vers `maecha-vow-vow`

## Video plus tard

Le modele doit etre pense pour aller vers la video, sans l'implementer tout de suite.

Pour cela :

- `Scene` doit etre l'objet narratif principal
- une `Scene` peut produire un `Panel` aujourd'hui
- la meme `Scene` pourra produire un `Shot` video plus tard

## Roadmap recommande

### Phase 1 - Fondations

- creer le schema BDD
- creer les types de domaine
- creer le renderer HTML a partir de donnees structurees
- migrer une serie existante

### Phase 2 - Studio editorial

- creer le backoffice serie/episode/panel
- creer l'editeur visuel d'overlays
- ajouter preview mobile

### Phase 3 - IA et publication

- ajouter le prompt compiler
- ajouter generation et variantes
- ajouter publication automatique

### Phase 4 - Template factory

- bouton `Creer une BD`
- clonage de templates
- duplication de styles et personnages
- initialisation d'une structure complete

### Phase 5 - Extension media

- preparation des scenes pour video
- renderer shot/video

## MVP recommande

Le MVP a construire maintenant doit faire seulement :

- creer une serie
- creer un episode
- creer des panels
- associer une image a chaque panel
- editer les bulles visuellement
- generer un HTML final
- publier la sortie statique

Ce MVP suffit deja a supprimer la maintenance manuelle du HTML.

## Decision produit

Le produit a construire n'est pas seulement un CMS.

C'est un studio narratif qui combine :

- contenu structure
- templates editoriaux
- generation IA controlee
- edition visuelle
- publication statique

## Prochaine etape

Si cette direction est validee, la prochaine etape est de produire :

1. le schema BDD concret
2. l'arborescence exacte du repo `maecha-studio`
3. le plan de migration depuis les fichiers actuels

## Decoupage PRD

Le plan d'execution detaille existe maintenant dans :

- `PRD/README.md`
- `PRD/PRD-01-FONDATIONS-STUDIO.md`
- `PRD/PRD-02-CONTENU-STRUCTURE-RENDERER.md`
- `PRD/PRD-03-BACKOFFICE-EDITORIAL-CORE.md`
- `PRD/PRD-04-EDITEUR-VISUEL-PLANCHES.md`
- `PRD/PRD-05-GENERATION-IA-PROMPT-COMPILER.md`
- `PRD/PRD-06-PUBLICATION-WORKFLOW-VERSIONING.md`
- `PRD/PRD-07-TEMPLATE-FACTORY-NOUVELLE-BD.md`
