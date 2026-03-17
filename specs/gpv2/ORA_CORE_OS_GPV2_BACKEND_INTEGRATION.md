# ORA_CORE_OS_GPV2 Backend Integration

## Objectif

Faire de `GPV2` une couche runtime reelle dans le backend d'`Ora_Core_Os`.

## Flux recommande

1. recevoir l'entree en `JSON`
2. appeler `HGOV`
3. produire le contrat canonique `GL`
4. compresser en `GL_G`
5. calculer le `HASH`
6. router via `ROUTE()` et `TAG()`
7. ecrire cache ou memoire si le statut le permet
8. rendre `EN`, `FR` ou `NATIVE_FINAL` seulement si necessaire

## Regle d'or

Le backend ne doit jamais router a partir de `EN`, `FR` ou `NATIVE_FINAL`.

Il doit router a partir de:

- `GL`
- `GL_G`
- `HGOV` status

## Stockage recommande

- conserver `JSON` pour la structure et le debug
- conserver `GL` pour l'audit et la verite transportee
- conserver `GL_G` pour le cache, le routage et l'index
- conserver `HASH` pour la reproductibilite

## Ce qu'il faut eviter

- stocker des glyphes visuels comme cle primaire backend
- compresser avant le passage `HGOV`
- oublier le statut d'incertitude lors du passage en `GL_G`
- utiliser `META.ID` seul comme cle de cache

## Modules backend a brancher en premier

- orchestration
- memoire
- audit
- cache
- router de modules

## Condition de mise en prod interne

- JSON spec valide
- hash stable
- roundtrip suffisant
- tests de perte nulle sur le chemin factuel
- `HGOV` lie au pipeline
