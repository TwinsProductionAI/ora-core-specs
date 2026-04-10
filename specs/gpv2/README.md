# ORA_CORE_OS_GPV2_BACKEND_V2_3

Bundle documentaire pour la version backend de `GPV2`, langage de compression, de transport semantique et de routage d'`Ora_Core_Os`.

## Positionnement

`GPV2` doit devenir le second module phare d'`Ora_Core_Os`, en paire avec `HGOV`.

- `HGOV` gouverne la verite, le risque, la memoire et les limites.
- `GPV2` transporte, compresse, indexe et rend les etats semantiques de facon stable.

Sans `HGOV`, `GPV2` compresse vite mais peut compresser une erreur.
Sans `GPV2`, `HGOV` raisonne juste mais sans bus semantique stable pour le backend.

## Decision centrale

La version fournie ici transforme `GPV2` d'un pipeline surtout rosetta/front-end en un langage backend canonique.

Cela implique:

- `JSON`, `GL` et `GL_G` deviennent les couches normatives.
- `EN`, `FR` et `NATIVE_FINAL` deviennent des rendus derives.
- `GLYPH_UI` devient une couche optionnelle de visualisation et de pedagogie.
- `HGOV` devient obligatoire sur les chemins factuels et memoire.

## Fichiers

- `ORA_CORE_OS_GPV2_BACKEND_ANALYSE.md`
  Analyse critique, angles morts et corrections retenues.
- `ORA_CORE_OS_GPV2_BACKEND_INTEGRATION.md`
  Notes d'integration runtime backend.
- `ORA_CORE_OS_GPV2_BACKEND_WhitePaper.md`
  White paper de la version backend.
- `ORA_CORE_OS_GPV2_BACKEND_SPEC_V2_3_PUBLIC.json`
  Spec machine corrigee et bonnifiee.
- `ORA_CORE_OS_GPV2_GLYPH_UI_NOTE.md`
  Note sur les visuels, les glyphes et ce qui doit rester non normatif.
- `ORA_CORE_OS_GLK_GIBBERLINK_KEY_GOLD_SPEC.md`
  Profil `GLK` pour un index backend adosse a la valeur de l'or monetaire mondial.
- `ORA_CORE_OS_GLK_GIBBERLINK_KEY_GOLD_PROFILE.json`
  Profil machine `GLK` pour cle, formule, hash et routage.

## Ce qui change par rapport a la version fournie

- suppression de la contradiction `FRONTEND_ONLY=true` versus usage backend
- inversion conceptuelle de l'autorite: la verite part de `GL`, pas de `EN/FR`
- preservation de l'incertitude dans la compression backend
- hash et cache durcis
- separation nette entre semantique executable et symbolique glyphique
- ajout d'un contrat de perte, de roundtrip et de provenance
- ajout d'un profil `GLK` pour un index monetaire adosse a l'or avec stabilisation gouvernee
