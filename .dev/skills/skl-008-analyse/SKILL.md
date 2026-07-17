---
name: skl-008-analyse
description: >-
  Produire une analyse critique d'un artefact existant (README, plan, fondation, code,
  document externe) déposée dans `.dev/analyses/ANL-<SEQ>-<SLUG>.md`. À utiliser quand une
  tâche demande de vérifier, réviser ou critiquer un livrable sans le modifier, le résultat
  attendu étant un diagnostic écrit et non une correction.
---

# Skill - Production d'une analyse critique

> Une analyse est un livrable de diagnostic : elle constate, hiérarchise et recommande, mais ne modifie pas l'artefact analysé. La correction, si elle est demandée ensuite, relève du skill du type de l'artefact concerné (ex. `skl-005-readme-presentation` pour un README).

## Quand l'utiliser

Quand une tâche demande de « vérifier », « réviser », « critiquer » ou « faire une analyse » d'un artefact existant, et que le livrable attendu est un constat écrit. Ne pas l'utiliser pour appliquer directement des corrections (utiliser alors le skill du type visé), ni pour une décision de gouvernance (`skl-006-adr`).

## Processus

1. Identifier l'artefact analysé et l'intention derrière la demande (objectif de la présentation ou du dépôt, audience visée) via la règle des 3 ingrédients (voir `CLAUDE.md`).
2. Lire l'artefact et les artefacts de contexte pertinents (`INTENTION.md`, `session.md`, artefacts liés) pour confronter le contenu à son intention déclarée.
3. Distinguer les niveaux de constat : erreurs bloquantes, incohérences de fond, fautes de langue, ton et cohérence éditoriale.
4. Hiérarchiser par priorité d'action, en tenant compte des contraintes de délai consignées dans `session.md`.
5. Terminer par des recommandations actionnables et, si pertinent, les questions ouvertes à trancher par l'humain avant toute correction.

## Critères de qualité

- Chaque constat pointe un emplacement précis (numéro de ligne ou section) et est vérifiable.
- Les constats sont hiérarchisés (bloquant, fond, forme) et non un simple relevé en vrac.
- L'analyse reste un diagnostic : aucune modification de l'artefact analysé n'est appliquée sous ce skill.
- Les recommandations sont actionnables et rattachées à l'intention et à l'audience.
- Markdown strict (voir `CLAUDE.md`).

## Structure du livrable

- **Emplacement** : `.dev/analyses/ANL-<SEQ>-<SLUG>.md`.
- **En-tête** : titre `# ANL-<SEQ> : <objet de l'analyse>`, puis une ligne de métadonnées (date, artefact analysé, source de la demande).
- **Corps** : sections par niveau de constat, puis une section de priorités et une section des questions ouvertes le cas échéant.
