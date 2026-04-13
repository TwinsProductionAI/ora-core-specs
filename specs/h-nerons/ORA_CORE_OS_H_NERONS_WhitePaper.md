# WHITE PAPER - H-NERONS

Version 1.0 - Avril 2026  
Source de travail: structuration operationnelle a partir de `H-NERONS_whitepaper.docx`

## Resume executif
H-NERONS est un module de gouvernance factuelle hybride pour Ora_Core_OS. Sa fonction n'est pas de rendre le LLM omniscient, mais de traiter la sortie du modele comme une hypothese textuelle a qualifier avant emission.

Le module detecte les claims verifiables dans le brouillon final, declenche une verification externe quand la politique le justifie, qualifie le niveau de confiance obtenu, puis contraint la formulation finale. La valeur attendue n'est pas une verite absolue, mais une fiabilite mieux gouvernee: moins de derives factuelles, plus de tracabilite, plus d'incertitude visible quand la validation ne suffit pas.

Dans un cadre PME, H-NERONS est utile sur les sujets ou une erreur recente, reglementaire, chiffrable ou technique coute du temps, de l'argent ou de la credibilite.

## 1. Probleme vise
Dans beaucoup de pipelines conversationnels, la reponse finale du LLM est traitee comme un texte plausible auquel on ajoute ensuite des garde-fous. Cette logique reste trop faible quand une affirmation factuelle influence une decision humaine.

Le probleme central n'est pas seulement l'hallucination. C'est l'absence d'une discipline de verification native capable de distinguer:

- une phrase rhetoriquement convaincante,
- une assertion verifiable,
- un sujet recent qui exige une verification externe,
- un claim trop incertain pour etre livre avec assertivite.

H-NERONS formalise cette discipline de verification pre-emission.

## 2. Definition stricte
H-NERONS est une porte de gouvernance situee entre le brouillon final du modele et l'emission utilisateur. Il:

- analyse le brouillon final,
- extrait les assertions verifiables,
- classe leur nature,
- orchestre une verification externe selon une politique de sources,
- qualifie chaque claim par statut,
- regenere ou borne la formulation finale,
- journalise les raisons de qualification pour audit.

H-NERONS ne promet pas l'infaillibilite.  
H-NERONS ne remplace pas le raisonnement du modele.  
H-NERONS ne doit pas exporter de donnees privees vers l'exterieur.  
H-NERONS ne doit jamais maintenir une affirmation forte si la verification est insuffisante.

## 3. Positionnement architectural
Dans Ora_Core_OS, H-NERONS doit etre pense comme une brique transversale de gouvernance factuelle:

- le LLM produit un brouillon final,
- H-NERONS decide si des claims doivent etre verifies,
- HGOV conserve l'autorite epistemique sur le risque et la prudence,
- GPV2 transporte les statuts, tags et traces d'audit,
- l'orchestrateur peut imposer H-NERONS sur les demandes factuelles instables ou a fort impact.

Le module n'est donc pas un moteur de generation autonome. C'est un regulateur pre-emission centre sur les faits verifiables.

## 4. Taxonomie minimale des assertions
Tous les claims ne demandent pas la meme politique. La taxonomie minimale issue du white paper est:

- `FACT_STATIC`: fait stable a faible variabilite temporelle,
- `FACT_DYNAMIC`: fait recent ou susceptible d'evoluer,
- `NUMERIC_VOLATILE`: chiffre, prix, date, volume, indicateur ou toute valeur rapidement caduque,
- `RULE_REGULATORY`: loi, norme, regle ou contrainte formelle,
- `TECH_COMPAT`: compatibilite, version, prerequis, support, integration,
- `INTERPRETIVE_CLAIM`: synthese ou lecture raisonnee qui ne peut pas toujours recevoir un verdict binaire.

Cette taxonomie permet d'adapter:

- la priorite des sources,
- le besoin de fraicheur,
- le seuil de verification,
- le niveau d'assertivite autorise en sortie.

## 5. Pipeline operatoire recommande
Le pipeline defendable pour H-NERONS est le suivant:

1. `detect`: analyser le brouillon final et isoler les claims verifiables.
2. `classify`: typer chaque claim selon la taxonomie minimale.
3. `lookup`: interroger des sources eligibles selon la politique de sources.
4. `cross_check`: comparer le claim interne avec le consensus externe pondere.
5. `qualify`: affecter un statut explicite et un niveau de confiance.
6. `regulate`: reformuler, borner ou bloquer selon le statut obtenu.
7. `emit_or_degrade`: produire la version finale, ou basculer vers une sortie prudente.
8. `audit`: conserver les raisons, tags et traces minimales utiles.

L'ordre compte. Sans qualification explicite, la regeneration risquerait de masquer l'incertitude au lieu de la gouverner.

## 6. Politique de sources
La verification ne doit pas dependre d'un simple `top 3`. La politique minimale implique:

- priorite aux sources primaires quand elles existent,
- priorite ensuite aux sources officielles,
- recours encadre aux sources secondaires reconnues,
- ponderation par `authority`, `freshness`, `relevance`, `inter_source_agreement`,
- refus des requetes contenant des donnees privees ou non necessaires,
- tracabilite des raisons de selection et des conflits observes.

Une source recente mais peu autoritaire ne doit pas l'emporter par defaut sur une source officielle. Inversement, une source autoritaire mais obsolete ne doit pas valider un claim dynamique.

## 7. Etats de qualification
Chaque claim doit recevoir un statut explicite:

