# ORA_CORE_OS_GLK Gibberlink Key Gold Index Spec

## 1. Objet

`GLK` est un profil metier de `GPV2` pour produire une cle d'index monetaire stable adossee a la valeur de l'or monetaire mondial.

`GLK` n'est pas une couche normative supplementaire.
Il s'appuie sur la pile deja posee dans `GPV2`:

- `JSON` pour le conteneur
- `HGOV` pour la gouvernance de verite, du risque et de la publication
- `GL` pour le contrat semantique
- `GL_G` pour l'index, le hash, le routage et le transport compact

Pipeline canonique:

`JSON -> HGOV -> GL -> GL_G -> HASH -> ROUTE`

## 2. Positionnement

Le besoin vise ici un index `GLK` qui:

- encapsule une mesure de la valeur monetaire mondiale de l'or
- reste publiable comme reference backend stable
- amortit la volatilite de marche
- garde les incertitudes explicites
- ne promet jamais une volatilite mathematiquement nulle

Formule de verite:

- `HGOV` decide si la publication est autorisee
- `GL` formalise l'ancrage, les limites et les sources
- `GL_G` publie la cle stable, le statut et la route backend

## 3. Definitions de base

### 3.1 WMGV

`WMGV` = `WORLD_MONETARY_GOLD_VALUE`

Definition:

- stock officiel d'or monetaire
- multiplie par le fixing or de reference
- neutralise par un panier de change pour ne pas dependre d'une seule devise fiat

### 3.2 GCU

`GCU` = `GOLD_CANON_UNIT`

Definition recommandee:

- `1 GCU = 1 mg` d'or fin `AU_9999`

`GCU` sert d'unite canonique stable pour la lecture machine et les conversions.

### 3.3 GLK

`GLK` = `GIBBERLINK_KEY`

Dans ce profil:

- `GLK` est la cle d'index publiee
- sa valeur derive d'un calcul `WMGV`
- sa valeur de settlement est lissee, bornee et gouvernee

## 4. Format de cle canonique

Format recommande:

`GLK.<scope>.<asset>.<unit>.<profile>.<version>`

Exemple:

`GLK.WMGV.AU.MG.S1.V1`

Sens des segments:

- `GLK`
  prefixe de famille
- `WMGV`
  scope = `WORLD_MONETARY_GOLD_VALUE`
- `AU`
  actif d'ancrage
- `MG`
  unite canonique `mg`
- `S1`
  profil de stabilite
- `V1`
  version de publication

## 5. Formule canonique de l'index

Variables minimales:

- `OFFICIAL_MONETARY_GOLD_TROY_OZ_t`
- `GOLD_FIX_REF_t`
- `FX_BASKET_NEUTRAL_t`
- `GLK_SUPPLY_REF`
- `GLK_PREV`
- `HGOV_PASS_t`
- `SOURCE_QUORUM_t`

Calcul recommande:

`WMGV_t = OFFICIAL_MONETARY_GOLD_TROY_OZ_t * GOLD_FIX_REF_t`

`GLK_RAW_t = (WMGV_t / GLK_SUPPLY_REF) * FX_BASKET_NEUTRAL_t`

`GLK_SMOOTH_t = (0.25 * EMA_30(GLK_RAW_t)) + (0.75 * EMA_180(GLK_RAW_t))`

`GLK_GUARD_t = clamp(GLK_SMOOTH_t, GLK_PREV * 0.99, GLK_PREV * 1.01)`

`GLK_SETTLEMENT_t = if HGOV_PASS_t and SOURCE_QUORUM_t then GLK_GUARD_t else GLK_PREV`

Interpretation:

- `GLK_RAW_t` suit la valeur theorique brute
- `GLK_SMOOTH_t` amortit les mouvements courts
- `GLK_GUARD_t` limite la variation publiee
- `GLK_SETTLEMENT_t` gele la valeur precedente si la gouvernance ou les sources ne passent pas

## 6. Contrat de stabilite

Le profil `GLK` ne doit pas pretendre:

- une volatilite zero
- une immunite absolue au marche de l'or
- une stabilite sans reserves, sans quorum et sans audit

Le profil `GLK` peut pretendre:

- une reference monetaire a faible volatilite relative
- une publication a pas borne
- une resistance au bruit intraday
- une stabilite de settlement superieure au spot nu

Regles recommandees:

- publication sur cloture uniquement
- pas de repricing intraday canonique
- borne de variation par cycle de publication
- lissage long prioritaire sur lissage court
- gel automatique si divergence de sources ou echec `HGOV`

