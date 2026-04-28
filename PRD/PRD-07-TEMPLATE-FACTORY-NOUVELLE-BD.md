# PRD-07 - Template Factory et Creation Rapide de BD

## Objectif

Permettre de creer une nouvelle BD en quelques clics a partir de templates editoriaux et visuels reutilisables.

## Probleme

Sans mecanisme de template, chaque nouvelle BD demandera encore une reconfiguration manuelle des styles, personnages, episodes et conventions.

## Utilisateurs cibles

- administrateur
- editeur principal

## Perimetre

### In scope

- `SeriesTemplate`
- clonage de style guide
- clonage de safety profile
- packs de personnages
- structure d'episodes predefinie
- wizard `Creer une BD`

### Out of scope

- marketplace publique de templates
- video factory
- generation automatique complete d'une BD sans validation humaine

## Exigences fonctionnelles

- l'utilisateur peut choisir un template de base
- l'utilisateur peut creer une nouvelle serie a partir de ce template
- le studio pre-remplit style, regles, personnages et structure
- l'utilisateur peut ensuite adapter les elements necessaires
- le systeme evite les duplications incoherentes

## Livrables

- entite `SeriesTemplate`
- UI de creation guidee
- clonage des ressources de base
- documentation de creation de template

## Criteres d'acceptation

- une nouvelle serie peut etre initialisee en moins de 5 minutes
- les prompts verrouilles clones restent proteges
- les episodes et personnages de base sont bien rattaches a la nouvelle serie
- la serie creee est directement exploitable dans le backoffice

## Dependances

- PRD-01
- PRD-03
- PRD-05
- PRD-06

## Risques

- templates trop rigides
- duplication de donnees difficile a maintenir

## Decision de cadrage

Ce PRD est celui qui realise la promesse produit : `cliquer sur creer une BD`, puis partir d'une base coherente au lieu de repartir de zero.
