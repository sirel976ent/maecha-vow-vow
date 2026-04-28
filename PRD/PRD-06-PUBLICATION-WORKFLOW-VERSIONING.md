# PRD-06 - Publication, Workflow et Versioning

## Objectif

Mettre sous controle le passage du brouillon prive vers la sortie publique, avec historique et statuts explicites.

## Probleme

Le site public sert des fichiers poses directement dans le dossier. Sans workflow de publication, il est facile d'exposer un mauvais asset ou une mauvaise version.

## Utilisateurs cibles

- operateur de publication
- administrateur

## Perimetre

### In scope

- statuts editoriaux
- snapshot de publication
- publication d'episode ou de serie
- export vers le dossier ou repo public
- historique des publications
- rollback simple vers une version precedente
- archivage des assets remplaces

### Out of scope

- moderation externe
- validation multi-equipe complexe
- publication multi-tenant

## Workflow cible

- `draft`
- `review`
- `approved`
- `published`
- `archived`

## Exigences fonctionnelles

- un contenu non approuve ne peut pas etre publie par erreur
- une publication cree un snapshot de contenu et d'assets
- le systeme garde un historique consultable
- un asset remplace reste accessible dans l'historique
- une version publiee precedente peut etre re-selectionnee rapidement

## Livrables

- tables `Publication` et historiques associes
- service d'export statique
- ecran de publication
- journal des publications
- mecanisme d'archivage versionne des assets

## Criteres d'acceptation

- un episode approuve peut etre publie depuis le studio
- la sortie generee est exploitable par le site public actuel
- une publication cree une trace complete
- un rollback simple est possible
- l'archivage des assets remplaces est automatique

## Dependances

- PRD-02
- PRD-03
- PRD-05

## Risques

- publication partielle incoherente
- confusion entre version courante et version publiee
- absence de rollback fiable

## Decision de cadrage

Le studio publie vers la cible statique. Il ne remplace pas le mode de diffusion public au debut.
