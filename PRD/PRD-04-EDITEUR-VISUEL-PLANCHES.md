# PRD-04 - Editeur Visuel des Planches

## Objectif

Permettre l'edition visuelle des textes et overlays directement sur l'image de la planche.

## Probleme

Le point le plus fragile du workflow actuel est le placement manuel des bulles dans le HTML. Cela ralentit chaque correction.

## Utilisateurs cibles

- editeur de contenu
- directeur artistique

## Perimetre

### In scope

- canvas de planche
- affichage de l'image active
- ajout d'overlays
- drag and drop
- redimensionnement simple
- edition du texte
- changement de type d'overlay
- preview mobile
- sauvegarde des coordonnees

### Out of scope

- generation IA
- publication
- edition collaborative temps reel

## Exigences fonctionnelles

- l'utilisateur peut ajouter une bulle sur une planche
- l'utilisateur peut deplacer une bulle
- l'utilisateur peut modifier le texte et le style associe
- l'utilisateur peut afficher ou masquer certains overlays
- l'utilisateur peut previsualiser le rendu mobile final
- les coordonnees sont persistantes

## Types a supporter en priorite

- `bubble`
- `thought`
- `narrator`
- `sfx`
- `notification`
- `transition`

## Livrables

- editeur de panel
- panneau de proprietes overlay
- preview mobile
- sauvegarde des positions

## Criteres d'acceptation

- l'utilisateur peut refaire l'equivalent d'une planche actuelle sans toucher au HTML
- le renderer final reutilise exactement les donnees editees dans l'UI
- la preview mobile est suffisamment fidele pour validation
- les overlays ne disparaissent pas lors d'un refresh

## Dependances

- PRD-02
- PRD-03

## Risques

- editeur trop ambitieux
- ecart entre preview et rendu final

## Decision de cadrage

L'objectif n'est pas un Figma complet. Il faut un outil pragmatique optimise pour les besoins webtoon.
