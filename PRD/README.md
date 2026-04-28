# Maecha Studio - Decoupage PRD

## But

Ce dossier decoupe le projet `maecha-studio` en PRD successifs pour avancer etape par etape, sans melanger :

- la vision produit
- les fondations techniques
- l'edition editoriale
- la generation IA
- la publication

Le document de reference haut niveau reste :

- `../MAECHA_STUDIO_PLAN.md`

Ce dossier sert a transformer cette vision en lots executables.

## Ordre recommande

### PRD-01 - Fondations Studio

Objectif :
poser la base technique et le modele de donnees du studio prive.

Sortie attendue :
un repo `maecha-studio` demarrable, avec apps, packages, BDD, auth minimale et API de base.

### PRD-02 - Contenu Structure et Renderer Statique

Objectif :
sortir le contenu du HTML manuel et produire le HTML final a partir de donnees structurees.

Sortie attendue :
un renderer capable de generer un episode webtoon statique sans edition manuelle du HTML.

### PRD-03 - Backoffice Editorial Core

Objectif :
creer l'interface pour gerer series, personnages, episodes, scenes et panels.

Sortie attendue :
un utilisateur non developpeur peut creer et modifier une BD sans toucher au code.

### PRD-04 - Editeur Visuel des Planches

Objectif :
ajouter l'edition visuelle des bulles, overlays et previews mobile.

Sortie attendue :
les textes et leurs positions sont geres depuis l'UI, pas depuis le HTML.

### PRD-05 - Generation IA et Prompt Compiler

Objectif :
industrialiser la generation d'images en respectant les prompts verrouilles, les styles et les garde-fous.

Sortie attendue :
generation de variantes, selection d'une version active et traque complete des prompts/modeles.

### PRD-06 - Publication, Workflow et Versioning

Objectif :
mettre sous controle la validation et la publication vers le site public.

Sortie attendue :
un workflow `draft -> review -> approved -> published` avec snapshots et historique.

### PRD-07 - Template Factory et Creation Rapide de BD

Objectif :
permettre de lancer une nouvelle BD depuis un template en quelques clics.

Sortie attendue :
creation rapide d'une nouvelle serie avec structure, styles, personnages et episodes preconfigures.

## Regle d'execution

Le projet doit avancer PRD par PRD.

Chaque PRD doit avoir :

- un objectif clair
- un perimetre ferme
- des livrables concrets
- des criteres d'acceptation
- des dependances explicites

## Definition of Done globale

Un PRD est considere termine si :

- le perimetre en scope est livre
- les criteres d'acceptation sont verifies
- la documentation d'usage minimale existe
- le PRD suivant n'a pas besoin de reouvrir les choix fondamentaux du PRD precedent

## Backlog hors sequence initiale

Ces sujets existent mais ne doivent pas casser la priorite des PRD 01 a 07 :

- support video
- roles avances et permissions fines
- analytics d'usage
- multi-langue public
- publication multi-canal