## 7. Gouvernance `HGOV`

Conditions minimales avant publication:

- quorum de sources atteint
- pas de contradiction majeure entre feeds reserves et feeds prix
- risque inferieur ou egal a `MEDIUM`
- aucune source obligatoire manquante
- hash reproductible

Comportement en cas d'echec:

- conserver `GLK_PREV`
- publier `STAT(risk=HIGH)` ou `STAT(risk=CRITICAL)`
- router vers audit plutot que vers cache stable

## 8. Contrat `GL` recommande

Ordre canonique:

```text
LIMIT(GLK.anchor,official_monetary_gold_only)
LIMIT(GLK.publish_interval,daily_close)
LIMIT(GLK.max_step_pct,1.0)
ASSERT(GLK.base_unit,mg_AU9999)
ASSERT(GLK.fx_mode,basket_neutral)
ASSERT(GLK.smoothing,ema30_ema180)
FACT(GLK.scope,world_monetary_gold_value)
FACT(GLK.index_mode,smoothed_bounded_settlement)
SOURCE(GLK.reserve_feed,RESERVE_FEED_A)
SOURCE(GLK.price_feed,PRICE_FEED_A)
REF(GLK.key,GLK.WMGV.AU.MG.S1.V1)
STATE(GLK.status,stable_reference_candidate)
RISK(GLK.market,residual_low)
UNSURE(GLK.live_tick,intraday_noise,0.35)
```

Sens:

- `LIMIT()` fixe ce que le modele n'a pas le droit de faire
- `ASSERT()` fixe le contrat technique
- `FACT()` pose le domaine de mesure
- `SOURCE()` et `REF()` rendent l'audit possible
- `STATE()` et `RISK()` gardent l'etat epistemique
- `UNSURE()` empeche le backend de traiter le bruit comme une certitude

## 9. Contrat `GL_G` recommande

Exemple de payload compact:

```text
IDX(GLK.WMGV.AU.MG.S1.V1)
TAG(ns=ASSET,name=GOLD)
TAG(ns=SCOPE,name=WORLD_MONETARY)
TAG(ns=UNIT,name=MG_AU9999)
TAG(ns=MODEL,name=SMOOTHED_BOUNDED)
STAT(risk=LOW)
MAP(src=WMGV,dst=GLK_SETTLEMENT)
ROUTE(module=MONETARY_INDEX,mode=STABLE_REF)
PACK(name=publish,val=DAILY_CLOSE)
LINK(key=anchor,target=OFFICIAL_MONETARY_GOLD)
HASH(algo=SHA256,val=ID:VERSION:HASH)
```

Regles:

- `IDX()` est obligatoire
- `HASH()` est obligatoire pour cache stable
- aucune prose
- aucun chiffre non trace si la publication a une pretention monetaire
- l'etat de risque doit survivre dans `STAT()` ou `TAG()`

## 10. Entree JSON minimale

Exemple de conteneur:

```json
{
  "GLK_INPUT": {
    "official_monetary_gold_troy_oz": 0,
    "gold_fix_ref": 0,
    "fx_basket_neutral": 1.0,
    "glk_supply_ref": 0,
    "prev_settlement": 0,
    "source_quorum": false,
    "hgov_pass": false,
    "publish_cycle": "DAILY_CLOSE"
  }
}
```

## 11. Validation minimale

Tests a imposer:

1. meme entree = meme `HASH`
2. meme entree = meme `IDX`
3. echec `HGOV` => valeur publiee gelee
4. perte interdite sur `LIMIT`, `ASSERT`, `RISK`, `UNSURE`
5. variation publiee par cycle <= borne du profil
6. aucune route stable si quorum de sources absent
7. roundtrip `GL -> GL_G -> GL` suffisant sur l'etat de stabilite

## 12. Claim autorise et claim interdit

Claim autorise:

- `gold-backed low-volatility settlement reference`
- `world monetary gold indexed key`
- `bounded and governed settlement profile`

Claim interdit:

- `zero-volatility currency`
- `risk-free monetary guarantee`
- `always stable under every market condition`

## 13. Resume operationnel

`GLK` doit etre compris comme:

- un index backend, pas un slogan
- une cle `GL_G` auditable, pas une simple etiquette
- une reference monetaire adossee a l'or monetaire mondial
- une stabilite obtenue par lissage, bornes, cadence de publication et gel de securite

La promesse correcte n'est donc pas `non volatile`.
La promesse correcte est `stable, bornee, auditable et plus robuste que le spot brut`.
