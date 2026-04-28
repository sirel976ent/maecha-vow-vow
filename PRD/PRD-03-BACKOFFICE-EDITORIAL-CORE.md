# PRD-03 - Backoffice Editorial Core

## Objectif

Permettre a un utilisateur non developpeur de gerer le contenu principal du studio depuis une interface web.

## Probleme

Tant que la creation et la maintenance des series passent par les fichiers, chaque mise a jour reste une operation technique.

## Utilisateurs cibles

- administrateur
- editeur de contenu

## Perimetre

### In scope

- dashboard des series
- creation et edition d'une serie
- creation et edition d'un style guide
- creation et edition de character sheets
- creation et edition d'episodes
- creation et edition de scenes et panels
- navigation simple entre ces entites

### Out of scope

- drag and drop des overlays
- generation IA
- publication finale automatisee

## Exigences fonctionnelles

- l'utilisateur peut creer une nouvelle serie depuis l'UI
- l'utilisateur peut definir le style obligatoire de la serie
- l'utilisateur peut definir les personnages et leurs prompts verrouilles
- l'utilisateur peut creer les episodes et leur ordre
- l'utilisateur peut creer les scenes puis les panels
- l'utilisateur peut modifier les metadonnees sans toucher au code

## Exigences UX

- navigation claire par serie
- formulaires simples et rapides a remplir
- distinction nette entre champs verrouilles et champs editables
- etats visibles `draft`, `review`, `approved`

## Livrables

- dashboard
- pages serie
- pages personnage
- pages episode
- pages scene
- pages panel
- formulaires CRUD

## Criteres d'acceptation

- une nouvelle serie peut etre creee en entier depuis l'interface
- les prompts verrouilles sont visibles mais proteges
- les episodes et panels peuvent etre reordonnes simplement
- un utilisateur non technique peut preparer la structure complete d'une BD

## Dependances

- PRD-01
- PRD-02

## Risques

- forms trop complexes trop tot
- confusion entre edition de contenu et edition de rendu

## Decision de cadrage

Le backoffice core gere le fond editorial. Le placement visuel des bulles arrive au PRD-04.
