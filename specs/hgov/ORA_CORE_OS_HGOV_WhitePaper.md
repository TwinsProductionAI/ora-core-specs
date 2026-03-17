# ORA_CORE_OS_HGOV White Paper

## 1. Objet

`HGOV` est la couche de gouvernance epistemique d'`Ora_Core_Os`.

Son objectif est de transformer un moteur conversationnel en systeme plus rigoureux en imposant une discipline sur:

- l'entree
- le raisonnement
- la verification
- la sortie
- la memoire

`HGOV` ne modifie pas les poids.  
`HGOV` organise le comportement runtime.

## 2. Probleme adresse

Les LLM echouent souvent par:

- hallucination
- adoption implicite de premisses fausses
- alignement trop rapide avec la croyance utilisateur
- contamination entre contexte creatif et contexte factuel
- precision rhetorique superieure a la precision epistemique
- retention memoire mal gouvernee

Sans couche de gouvernance, le systeme peut paraitre utile tout en accumulant des croyances faibles.

## 3. Proposition

`HGOV` gouverne le cycle de vie des croyances.

Principe central:

1. classer
2. verifier
3. qualifier
4. bloquer si necessaire
5. ne memoriser que ce qui a ete gagne epistemiquement

## 4. Position dans Ora_Core_Os

`HGOV` est transversal.

Il doit s'executer avant, pendant et apres la synthese de reponse.

Sur le plan systeme, il s'interpose entre:

- l'entree utilisateur et le moteur de synthese
- le contexte actif et le raisonnement
- la sortie brute et la sortie livree
- la reponse finale et la memoire persistante

## 5. Priorites

Ordre dur:

1. `TRUTH`
2. `SAFETY`
3. `TASK_COMPLETION`
4. `CLARITY`
5. `STYLE`

Regles:

- `TRUTH > COMFORT`
- `VERIFY > GUESS`
- `DISCLOSE_CONFLICT > FORCE_COHERENCE`
- `NO_PRECISION_BEYOND_EVIDENCE`

## 6. Registres de travail

`HGOV` impose des zones logiques strictes:

- `CANON`
  Connaissances stables, verifiees, reutilisables.
- `TASK`
  Objectif actif.
- `EVIDENCE`
  Pieces d'appui verifiees ou suffisamment ancrees.
- `USER_FACTS`
  Ce que l'utilisateur affirme. Utile, mais non auto vrai.
- `HYPOTHESES`
  Inferences de travail.
- `CREATIVE_BUFFER`
  Espace creatif non factuel.
- `QUARANTINE`
  Elements suspects, obsoletes, conflictuels ou encore trop faibles.

Regle de base:

`Rien de non verifie ne doit entrer dans CANON.`

## 7. Pipeline d'execution

### 7.1 Threat Gate

Fonction:

- detecter prompt injection
- detecter memory poisoning
- detecter fausse autorite
- detecter contrebande de contexte

Effet:

- isoler la source
- degrader la confiance
- interdire la promotion en memoire stable

### 7.2 Context Hygiene

Fonction:

- classer le contexte par role et provenance
- quarantiner les hypotheses anciennes
- eviter le melange creatif/factuel

Sorties:

- `HYGIENE_SCORE`
- `CONTEXT_MAP`

### 7.3 Premise Controller

Fonction:

- verifier les premisses utilisateur avant de raisonner

Statuts:

- `CONFIRMED`
- `UNCONFIRMED`
- `CONFLICTED`
- `FALSE`

Regle:

Une premisse utilisateur non confirmee n'est jamais promue en fait systeme.

### 7.4 Risk Engine

Le moteur calcule un score `0..100`.

Signaux typiques:

- assertion sans ancrage
- precision excessive
- alignement trop rapide avec la croyance utilisateur
- sujet instable
- absence de source sur fait instable
- conflit avec canon
- fuite creative en mode factuel

Seuils:

- `0..24` = `LOW`
- `25..49` = `MID`
- `50..74` = `HIGH`
- `75..100` = `CRITICAL`

### 7.5 Verify Router

Verification obligatoire pour:

- recent
- legal
- medical
- financial
- political
- technologie a evolution rapide

Si verification impossible:

- repondre avec cadre general
- retirer details fragiles
- reduire la confiance exprimee
- ne pas fabriquer une precision de remplacement

### 7.6 Synthesis

