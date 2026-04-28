# AGENTS.md

This file provides guidance to Codex (Codex.ai/code) when working with code in this repository.

> Le AGENTS.md parent (`/home/sirel/docker/openclaw-raya/AGENTS.md`) decrit RAYA, ses skills et ses regles generales. Lis-le en premier. Ce fichier-ci couvre uniquement ce qui est **specifique au dossier Maecha_VowVow**.

## Ce que ce dossier est

Ce n'est pas un codebase applicatif — c'est un **dossier de livrables** (images PNG + HTML statiques) pour trois series webtoon de prevention PSP Mayotte. Pas de build, pas de tests, pas de package manager. Le "deploiement" consiste juste a deposer les fichiers ici.

**Exposition publique immediate** : ce dossier est servi tel quel par nginx sur `https://maecha.sirel976.com` (conteneur `maecha-webtoon`, image `nginx:alpine` avec bind-mount read-only). Tout fichier depose est visible en ligne apres quelques secondes (cache HTML no-cache, images 5 min). Il est aussi accessible en lecture/ecriture via FileBrowser sur `https://studio.sirel976.com`.

## Les trois series (hierarchie)

```
Maecha_VowVow/                      ← racine = serie "Maecha VowVow" (complete, COMPLET)
├── index.html                      ← landing global : liste les 3 series
├── HTML/index.html + episode_1-5.html
├── IMAGES/EP1..EP5/                ← 57 planches
├── CHARACTER_SHEETS/ SCRIPTS/ REFERENCES/ TEMPLATES/ STYLE_GUIDE.md README.md
│
├── Ciel_Bleu_de_Mayotte/           ← serie 2 (EN PROD.), structure auto-contenue
│   └── HTML/ IMAGES/ CHARACTER_SHEETS/ SCRIPTS/ REFERENCES/ STYLE_GUIDE.md 00_BRIEF.md README.md
│
└── Courage_Amina/                  ← serie 3 (EN PROD.), meme structure
    └── HTML/ IMAGES/ CHARACTER_SHEETS/ SCRIPTS/ REFERENCES/
```

Chaque serie est **auto-contenue** : son propre STYLE_GUIDE, ses propres characters, ses propres HTML. Ne pas melanger les assets d'une serie a l'autre.

## Convention de nommage des planches (OBLIGATOIRE)

- Format : `{EP}_{PLANCHE}.png` — ex: `1_00.png`, `3_07.png`, `5_11.png`
- Planche `_00` = transition d'ouverture
- Variantes alternatives : prefixe `X` (ex: `X4_10.png`, `X5_11.png`) — generees en parallele pour comparaison, gardees dans le meme dossier EP
- Variantes avec suffixe `X` apres le nom (ex: `1_01X.png`) = retouches/versions alternatives
- Les HTML referencent les images en chemins relatifs `../IMAGES/EP{X}/{X}_{YY}.png` — ne pas renommer sans mettre a jour le HTML

## Regle de versioning (heritee de SOUL.md section 14)

**Avant d'ecraser une image existante** : deplacer l'ancienne vers un sous-dossier `_archive/` (ou `archive_v{N}/`) avec un suffixe date (`1_01_v2_20260222.png`). Cette regle existe deja dans chaque `IMAGES/EP*/` — respecter la meme structure.

## Workflow typique (production d'une planche)

1. **Lire le character sheet** de chaque personnage present (ex: `CHARACTER_SHEETS/INAYA.md`) — copier le **bloc PROMPT DE BASE verrouille**, ne jamais paraphraser les traits physiques
2. **Lire le script de l'episode** (`SCRIPTS/EPISODE_X_*.md` pour les series, ou `_ARCHIVE/prompts_et_dialogues_complets.md` pour Maecha) pour le prompt de scene + dialogues
3. **Lire le STYLE_GUIDE** de la serie concernee — le bloc style (`Korean webtoon manhwa style, semi-realistic, soft cel-shading...`) doit etre inclus dans CHAQUE prompt, sans exception
4. **Generer via le skill RAYA** `skills/image-gen/SKILL.md` — appel `curl` vers OpenRouter avec `google/gemini-3-pro-image-preview` (realiste) ou `google/gemini-2.5-flash-image` (illustration). Ne pas appeler le modele image directement en tant que provider LLM
5. **Sauvegarder** dans `{Serie}/IMAGES/EP{X}/{X}_{YY}.png` — archiver l'ancienne version d'abord si remplacement
6. **Integrer dans le HTML** de l'episode : ajouter une `<div class="panel">` avec l'image et ses bulles/SFX positionnees en absolute (voir `TEMPLATES/webtoon_template.html` pour le modele de classes CSS : `.bubble`, `.bubble.thought`, `.narrator-box`, `.sfx`, `.notification`, `.transition-text`)

## Structure HTML (toutes series)

Chaque episode est un HTML **standalone** avec CSS inline — pas de fichier CSS partage, pas de JS, pas de build. Police Google Fonts (`Bangers` + `Comic Neue`). Conteneur `max-width: 450px` (format vertical mobile). Les bulles sont positionnees en `absolute` par rapport a chaque `.panel` — les coordonnees (`top`, `left`, `right`) sont ajustees manuellement par planche en fonction de la composition de l'image. Quand tu modifies une image, **verifier que les bulles sont toujours bien positionnees** (elles ne sont pas responsive au contenu de l'image).

Ressources PSP/3018/119 : OBLIGATOIRES dans l'episode 5 de chaque serie (bloc `.resources-box`).

## Contenu sensible — regles non-negociables

Les trois series traitent de sujets durs (cyber-harcelement, exploitation sexuelle, emprise). Jamais de :
- Actes sexuels, nudite, violence graphique
- Details de l'exploitation / traumatisme explicite

Techniques autorisees : ellipses, ombres, silhouettes, focus sur les reactions emotionnelles. Voir `Ciel_Bleu_de_Mayotte/00_BRIEF.md` section "Guidelines Sensibles".

## Git

Repository remote : `https://github.com/sirel976ent/maecha-vow-vow.git`. Branche `main`. Les commits suivent un format court en francais (`Add/Fix/Update <quoi> — <details>`). Pas de CI, pas de hook — le push suffit, nginx sert deja le dossier en live via bind-mount.

## Ce qu'il ne faut PAS faire ici

- Ne pas creer de `package.json`, `build/`, `node_modules/` — ce n'est pas une app
- Ne pas ecraser une image sans archiver l'ancienne (voir regle versioning)
- Ne pas modifier un character sheet "prompt de base" sans validation El-Farouk (consistance visuelle sur 57 planches)
- Ne pas deposer de fichier sensible (brouillons, credentials) — tout est publiquement accessible via `maecha.sirel976.com`
