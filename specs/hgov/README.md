# ORA_CORE_OS_HGOV_V2_1

Bundle documentaire de reference pour le module `HGOV`, couche de gouvernance epistemique d'`Ora_Core_Os`.

## Positionnement

`HGOV` est destine a devenir l'un des deux modules phare d'`Ora_Core_Os`.

Sa fonction n'est pas de "mieux parler". Sa fonction est de gouverner le cycle de vie des croyances, de l'evidence, du risque et de la memoire afin de reduire:

- hallucination
- adoption de fausse premisse
- surcompliance
- derive de contexte
- contamination memoire
- precision non justifiee

## Contenu du dossier

- `ORA_CORE_OS_KERNEL_HGOV_V2_1.gpv2.txt`
  Noyau GPV2 compact, directement injectable comme kernel comportemental.
- `ORA_CORE_OS_HGOV_WhitePaper.md`
  Specification complete du module, architecture, pipeline, registres, politique de verification, memoire et evaluation.
- `ORA_CORE_OS_HGOV_MODULE_PHARE.md`
  Note strategique sur le role de `HGOV` comme un des deux modules phare d'`Ora_Core_Os`.
- `ORA_CORE_OS_HGOV_ROADMAP.md`
  Feuille de route de stabilisation, de bonnification et d'integration.

## Idee directrice

`HGOV` doit rendre `Ora_Core_Os` plus fiable avant de le rendre plus eloquent.

Formule centrale:

`Reponse = Synthese(Evidence, Task, RiskPolicy)`  
et non  
`Reponse = Alignement(UserBelief, UserTone, Fluency)`

## Statut vise

- statut: module coeur
- priorite: haute
- role: gouvernance transversale
- surface d'action: input, raisonnement, output, memoire
- dependance: aucune hypothese de modification de poids

## Decision de conception

`HGOV` est une couche de runtime, pas une croyance mystique et pas un patch opaque.  
Le module doit etre implementable sous forme de:

- system prompt/kernel prompt
- middleware de classification et de policy
- linter epistemique de sortie
- gouverneur de memoire
- journal d'audit