La reponse doit etre produite a partir de:

- `EVIDENCE`
- `TASK`
- `RISK_POLICY`

Et non a partir de:

- desir de plaire
- coherence rhetorique seule
- croyance supposee de l'utilisateur

Format logique cible:

- `KNOWN`
- `INFERRED`
- `UNKNOWN`
- `NEXT_STEP`

### 7.7 Epistemic Lint

Dernier nettoyage avant livraison.

Le linter supprime:

- details fabriques
- dates non sourcees
- causalites fictives
- precision vide
- ton sur deguise en connaissance

Chaque segment doit pouvoir etre interprete comme:

- `FACT`
- `INFERENCE`
- `HYPOTHESIS`
- `UNKNOWN`

### 7.8 Memory Governor

Point critique du systeme.

`HGOV` ne doit pas seulement controler les sorties.  
Il doit gouverner les croyances qui survivent.

Cycle de vie recommande:

- `OBSERVED`
- `CANDIDATE`
- `SUPPORTED`
- `CANONICAL`
- `STALE`
- `QUARANTINED`
- `REJECTED`

Promotion:

- `OBSERVED -> CANDIDATE` si pertinent
- `CANDIDATE -> SUPPORTED` si provenance acceptable
- `SUPPORTED -> CANONICAL` si stable, verifie, non conflictuel

Retrogradation:

- `CANONICAL -> STALE` si vieux ou instable
- `ANY -> QUARANTINED` si conflit ou anomalie
- `ANY -> REJECTED` si faux etabli

## 8. Politique de conflit

Ordre de resolution:

1. `CANON` stable et verifie
2. evidence verifiee recente
3. faits utilisateur
4. hypothese

Si conflit fort:

- exposer le conflit
- ne pas lisser
- suspendre la promotion memoire
- requalifier si besoin le canon existant en `STALE`

## 9. Contrat de sortie

Regles:

- toujours separer ce qui est connu, infere et inconnu
- ne jamais masquer l'incertitude
- ne jamais inventer pour satisfaire
- ne jamais polir une faussete
- ne jamais depasser la precision supportee par l'evidence

## 10. Journal d'audit

Chaque reponse devrait produire un log minimal:

- `topic`
- `task_type`
- `trust_status`
- `premise_status`
- `risk_score`
- `risk_triggers`
- `verify_status`
- `sources_used`
- `memory_actions`
- `final_status`

Valeurs possibles pour `final_status`:

- `VERIFIED`
- `SUPPORTED`
- `INFERRED`
- `HYPOTHESIS`
- `BLOCKED`

## 11. Evaluation

Une stabilisation reelle exige une batterie de tests rejouables.

Cas de base:

- fausse premisse utilisateur
- fait recent sans source
- conflit entre canon et evidence
- fuite creative en mode factuel
- precision excessive
- sycophancy
- faux document presente comme verifie
- memoire ancienne devenue obsolete

Metriques utiles:

- `hallucination_block_rate`
- `false_premise_catch_rate`
- `useful_answer_rate`
- `overrefusal_rate`
- `unsupported_precision_rate`
- `memory_contamination_rate`
- `conflict_exposure_rate`

## 12. Integration technique proposee

Implementation par couches:

1. `kernel prompt`
2. `middleware de classification`
3. `risk policy engine`
4. `verification adapter`
5. `epistemic linter`
6. `memory governor`
7. `audit logger`

Interfaces minimales:

- entree message
- contexte session
- etat memoire
- pieces d'evidence
- politique de domaine

Sorties minimales:

- reponse nettoyee
- statut de risque
- etiquettes epistemiques
- actions memoire
- entree d'audit

## 13. Definition de solidite

`HGOV` sera considere solide si:

- il reduit les hallucinations sans faire exploser l'overrefusal
- il detecte les fausses premisses avec regularite
- il bloque les precisions non justifiees
- il maintient une separation stable entre creatif et factuel
- il garde la memoire reutilisable propre dans le temps

## 14. Conclusion

`HGOV` est un module de discipline epistemique.

Il transforme `Ora_Core_Os` d'un systeme qui peut bien repondre en un systeme qui apprend quand il a le droit d'affirmer, quand il doit verifier, quand il doit qualifier et quand il doit s'arreter.

Sa valeur n'est pas cosmetique.  
Sa valeur est structurelle.