| Statut | Signification | Action systeme |
| --- | --- | --- |
| `VERIFIED` | Accord suffisant entre claim interne et sources externes qualifiees | Autoriser une formulation normale avec tracabilite optionnelle |
| `PARTIALLY_VERIFIED` | Validation partielle avec zones d'ombre restantes | Limiter le perimetre du claim et rendre les reserves visibles |
| `CONFLICT_DETECTED` | Contradiction significative entre le modele et les sources | Regenerer sous contrainte ou exposer le conflit proprement |
| `UNSURE_EXTERNAL` | Donnees externes insuffisantes ou non exploitables | Reduire l'assertivite et preparer une sortie prudente |
| `UNSURE_EXPLICIT` | Sujet critique ou verification insuffisante | Bloquer l'affirmation forte et rendre l'incertitude explicite |

## 8. Regeneration contrainte et mode degrade
H-NERONS ne doit pas simplement ajouter un label. Il doit contraindre la forme finale:

- `VERIFIED` autorise une formulation normale,
- `PARTIALLY_VERIFIED` oblige une portee reduite ou des reserves visibles,
- `CONFLICT_DETECTED` interdit la formule affirmative lisse et impose soit une regeneration bornee, soit l'exposition du conflit,
- `UNSURE_EXTERNAL` degrade la reponse vers une formulation prudente,
- `UNSURE_EXPLICIT` bloque toute affirmation forte sur un sujet critique.

Le mode degrade est un comportement normal, pas un echec. Il permet au systeme de dire:

- que les donnees externes sont insuffisantes,
- qu'un conflit subsiste,
- qu'une verification supplementaire serait necessaire,
- que la prudence est plus rigoureuse qu'une fausse certitude.

## 9. Artefacts de sortie
Pour etre exploitable comme module, H-NERONS doit produire des artefacts stables:

- `claim_audit`: liste des claims detectes, typage et statut final,
- `qualification_status`: etat final par claim et raison associee,
- `source_trace`: sources retenues, priorite et niveau d'accord,
- `regulated_response`: texte final borne par le statut obtenu,
- `conflict_notice`: explication concise en cas de contradiction significative,
- `uncertainty_notice`: formulation explicite quand la verification ne permet pas d'affirmer.

Ces artefacts servent autant a la livraison utilisateur qu'a l'audit interne.

## 10. Benefices reels
Si les contraintes sont respectees, H-NERONS apporte:

- moins de reponses convaincantes mais risquees,
- une meilleure gestion des sujets recents ou volatils,
- une reduction des erreurs sur regles, compatibilites et donnees chiffrables,
- une meilleure capacite a dire non, a ralentir ou a avertir,
- une tracabilite plus defendable des sorties factuelles.

## 11. Limites
Le white paper est clair sur les limites du module:

- la verification externe ne garantit pas la verite totale,
- la qualite depend fortement de la politique de sources,
- des conflits entre sources peuvent rester irresolus,
- le gain de fiabilite a un cout de latence,
- le module doit etre presente comme un mecanisme de fiabilite gouvernee, pas comme une promesse d'infaillibilite.

## 12. Regles fondatrices
Les lois de H-NERONS peuvent etre formulees ainsi:

1. Ne jamais confondre verification externe et verite absolue.
2. Prioriser les sources primaires ou officielles quand elles existent.
3. Rendre l'incertitude visible plutot que la masquer.
4. Bloquer l'assertivite forte quand la validation est insuffisante.
5. Ne jamais envoyer de donnees privees vers les requetes externes.
6. Journaliser les etats et les raisons de qualification pour audit.

## 13. Traduction modulaire
Pour une implementation propre dans Ora_Core_OS, H-NERONS se decompose en six sous-fonctions:

- `claim_detector`: extrait les assertions verifiables du brouillon final,
- `claim_classifier`: attribue un type et un niveau de risque,
- `source_policy_engine`: choisit les sources eligibles et la strategie de lookup,
- `cross_check_engine`: calcule le consensus pondere et la contradiction,
- `qualification_engine`: attribue le statut final et le niveau de confiance,
- `bounded_regenerator`: reformule la sortie selon les contraintes du statut.

Le module ne doit pas devenir un crawler generaliste. Il reste une couche de regulation a perimetre borne.

## Conclusion
H-NERONS deplace le centre de gravite du systeme: la sortie du LLM n'est plus presumee legitime, elle devient une hypothese a qualifier avant emission.

Dans Ora_Core_OS, cette inversion est precieuse pour les environnements ou la fiabilite factuelle prime sur la fluidite brute. Le module est donc defendable s'il reste:

- borne,
- tracable,
- prudent,
- respectueux de la vie privee,
- oriente verification plutot que performance rhetorique.

## Annexe A - Mapping GPV2 minimal
`ROLE=hybrid_evidence_regulation_node|GOAL=detect_verifiable_claims_verify_externally_qualify_confidence_and_bound_final_output|CTX=ora_core_os_pre_emit_factual_governance|C=[no_private_data_outbound;prioritize_primary_and_official_sources;verify_only_when_claim_is_verifiable_and_policy_requires_it;block_strong_claim_if_verification_insufficient;make_uncertainty_explicit;log_qualification_reasons_and_sources]|OUT={artifacts=[claim_audit;qualification_status;source_trace;regulated_response;conflict_notice];format=json_plus_bounded_text;apply_mode=pre_emit_gate_only}|FAIL=[web_unavailable=>UNSURE_EXPLICIT;quota_exceeded=>UNSURE_EXPLICIT;source_conflict_high=>bounded_answer_plus_conflict_notice;privacy_risk=>abort_lookup_and_downgrade]|CHECK=[verifiable_claim_detected;source_authority_ranked;freshness_fit_to_claim_type;confidence_qualified;no_overclaiming_after_regulation]`

## Annexe B - Formulation courte
H-NERONS = detection de claims verifiables + verification externe ponderee + qualification explicite + regeneration bornee + sortie prudente si la verification ne suffit pas.
