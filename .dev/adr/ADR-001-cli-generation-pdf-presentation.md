# ADR-001 — CLI de génération du pdf de présentation, porté in-repo

- **Statut** : Accepté
- **Date** : 2026-07-07
- **Décideurs** : Jérémy Viau-Trudel (noumanity)
- **Sources** : `PLN-002-skills-materiel-presentation.md`, `.dev/session.md` (tâche 2), `ADR-001-stack-technologique.md` du dépôt `review_impact-of-PQC-risks-on-main-Linux-distributions`

## Contexte

Ce dépôt doit produire le pdf de la présentation du 2026-07-07 (Rencontre Linux au Québec). Un CLI de génération de pdf de présentation existe déjà, validé, dans le dépôt d'une présentation RLQ antérieure (`review_impact-of-PQC-risks-on-main-Linux-distributions`) : orchestrateur bash (`scripts/dev.sh`) pilotant un moteur Lua/LuaLaTeX/Beamer. L'humain a confirmé (session.md, tâche 2, point 2) que ce script est fonctionnel et a demandé son **portage in-repo**, sans redesign, pour un usage direct dans ce dépôt.

Contrainte de délai : la présentation a lieu le jour même de cette décision — reconstruire une chaîne de génération de pdf sous une contrainte de temps courte est un risque plus grand que réutiliser un outil déjà éprouvé.

## Décision (résumé)

> Porter tel quel, à la racine de ce dépôt, le CLI `dev.sh` et son moteur Lua/LuaLaTeX/Beamer du dépôt source — améliorations mineures à faible impact seulement, pas de changement de stack ni de redesign architectural.

## Décisions détaillées

### Rendu et prétraitement
- **Décision** : reprise intégrale de la stack source — Beamer + LuaLaTeX, thème `beamerthemeNoumanity` (base metropolis), prétraitement bash + Lua (`texlua`, `etlua`, `lunamark`).
- *Alternatives écartées* : redesigner avec pandoc, reveal.js/marp, ou une autre stack — écartées car un redesign sous contrainte de délai (présentation le jour même) introduit un risque d'indisponibilité du pdf plus grand que le bénéfice d'un outil « plus propre » ; l'humain a explicitement demandé un portage, pas une refonte (session.md, tâche 2, point 2).

### Emplacement in-repo
- **Décision** : miroir de la convention du dépôt source, à la racine de ce dépôt : `scripts/`, `templates/`, `activate`, `src/` (contenu des diapos), `config.yaml`, `dist/` (pdf final, suivi par git), `workdir/` (temporaire, ignoré par git). `.dev/` reste réservé aux livrables de gouvernance (plans, fondations, skills, ADR) — le CLI n'y va pas.
- *Alternatives écartées* : loger le CLI sous `.dev/` avec le reste des livrables de gouvernance — écartée car le CLI n'est pas un document de gouvernance versionné avec séquence (`PLN-`, `FND-`, `ADR-`), c'est un outil applicatif ; le mélanger aux livrables de gouvernance aurait cassé la convention `.dev/<type>/<PREFIX>-<SEQ>-<SLUG>.md`.

### Portée du portage
- **Décision** : copie fonctionnelle + améliorations mineures à faible impact sur la robustesse uniquement. Les constats plus lourds (cohérence de l'interface CLI au regard des pratiques standards de l'industrie, architecture applicative actuelle) sont consolidés séparément et proposés dans un plan distinct (`PLN-004`), non exécutés ici.
- *Alternative écartée* : refactoring en profondeur dans le cadre de ce portage — explicitement écartée par l'humain (session.md, tâche 2, point 2 : « Ne pas faire un gros refactoring »).

### Dépendances système
- **Constat** (vérifié dans cet environnement) : `texlua` et `lualatex` sont disponibles. `latexmk` est absent — non bloquant, `dev.sh` gère déjà ce cas par un repli sur une double passe `lualatex` directe. `luarocks` est absent — à vérifier au codage (étape suivante) : le module `etlua` est vendorisé dans `scripts/lib/` côté source (pas de dépendance `luarocks` à l'exécution pour ce module) ; les autres modules Lua (`lunamark`, parseur YAML) restent à confirmer.

## Conséquences

**Positives**
- Réutilisation d'un outil déjà validé (a produit un pdf fonctionnel dans le dépôt source le 2026-06-17) : risque d'indisponibilité du pdf minimisé pour une échéance le jour même.
- Séparation orchestration (bash) / transformation de contenu (Lua) déjà propre, héritée sans coût de conception supplémentaire.
- Abstraction Markdown + modèle (`content.md` + `model`) préservée : l'auteur humain n'a pas à toucher au LaTeX.

**Négatives / risques**
- Dépendances système lourdes (TeX Live quasi complet) requises dans tout environnement voulant régénérer le pdf ; `luarocks` absent dans cet environnement, à vérifier/vendoriser.
- Aucun test automatisé sur le CLI (hérité du dépôt source) ; la vérification reste manuelle (génération + inspection visuelle du pdf).
- Couplage aux conventions héritées (`src/slide-<SEQ>/content.md`, `templates/models/*.yaml`) : tout changement de convention nécessitera de revisiter le moteur Lua, pas seulement `dev.sh`.
- Interface CLI et architecture applicative non revues en profondeur dans ce portage (voir `PLN-004`) : les défauts identifiés (ex. absence de `-h`, pas de `--version`, config résolue inconditionnellement même pour des commandes qui n'en ont pas besoin) subsistent tels quels après ce portage.

## Migration / porte de sortie

Cette décision ne figera pas la stack au-delà de ce qui est nécessaire : l'abstraction contenu/modèle héritée de l'ADR source préserve la possibilité de changer de moteur de rendu plus tard sans réécrire le contenu des diapositives. Les interventions plus lourdes sur l'interface CLI et l'architecture applicative, si elles sont retenues, seront proposées et actées via `PLN-004`, pas par cet ADR.

## Références

- `.dev/plans/PLN-002-skills-materiel-presentation.md`
- `.dev/session.md` (tâche 2, points 2 et 3)
- `$HOME/git/noumanity-communication/review_impact-of-PQC-risks-on-main-Linux-distributions/.dev/adr/ADR-001-stack-technologique.md`
