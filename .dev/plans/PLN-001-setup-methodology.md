# PLN-001 — Mise en place de la méthodologie de travail

**Statut : exécuté**

---

## Changelog

- **v1** : première proposition, basée sur la version initiale de `session.md` (racine du dépôt), avec `GOVERNANCE.md` et dossier `plans/`.
- **v2** : révision suite à la mise à jour de `session.md` (déplacé vers `.dev/session.md`) : `GOVERNANCE.md` renommé en `CONSTITUTION.md`, dossier des plans confirmé à `.dev/plans/`, ajout des livrables « recherche de fondation » et « skill », clarification des canaux d'objections, prise en compte de `skl-001-skill-writer` et `skl-002-recherche-de-fondation`.
- **v3** : intégration des réponses de l'humain (tâche 3 de `session.md`) à mes objections :
  1. dépendance `FND-001` retirée (l'humain a directement corrigé `skl-001-skill-writer`, référence supprimée) ;
  2. les fichiers harnais sont des **livrables vivants** (pas écrits une fois) — un skill de production/évolution pour le harnais est donc justifié, contrairement à ce que j'avais proposé ;
  3. confirmation : produire `skl-003-plan-de-travail`, actuellement inexistant ;
  4. précision de nomenclature générale pour les « artefacts-de-travail » : `.dev/<type>/<TYPE_PREFIX>-<SEQ>-<SLUG>.md`, sauf exceptions à contrainte fixe (skills → convention Claude Code ; harnais → noms de fichiers fixes à la racine).
- **v4** (courante) : exécution (tâche 4 de `session.md`) — création de `CONSTITUTION.md`, `INTENTION.md`, `CLAUDE.md`, `skl-003-plan-de-travail` et `skl-004-harnais`.

---

## Intention

Écrire les fichiers de harnais (« harness files ») nécessaires — `CLAUDE.md`, `CONSTITUTION.md`, `INTENTION.md`, etc. — pour fixer une méthode de travail augmentée par IA, légère, dans laquelle toute demande adressée à l'agent est cadrée par trois ingrédients :

1. l'**intention** (le pourquoi),
2. le **contexte** (les contraintes et la façon de collaborer), et
3. la **spécification du livrable** (la forme attendue du résultat).

## Contexte

La gouvernance entre l'humain et l'agent IA suit un modèle **objection-sociocratique** :

- l'humain soumet un problème ;
- l'agent propose une intervention sous forme d'un **plan** ;
- avant toute exécution, l'humain peut émettre des **objections raisonnées** ;
- l'agent ne peut pas exécuter le plan tant que des objections restent **non résolues**.

Précisions :

- **Point d'entrée unique** : l'humain ne s'adresse à l'agent qu'à travers `.dev/session.md`.
- **Canaux d'objections séparés** : celles de l'**humain** dans `.dev/session.md`, celles de l'**agent IA** dans **le plan** (section dédiée ci-dessous).
- **Quatre types de livrables**, chacun encadré par un **skill** qui en spécifie le processus de production et les critères de qualité :
  1. les **plans** (`.dev/plans/PLN-<SEQ>-<SLUG>.md`) ;
  2. les **recherches de fondation** (`.dev/fondations/FND-<SEQ>-<SLUG>.md`) ;
  3. le **harnais** (`CLAUDE.md`, `CONSTITUTION.md`, `INTENTION.md`, à la racine) — **vivant** : ces fichiers évoluent pour corriger le comportement de l'agent ou faire évoluer le concept ; ce n'est pas une écriture ponctuelle, même si leur cycle de vie est plus lent que celui des autres livrables ;
  4. les **skills** eux-mêmes (`.dev/skills/skl-<SEQ>-<nom>/SKILL.md`).
- **Nomenclature générale** : tout livrable de type « artefact-de-travail » (plans, fondations) suit `.dev/<type>/<TYPE_PREFIX>-<SEQ>-<SLUG>.md`. Exceptions à contrainte fixe : les **skills** suivent la convention Claude Code (`.dev/skills/skl-<SEQ>-<nom>/SKILL.md`) ; le **harnais** utilise des noms de fichiers fixes à la racine (pas de séquence, un fichier = un rôle).

Le travail repose sur des **documents livrables** versionnés dans le dépôt plutôt que sur des échanges éphémères en conversation.

## Spécification des livrables

| Livrable | Emplacement | Skill de production |
|---|---|---|
| Plan de travail | `.dev/plans/PLN-<SEQ>-<SLUG>.md` | `skl-003-plan-de-travail` |
| Recherche de fondation | `.dev/fondations/FND-<SEQ>-<SLUG>.md` | `skl-002-recherche-de-fondation` |
| Harnais | `CLAUDE.md`, `CONSTITUTION.md`, `INTENTION.md` | `skl-004-harnais` |
| Skill | `.dev/skills/skl-<SEQ>-<nom>/SKILL.md` | `skl-001-skill-writer` |

Ce document (`PLN-001`) respecte la convention de son propre type de livrable : `.dev/plans/PLN-001-setup-methodology.md`.

## Constat de l'état actuel du dépôt

- **Existant** : `.dev/session.md`, `.dev/plans/PLN-001-*.md` (ce document), `.dev/skills/skl-001-skill-writer/SKILL.md` (référence `FND-001` retirée), `.dev/skills/skl-002-recherche-de-fondation/SKILL.md`.
- **Absent** : `CLAUDE.md`, `CONSTITUTION.md`, `INTENTION.md`, `.dev/fondations/` (dossier), `skl-003-plan-de-travail`, `skl-004-harnais`.

---

## Plan proposé

### 1. `CONSTITUTION.md` — le processus de décision
Décrire formellement le cycle objection-sociocratique : les états d'un plan (`proposé` → `objection` → `résolu` → `approuvé` → `exécuté`), ce qui constitue une « objection raisonnée », comment une objection est levée, la règle absolue de blocage tant qu'une objection est ouverte, et la séparation des canaux d'objections (humain → `session.md`, agent → le plan).

### 2. `INTENTION.md` — le registre des intentions
Capturer l'intention globale du projet/dépôt (le « pourquoi » de haut niveau, stable dans le temps), par opposition aux intentions locales à chaque `PLN-xxx`.

### 3. `CLAUDE.md` — le mode opératoire de l'agent
Fichier de configuration lu automatiquement par l'agent : règle des 3 ingrédients, renvoi vers `CONSTITUTION.md` et `INTENTION.md`, les quatre types de livrables avec emplacements et skills associés, la nomenclature générale `.dev/<type>/<PREFIX>-<SEQ>-<SLUG>.md` et ses exceptions.

### 4. `skl-003-plan-de-travail`
Skill encadrant la production d'un plan, calqué sur le gabarit de `skl-001`/`skl-002`. Emplacement : `.dev/skills/skl-003-plan-de-travail/SKILL.md`.

### 5. `skl-004-harnais`
Skill encadrant la production **et l'évolution** des fichiers de harnais — distinct des skills précédents en ce qu'il encadre la modification d'un fichier existant (pas seulement sa création initiale) : quand amender `CLAUDE.md`/`CONSTITUTION.md`/`INTENTION.md`, comment vérifier la cohérence avec les autres harnais après une modification, critères de non-régression. Emplacement : `.dev/skills/skl-004-harnais/SKILL.md`.

### 6. Validation humaine
Ce plan reste en statut *proposition* tant qu'une objection reste ouverte (agent ou humain). Les objections de l'agent listées ci-dessous sont résolues suite aux réponses de la tâche 3. Aucune objection humaine n'est actuellement ouverte dans `session.md`. Une fois ce statut confirmé par l'humain, l'agent exécutera les étapes 1 à 5 — probablement dans cet ordre (`CONSTITUTION.md` et `INTENTION.md` avant `CLAUDE.md` puisque ce dernier y renvoie, puis les deux skills).

---

## Objections de l'agent IA

1. ~~Dépendance non résolue `FND-001`~~ — **résolu** : l'humain a retiré la référence directement dans `skl-001-skill-writer`.
2. ~~Un « harnais » a-t-il besoin d'un skill dédié ?~~ — **résolu, mon hypothèse était fausse** : le harnais est vivant, pas écrit une fois. Skill `skl-004-harnais` ajouté au plan (étape 5).
3. ~~Étape 4 (`skl-003-plan-de-travail`) est-elle dans le périmètre de PLN-001 ?~~ — **résolu, confirmé** par l'humain.

_Aucune objection ouverte actuellement._

---

## Note sur les objections humaines

Conformément à la gouvernance, les objections de l'humain sur ce plan ne sont pas consignées ici mais dans `.dev/session.md`.
