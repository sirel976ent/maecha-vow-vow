# 🌊 LE CIEL BLEU DE MAYOTTE

## Kit de Production Webtoon - RAYA

---

## 📋 Informations Projet

| Attribut | Valeur |
|----------|--------|
| **Titre** | Le Ciel Bleu de Mayotte |
| **Format** | Webtoon vertical (9:16) |
| **Style** | Korean manhwa semi-réaliste |
| **Épisodes** | 5 |
| **Planches totales** | 57 |
| **Générateur** | Gemini via Nano Banana API |
| **Contexte** | PSP Mayotte - Sensibilisation |

---

## 📁 Structure du Kit

```
RAYA_KIT_CIEL_BLEU/
├── README.md                          ← CE FICHIER
├── 00_BRIEF.md                        ← Synopsis et contexte
│
├── 01_CHARACTER_SHEETS/
│   ├── MARIA.md                       ← Protagoniste (DESIGN VALIDÉ ✅)
│   ├── AICHA.md                       ← Sauveuse / Travailleuse sociale
│   ├── BEN.md                         ← Travailleur social
│   └── FILLES_REFUGE.md               ← Antagonistes (groupe)
│
├── 02_SCRIPTS/
│   ├── EPISODE_1_ARRIVEE.md           ← 11 planches
│   ├── EPISODE_2_FAUX_REFUGE.md       ← 11 planches
│   ├── EPISODE_3_ENGRENAGE.md         ← 12 planches
│   ├── EPISODE_4_MAIN_TENDUE.md       ← 11 planches
│   └── EPISODE_5_RENAITRE.md          ← 12 planches
│
└── 03_TEMPLATES/
    └── webtoon_template.html          ← Template HTML/CSS
```

---

## 🎯 Synopsis

**Maria**, jeune femme **malgache** de 20 ans, arrive à Mayotte pleine d'espoir. Seule et sans ressources, elle est recueillie par un groupe de jeunes filles qui lui offrent l'hébergement. Mais ce refuge cache un piège : exploitation sexuelle.

Après des semaines de cauchemar, **Aïcha**, une travailleuse sociale, remarque Maria au marché et lui glisse discrètement un numéro de téléphone. Maria trouve le courage d'appeler. Elle est mise en sécurité, se reconstruit, et finit par tendre la main à son tour à une autre jeune fille en danger.

---

## 🎨 Style Visuel

### Bloc Art Style (à copier dans CHAQUE prompt)
```json
"art_style": "Korean webtoon manhwa style illustration, semi-realistic rendering, soft cel-shading, clean thin black outlines, high quality digital art."
```

### Règles Visuelles
| ✅ FAIRE | ❌ NE PAS FAIRE |
|----------|-----------------|
| Vêtements UNIS (plain solid) | Motifs floraux/géométriques |
| Couleurs distinctes par personnage | Mêmes couleurs |
| Style manhwa cohérent | Mélanger styles |
| Format vertical 9:16 | Autres formats |

---

## 👤 Personnages Principaux

### MARIA - Protagoniste
- **Origine:** Madagascar (Malgache)
- **Robe:** Jaune pâle unie
- **Cheveux:** Curly noir → blond ombre
- **Accessoire:** Bracelet or fin

### AÏCHA - Sauveuse
- **Origine:** Mahoraise
- **Tenue:** Salouva bleu-vert uni
- **Cheveux:** Afro court naturel
- **Accessoires:** Créoles argent

### BEN - Travailleur social
- **Origine:** Mahorais
- **Tenue:** Chemise bleu clair unie
- **Cheveux:** Courts noirs, barbe courte

### LES FILLES - Antagonistes
- **Fille 1:** Cornrows, t-shirt rouge foncé
- **Fille 2:** Cheveux courts, haut vert
- **Fille 3:** Chignon haut, robe grise

---

## 📊 Structure Épisodes

| EP | Titre | Planches | Arc Émotionnel |
|----|-------|----------|----------------|
| 1 | L'Arrivée | 11 | Espoir → Solitude → Soulagement |
| 2 | Le Faux Refuge | 11 | Gratitude → Doute → Inquiétude |
| 3 | L'Engrenage | 12 | Choc → Terreur → Effondrement |
| 4 | La Main Tendue | 11 | Vide → Courage → Sauvetage |
| 5 | Renaître | 12 | Guérison → Transmission → Espoir |

---

## 🔧 Workflow RAYA

### Étape 1 : Génération Image
```
1. Lire le script de l'épisode
2. Copier le prompt JSON de la planche
3. Envoyer à Gemini via Nano Banana API
4. Sauvegarder l'image : {EP}_{PLANCHE}.png
```

### Étape 2 : Validation
```
1. Vérifier consistance personnage (robe, cheveux, bracelet)
2. Vérifier style manhwa
3. Vérifier absence de watermark
4. Si OK → continuer, sinon → régénérer
```

### Étape 3 : Assemblage HTML
```
1. Créer dossier IMAGES/EP{X}/
2. Utiliser template HTML
3. Intégrer images + dialogues
4. Tester navigation
```

---

## 📂 Naming Convention

### Images
```
{EPISODE}_{PLANCHE}.png

Exemples:
1_00.png  → Épisode 1, Planche 00 (transition)
1_01.png  → Épisode 1, Planche 01
3_07.png  → Épisode 3, Planche 07
```

### Dossiers
```
/IMAGES/EP1/
/IMAGES/EP2/
/IMAGES/EP3/
/IMAGES/EP4/
/IMAGES/EP5/
/HTML/
```

---

## ⚠️ Notes Importantes

### Contenu Sensible
- Épisode 3 traite de l'exploitation sexuelle
- **JAMAIS** de contenu explicite
- Utiliser ellipses, ombres, suggestions
- Focus sur émotions, pas sur actes

### Consistance Maria
- Toujours copier le bloc CHARACTER identique
- Robe jaune pâle UNIE (pas de motifs)
- Bracelet or toujours visible
- Cheveux ombre noir→blond

### Message Final
- Inclure ressources d'aide réelles
- Numéro PSP Mayotte
- Message de soutien

---

## 🚀 Commandes RAYA

```
/webtoon brief          → Affiche le synopsis
/webtoon character X    → Affiche le character sheet de X
/webtoon episode X      → Affiche le script de l'épisode X
/webtoon prompt X_YY    → Affiche le prompt JSON de la planche
/webtoon batch X        → Génère toutes les planches de l'épisode X
```

---

## 📞 Contact

**Projet:** PSP Mayotte - Parcours de Sortie de Prostitution
**Développeur:** SIREL976
**Site:** https://sirel976.com

---

*Kit de Production - Le Ciel Bleu de Mayotte*
*Version 1.0 - Mars 2026*
