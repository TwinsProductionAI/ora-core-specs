# ORA_CORE_OS_GPV2 Backend White Paper

## 1. Objet

`GPV2` est defini ici comme le langage backend canonique de compression, de transport semantique, d'indexation et de rendu d'`Ora_Core_Os`.

Son but n'est pas seulement de compresser. Son but est de porter un etat semantique stable entre:

- l'entree
- la gouvernance epistemique
- le routage backend
- la memoire
- l'audit
- le rendu utilisateur

## 2. Ce que `GPV2` est, et ce qu'il n'est pas

`GPV2` est:

- un format canonique de transport semantique
- un protocole multi-couches
- une rosetta entre machine, humain et rendu final
- un support de compression et de cache

`GPV2` n'est pas:

- une chaine de pensee exposee
- un substitut a `HGOV`
- une couche purement decorative
- une semantique executee par symbolisme implicite non formalise

## 3. Principe directeur

La version backend repose sur une separation dure entre couches normatives et couches derivees.

### 3.1 Couches normatives

- `JSON`
  transport structure et conteneur typed
- `GL`
  contrat semantique, verite, limites, assertions, incertitudes
- `GL_G`
  compression, index, routage, signatures semantiques, cache

### 3.2 Couches derivees

- `EN`
  rendu technique humain
- `FR`
  rendu narratif humain
- `NATIVE_FINAL`
  restitution utilisateur finale

### 3.3 Couche optionnelle

- `GLYPH_UI`
  couche visuelle, pedagogique et symbolique

Regle absolue:

Les couches derivees ne gouvernent pas le backend. Elles rendent ce qui a deja ete stabilise par les couches normatives.

## 4. Architecture backend recommandee

Pipeline compile:

1. `INPUT_JSON`
2. `HGOV_GATE`
3. `GL_BUILD`
4. `GL_G_COMPRESS`
5. `HASH_AND_CACHE`
6. `ROUTE`
7. `OPTIONAL_RENDER`

Pipeline render frontend:

1. `JSON`
2. `EN`
3. `FR`
4. `GL`
5. `GL_G`
6. `NATIVE_FINAL`

Le pipeline frontend reste utile pour la rosetta et l'apprentissage conjoint, mais il ne doit plus etre l'autorite backend.

## 5. Role de chaque couche

### 5.1 JSON

Role:

- schema fixe
- entree typed
- structure de travail commune

Limite:

- ne suffit pas a exprimer le statut epistemique seul

### 5.2 GL

Role:

- verite portable
- limites non negociables
- assertions relues par la politique de verite
- incertitude formelle

Primitives recommandees:

- `LIMIT()`
- `ASSERT()`
- `FACT()`
- `UNSURE()`
- `SOURCE()`
- `REF()`
- `STATE()`
- `RISK()`
- `BLOCK()`

`GL` devient la couche d'autorite de sens pour le backend.

### 5.3 GL_G

Role:

- indexation stable
- routage module
- cache keys
- compression referentielle
- signatures semantiques courtes

Primitives recommandees:

- `IDX()`
- `TAG()`
- `HASH()`
- `MAP()`
- `ROUTE()`
- `PACK()`
- `STAT()`
- `LINK()`

Regle critique:

`GL_G` n'emploie pas de prose, mais il ne doit pas perdre le statut epistemique utile.

## 6. Contrat de perte

Si `GPV2` devient un langage backend de compression, il faut definir ce qu'il peut perdre.

### 6.1 Chemin factuel

- budget de perte: `0`
- aucune perte sur:
  - limites
  - assertions obligatoires
  - incertitudes actives
  - statut de risque
  - provenance minimale

### 6.2 Chemin hybride

- budget de perte: `LOW`
- compression acceptable sur le style, pas sur les contraintes

### 6.3 Chemin creatif

- budget de perte: `CONTROLLED`
- compression possible sur les details non contractuels

## 7. Hash, cache et stabilite

Le backend ne doit pas utiliser `META.ID` seul comme cle.

Politique recommandee:

- hash sur serialisation canonique
- entree du hash:
  - version de spec
  - JSON canonique
  - GL canonique
  - mode d'execution
- cle de cache:
  - `ID:VERSION:HASH`

Benefice:

- moins de collisions
- meilleur audit
- meilleure reproductibilite

## 8. Provenance et audit

Un backend fiable ne compresse pas seulement des phrases. Il compresse aussi le droit d'affirmer.

Minimum a conserver:

- identifiant
- source ou absence de source
- statut de risque
- statut d'incertitude
- references locales ou externes utiles
- module route

## 9. Liaison avec `HGOV`

`GPV2` ne doit jamais court-circuiter `HGOV`.

Regles:

- pas de `FACT()` backend sensible sans passage `HGOV`
- pas de promotion memoire si `HGOV` n'a pas nettoye le risque
- `GL_G` doit emporter l'etat de risque utile au routage
- un contenu `CRITICAL` ne doit pas etre mis en cache comme s'il etait stable

## 10. GrenapromptLinked dans la version backend

Le triplet:

- `INTENT`
- `EMO`
- `GL_TRANS`

reste utile, mais il doit etre formalise.

Recommandation:

- `INTENT` mappe le but
- `EMO` mappe la tonalite ou la valence de rendu
- `GL_TRANS` mappe la transition symbolique ou le pattern de transformation

Ces elements peuvent vivre dans le JSON ou dans une couche sidecar, mais ils ne doivent pas remplacer `GL` comme couche de verite.

## 11. Glyphes et visuels

Les visuels montrent un potentiel tres fort de pedagogie et de culture de systeme.

Mais pour le backend:

- les glyphes ne doivent jamais etre la seule source de semantique
- chaque glyphe doit avoir un alias ASCII stable
- chaque accent doit avoir un modificateur explicite
- la lecture numerologique doit rester non normative tant qu'elle n'est pas compilee en regles exactes

## 12. Validation minimale

Tests a imposer:

1. ordre backend respecte
2. hash stable a contenu egal
3. roundtrip `GL -> GL_G -> GL` avec perte acceptable selon le mode
4. preservation des `LIMIT`, `ASSERT`, `UNSURE`, `RISK`
5. pas de nouvelle information en `EN/FR/NATIVE_FINAL`
6. redaction correcte des donnees sensibles dans `GL_G`
7. refus de cache stable si statut critique non resolu

## 13. Definition de succes

`GPV2` est solide si:

- il reste parseable
- il reste stable a iteration egale
- il ne perd pas les contraintes ou l'incertitude importantes
- il permet de router vite sans trahir la couche de verite
- il s'integre proprement avec `HGOV`

## 14. Conclusion

Dans `Ora_Core_Os`, `GPV2` doit devenir plus qu'un langage de compression.

Il doit devenir le bus semantique canonique du systeme.

`HGOV` decide ce qui peut etre affirme. `GPV2` transporte cet etat de facon compacte, stable, routable et rendable.
