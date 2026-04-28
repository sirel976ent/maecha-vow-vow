# PRD-01 - Fondations Studio

## Objectif

Construire la base privee du futur `maecha-studio`, avec une architecture claire, une BDD propre et des primitives metier stables.

## Probleme

Aujourd'hui, le workflow repose sur un dossier de livrables publics. Il n'existe pas de source de verite privee pour :

- structurer le contenu
- versionner le travail editorial
- isoler les brouillons du public
- preparer un backoffice et des workers

## Utilisateurs cibles

- administrateur du studio
- editeur de contenu
- operateur de publication

## Perimetre

### In scope

- creation du repo `maecha-studio`
- choix de la stack technique
- structure monorepo apps/packages
- BDD PostgreSQL et migrations initiales
- auth minimale pour proteger le studio
- API de base pour `Series`, `Episode`, `Scene`, `Panel`
- abstraction de stockage assets
- configuration dev locale

### Out of scope

- rendu HTML final complet
- editeur visuel
- generation IA
- publication vers le site public

## Exigences fonctionnelles

- un utilisateur authentifie peut creer une serie
- un utilisateur authentifie peut lister les series
- un utilisateur authentifie peut creer un episode rattache a une serie
- un utilisateur authentifie peut creer une scene et un panel
- les entites ont des statuts de base

## Exigences non fonctionnelles

- le studio ne doit pas exposer de brouillons publiquement
- le schema de donnees doit permettre l'ajout futur d'assets, overlays, jobs et publications
- les noms et types doivent rester coherents avec le domaine actuel webtoon
- la stack doit permettre d'ajouter un worker asynchrone sans refonte

## Livrables

- repo `maecha-studio`
- `apps/studio-web`
- `apps/api`
- `apps/worker`
- `packages/domain`
- `packages/renderers`
- schema BDD initial
- migrations initiales
- auth minimale
- `.env.example`
- documentation de demarrage

## Entites minimales

- `User`
- `Series`
- `StyleGuide`
- `SafetyProfile`
- `CharacterSheet`
- `Episode`
- `Scene`
- `Panel`

## Criteres d'acceptation

- le repo demarre localement avec des commandes documentees
- la BDD peut etre creee depuis les migrations
- l'API expose des endpoints CRUD minimaux pour `Series`, `Episode`, `Scene`, `Panel`
- les routes du studio sont protegees par auth
- une serie test peut etre creee sans toucher a la BDD a la main

## Dependances

Aucune. C'est le point d'entree du projet.

## Risques

- sur-ingenierie trop tot
- schema trop rigide avant d'avoir teste le renderer
- auth trop lourde pour un outil encore mono-equipe

## Decision de cadrage

L'objectif n'est pas de finaliser le produit ici, mais de poser un socle qui ne devra pas etre refait au PRD-03.
