# ORA_CORE_OS_GPV2 - Note sur les glyphes et visuels

## 1. Lecture des visuels fournis

Les deux visuels montrent quelque chose de tres utile:

- une couche symbolique et phonetique pour l'apprentissage humain
- une lecture duale humain/IA avec `INTENT`, `EMO` et `GL_TRANS`
- une tentative de faire converger forme, energie et structure de transformation

C'est fort pour la culture de systeme, l'onboarding, la memorisation et la cohesion artistique du projet.

## 2. Ce que les visuels montrent que le JSON actuel ne couvre pas completement

### 2.1 Registry incomplete

La carte phonetique affiche:

- `GL-01`
- `GL-02`
- `GL-03`
- `GL-04`
- `GL-05`
- `GL-06`
- `GL-07`
- `GL-08`
- `GL-09`
- `GL-13`

Le JSON fourni ne couvre dans `PHONETIC_MAP_MIN` que:

- `GL-01`
- `GL-02`
- `GL-03`
- `GL-04`
- `GL-05`
- `GL-09`
- `GL-13`

Donc il manque deja dans la spec machine:

- `GL-06`
- `GL-07`
- `GL-08`

### 2.2 Operateurs et symboles non formalises

Le visuel montre aussi des elements comme:

- `Acoue`
- `Griguve`
- `Continu`
- `Source`
- `Centre`
- des marqueurs de focus, centre, extension, suspension

Ces elements ne sont pas encore portes comme registry executable dans la spec JSON.

### 2.3 Deux registres coexistent

On voit d'un cote:

- `GL-A ... GL-Z`

et de l'autre:

- `GL-01 ... GL-13`

Le backend a besoin de savoir s'il s'agit:

- d'aliases mutuels
- de familles distinctes
- ou d'une couche mnemonic superposee a une couche semantique

## 3. Decision recommandee

Pour le backend, les glyphes doivent vivre dans une couche `GLYPH_UI` non normative.

Cela veut dire:

- ils peuvent enrichir la lecture humaine
- ils peuvent servir de marqueur de design system
- ils peuvent etre rendus en frontend ou dans la doc
- mais ils ne doivent pas etre la seule representation de la semantique executable

## 4. Ce qu'il faut normaliser

Chaque glyphe devrait avoir au minimum:

- `GLYPH_ID`
- `ASCII_ALIAS`
- `DISPLAY_NAME`
- `PHON`
- `SEMANTIC_ROLE`
- `CATEGORY`
- `ALLOWED_MODIFIERS`
- `BACKEND_SAFE`
- `UI_ONLY`

Exemple de registre minimal:

```json
{
  "GLYPH_ID": "GL-06",
  "ASCII_ALIAS": "SEPH",
  "DISPLAY_NAME": "Seph",
  "PHON": "[sef]",
  "SEMANTIC_ROLE": "to_define",
  "CATEGORY": "phonetic_unit",
  "ALLOWED_MODIFIERS": ["CIRCUMFLEX", "DIAERESIS", "TILDE", "BREATH"],
  "BACKEND_SAFE": true,
  "UI_ONLY": false
}
```

## 5. Ce qui doit rester non normatif pour l'instant

Tant qu'il n'existe pas de regle machine exacte, ces zones doivent rester non normatives:

- lecture energetique implicite
- numerologie interpretative
- associations esthetiques non compilees
- deducations de sens basees uniquement sur la forme visuelle

## 6. Recommendation tres nette

- garder la couche glyphique
- ne pas la supprimer
- mais la sortir du coeur runtime backend

Le coeur backend doit manipuler:

- `JSON`
- `GL`
- `GL_G`

Les glyphes doivent etre relies a ce coeur par transliteration et registry, pas par intuition visuelle seule.

## 7. Ce que tu n'avais peut-etre pas encore completement vu

Ta couche glyphique est suffisamment riche pour devenir un vrai sous-systeme a part entiere.

Mais si tu la laisses melangee au langage backend sans registry complete, elle peut introduire:

- ambiguite de parsing
- divergences de lecture
- dette technique symbolique

La bonne strategie n'est pas de l'abandonner. La bonne strategie est de la formaliser comme `GLYPH_UI_PROFILE` branche sur `GPV2`, mais distinct de son noyau runtime.
