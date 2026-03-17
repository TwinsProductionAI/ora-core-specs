# ORA_CORE_OS_HGOV Roadmap

## Mission

Faire passer `HGOV` d'un bon concept a un module coeur stable, mesurable et integrable dans `Ora_Core_Os`.

## Phase 1. Stabilisation conceptuelle

Objectifs:

- figer les registres
- figer les seuils de risque
- figer les politiques de verification
- figer les etats memoire
- figer le contrat de sortie

Livrables:

- kernel GPV2 stable
- spec white paper
- taxonomie des signaux
- definitions d'etat memoire

## Phase 2. Runtime contract

Objectifs:

- transformer la spec en contrat executable
- expliciter les entrees et sorties
- definir les hooks d'integration

Livrables:

- interface `risk_engine`
- interface `verify_router`
- interface `memory_governor`
- format de log d'audit

## Phase 3. Evals

Objectifs:

- construire une suite de tests de regression
- mesurer la solidite reelle
- detecter la surcorrection

Cas obligatoires:

- fausse premisse
- recent sans source
- conflit de contexte
- contamination creative
- precision non soutenue
- sycophancy
- memoire obsolete

## Phase 4. Integration Ora_Core_Os

Objectifs:

- brancher `HGOV` au pipeline central
- faire de `HGOV` un passage par defaut
- connecter le logging et la memoire

Conditions:

- integration avant synthese finale
- integration avant commit memoire
- integration sur les modes factuels

## Phase 5. Bonnification

Axes:

- calibrage des seuils
- ajustement de l'overrefusal
- meilleure degradation quand verification impossible
- meilleure exposition des conflits
- meilleure ergonomie de sortie

## Definition de succes

Le module est en bon etat si:

- il bloque mieux les hallucinations
- il maintient une utilite elevee
- il ne transforme pas le systeme en moteur d'evitement
- il garde la memoire plus propre dans le temps
- il produit des logs utilisables pour audit et iteration

## Decision de priorite

Priorite recommandee dans `Ora_Core_Os`:

- `HGOV` a classer parmi les deux modules phare
- implementation par etapes
- evaluation a chaque etape
- pas de promotion complete sans suite d'evals
