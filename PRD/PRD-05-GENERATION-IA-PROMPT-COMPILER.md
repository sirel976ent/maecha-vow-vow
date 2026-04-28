# PRD-05 - Generation IA et Prompt Compiler

## Objectif

Industrialiser la generation d'images sans perdre les contraintes de coherence visuelle, de securite editoriale et de tracabilite.

## Probleme

Aujourd'hui, les prompts sont distribues entre plusieurs fichiers et le processus de generation repose encore trop sur des manipulations manuelles.

## Utilisateurs cibles

- directeur artistique
- operateur IA
- editeur de contenu

## Perimetre

### In scope

- compileur de prompts
- injection automatique des blocs style
- injection automatique des prompts personnage verrouilles
- application d'un profil sensible
- lancement de jobs de generation
- stockage des variantes
- choix d'un asset actif
- historique des prompts/modeles

### Out of scope

- generation video
- retouche image avancee in-app
- moderation automatisee avancee

## Exigences fonctionnelles

- un panel peut etre genere depuis le studio
- le prompt final est compose automatiquement
- chaque generation garde une trace complete
- plusieurs variantes peuvent etre generees pour un meme panel
- l'utilisateur peut selectionner une version active
- une ancienne version n'est jamais ecrasee silencieusement

## Regles metier critiques

- les `PROMPT DE BASE` personnages sont verrouilles
- le bloc style obligatoire est toujours injecte
- les regles sensibles de la serie sont appliquees a chaque generation
- la selection d'un nouvel asset doit conserver l'historique

## Livrables

- package `prompt-compiler`
- service de generation IA
- file de jobs
- table `AssetVersion`
- table `GenerationJob`
- UI de comparaison de variantes

## Criteres d'acceptation

- un panel peut lancer une generation depuis le studio
- le prompt compile est consultable
- plusieurs variantes sont stockees et comparables
- un asset actif peut etre choisi sans perte d'historique
- les metadonnees de generation sont persistantes

## Dependances

- PRD-01
- PRD-03
- PRD-04

## Risques

- sur-couplage au provider initial
- trous de tracabilite sur les prompts
- absence de garde-fous sur les contenus sensibles

## Decision de cadrage

Le compileur de prompts est un composant de domaine, pas une logique enterree dans une page UI.
