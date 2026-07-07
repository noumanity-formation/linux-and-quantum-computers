# PLN-002 — Skills pour le matériel de présentation RLQ

**Statut : exécuté**

---

## Changelog

- **v1** : proposition initiale (tâche 1 de `session.md`), basée sur l'analyse en lecture seule du dépôt source. Quatre objections agent soulevées.
- **v2** : intégration des réponses de l'humain (tâche 2 de `session.md`) aux quatre objections. Ajout de deux nouveaux livrables demandés (`skl-<SEQ>-adr` et un ADR pour le CLI porté) et de la mise à jour des harnais pour les nouveaux types de livrables. Séquence d'exécution imposée par l'humain. Les quatre objections v1 sont résolues ; deux décisions d'implémentation non explicitement tranchées par l'humain sont signalées en clair (pas comme objections bloquantes) pour permettre une correction avant exécution.
- **v3** (courante) : exécution (tâche 3 de `session.md`, « exécuter le plan PLN-002 »), aucune correction reçue sur les deux décisions signalées en v2 — traitées comme acceptées tacitement. Les 9 étapes ont été exécutées dans l'ordre prévu : `skl-005-readme-presentation`, mise à jour de `CLAUDE.md`, `skl-006-adr`, analyse du CLI, `ADR-001-cli-generation-pdf-presentation.md`, `skl-007-script-pdf-presentation`, portage du CLI in-repo (avec test de fumée réussi : génération d'un pdf de test, puis nettoyage des artefacts de test), et proposition de `PLN-004` pour les interventions plus lourdes.

---

## Intention

Produire le matériel accompagnant la présentation du 2026-07-07 à la Rencontre Linux au Québec (README de présentation, pdf de présentation, rapport de recherche — voir `.dev/session.md`). Cette itération couvre les tâches 1 et 2 : s'appuyer sur le dépôt de la dernière présentation RLQ (`$HOME/git/noumanity-communication/review_impact-of-PQC-risks-on-main-Linux-distributions`) pour :

1. déduire un skill spécialisé pour les README.md de présentation (production **et** vérification) ;
2. porter dans ce dépôt, pour un usage in-repo, le CLI de génération de pdf de présentation existant — analysé mais non refactoré en profondeur ;
3. gouverner ce portage par un ADR (nouveau type de livrable) et un skill dédié au CLI, produits dans un ordre précis imposé par l'humain ;
4. mettre à jour les fichiers de harnais (`CLAUDE.md`, `CONSTITUTION.md`) pour reconnaître les nouveaux types de livrables issus de `session.md` (README de présentation, pdf de présentation, rapport de recherche) et, par cohérence directe avec la règle déjà en vigueur (« chaque type de livrable a un skill associé »), le nouveau type ADR.

## Contexte

Analyse en lecture seule du dépôt source (aucune modification apportée à ce dépôt tiers), et réponses de l'humain (tâche 2 de `session.md`) :

- **`README.md`** (39 lignes) suit un patron régulier : titre accrocheur → mention de l'événement/date → `## Résumé` (abstract narratif) → `## Auteurs` avec, par auteur, un sous-titre `### [Nom](LinkedIn) - Rôle`, une image de profil, et une bio en prose. **Aucune section « fiche entreprise » distincte** n'existe dans la source — confirmé par l'humain comme une lacune réelle à corriger : la spécification du skill doit inclure cette section. **Recadrage humain important** : ce skill n'a pas vocation à faire *rédiger* le README par l'agent — le README sera probablement écrit par un humain ; le skill doit encadrer aussi bien sa **production** que sa **vérification** par l'agent.
- Le « script bash de génération de PDF » est en réalité `scripts/dev.sh` (307 lignes, `set -euo pipefail`), un **orchestrateur CLI** qui pilote un moteur de rendu **LuaLaTeX/Beamer** (4 scripts Lua + templates `.tex`/`.yaml`). L'humain confirme : **le script est fonctionnel**, il doit être **copié dans ce dépôt pour un usage in-repo** (pas seulement un patron générique abstrait) ; **pas de gros refactoring** — seulement des améliorations mineures à faible impact sur la robustesse, plus deux analyses (cohérence de l'interface CLI vs pratiques standards de l'industrie ; architecture applicative actuelle) dont les constats plus lourds sont reportés dans un **nouveau plan PLN-004**, pas exécutés ici.
- L'humain demande d'ajouter un **skill de rédaction des ADR** et la **rédaction d'un ADR** regroupant les choix d'architecture de ce CLI, avec une séquence d'exécution imposée : *rédaction skill ADR → analyse du CLI → rédaction ADR pour le CLI → rédaction skill CLI → codage du CLI*.
- L'humain demande la mise à jour de `CLAUDE.md`/`CONSTITUTION.md` pour couvrir les nouveaux livrables listés dans `session.md` : **README de présentation, pdf de présentation, rapport de recherche**. Ces trois éléments sont les livrables *finaux* de la présentation (voir section « Livrables » de `session.md`) ; le CLI/ADR/skills sont l'outillage de gouvernance qui les produit, pas ces livrables eux-mêmes.
- **Vérification d'environnement** (nécessaire pour juger la faisabilité du portage in-repo) : dans cet environnement, `texlua` et `lualatex` sont disponibles ; `latexmk` et `luarocks` sont **absents**. `dev.sh` gère déjà l'absence de `latexmk` par un repli sur double passe `lualatex` directe — pas un problème bloquant. L'absence de `luarocks` doit être vérifiée à l'étape « analyse du CLI » (les modules Lua requis, ex. `etlua`, sont en partie vendorisés dans `scripts/lib/` côté source ; à confirmer pour les autres, ex. `lunamark`).
- Le dépôt source a sa propre gouvernance (ADR + tickets) et ses propres skills ; aucun ne couvre un skill « README de présentation » ni « script bash de génération PDF » — pas de risque de duplication directe.
- Ce dépôt (`intentional-doers-governance`) ne définit actuellement, dans `CLAUDE.md`, que quatre types de livrables (plan, fondation, harnais, skill). Ni **ADR**, ni **CLI/script**, ni les trois livrables finaux (README/pdf de présentation, rapport de recherche) n'y figurent.

## Spécification du livrable

- **`skl-005-readme-presentation`** (`.dev/skills/skl-005-readme-presentation/SKILL.md`, suivant `skl-001-skill-writer`) : encadre la **production et la vérification** d'un README de présentation, patron dérivé de la source (titre, résumé, auteurs) **augmenté** d'une section « fiche entreprise » (absente de la source, ajoutée sur confirmation humaine).
- **`skl-006-adr`** (`.dev/skills/skl-006-adr/SKILL.md`) : encadre la rédaction d'un Architecture Decision Record, nouveau type de livrable.
- **`ADR-001-<slug>`** (`.dev/adr/ADR-001-<slug>.md`) : regroupe les choix d'architecture du CLI porté dans ce dépôt (stack, dépendances, conventions in-repo), produit avec `skl-006-adr`.
- **`skl-007-script-pdf-presentation`** (`.dev/skills/skl-007-script-pdf-presentation/SKILL.md`) : encadre l'écriture/l'évolution du script bash d'orchestration pour ce dépôt, informé par l'ADR-001 — la stack LuaLaTeX/Beamer y est donc documentée comme un **choix explicite de ce dépôt**, pas silencieusement figée.
- Le **CLI porté** : `scripts/dev.sh` + moteur Lua (`compute_numbering.lua`, `render_slide.lua`, `model_helper.lua`, `theme_helper.lua`, `lib/etlua.lua`) + `templates/` + `activate`, copiés à la racine de ce dépôt (miroir de la convention source — voir plan, étape 1), avec améliorations mineures de robustesse seulement.
- **`PLN-004`** (`.dev/plans/PLN-004-<slug>.md`) : plan d'intervention proposé (pas exécuté dans ce plan-ci), basé sur les constats de l'analyse de cohérence CLI et d'architecture applicative.
- Mise à jour de `CLAUDE.md` et `CONSTITUTION.md` (via `skl-004-harnais`) : ajout au tableau des livrables de README de présentation, pdf de présentation, rapport de recherche, et ADR.

## Plan proposé

Ordre imposé par l'humain pour le volet CLI/ADR : *rédaction skill ADR → analyse du CLI → rédaction ADR pour le CLI → rédaction skill CLI → codage du CLI*. Les autres étapes (emplacement, `skl-005`, mise à jour des harnais) sont indépendantes de cette chaîne et placées avant elle.

### 1. Décider l'emplacement du CLI dans ce dépôt (décision d'implémentation, non tranchée explicitement par l'humain — signalée ici, pas en objection)
Miroir de la convention du dépôt source, à la racine de `intentional-doers-governance` : `scripts/`, `templates/`, `activate`, `src/` (contenu des diapos), `config.yaml`, `dist/` et `workdir/` (à ajouter au `.gitignore`). `.dev/` reste réservé aux livrables de gouvernance (plans, fondations, skills, ADR) — le CLI n'y va pas, ce n'est pas un livrable-document.

### 2. Produire `skl-005-readme-presentation` — skill README de présentation
Dériver le patron générique observé (titre, résumé, section auteurs avec bio), **ajouter** une section « fiche entreprise » (confirmée manquante à l'étape 1 par l'humain), et encadrer explicitement les deux usages : **production** (si l'agent rédige) et **vérification** (cas probable : un humain rédige, l'agent vérifie contre le patron). Exclure tout contenu spécifique à la source (URLs d'images, bios nominatives, sujet PQC).

### 3. Mettre à jour `CLAUDE.md` et `CONSTITUTION.md` (via `skl-004-harnais`)
Ajouter au tableau des livrables : README de présentation, pdf de présentation, rapport de recherche (demandés explicitement par l'humain), et **ADR** (conséquence directe de l'étape 4 — sans entrée de table, `skl-006-adr` violerait la règle déjà en vigueur dans `CLAUDE.md` : « chaque type de livrable a un skill associé »). Nomenclature ADR proposée, alignée sur la convention artefact-de-travail existante : `.dev/adr/ADR-<SEQ>-<SLUG>.md`.

### 4. Produire `skl-006-adr` — skill de rédaction des ADR
Premier maillon de la chaîne imposée par l'humain. Gabarit et processus de production d'un ADR, réutilisable au-delà du CLI présent.

### 5. Analyse du CLI
Analyse (déjà largement réalisée en amont de ce plan, à consolider) du code de `scripts/dev.sh` et du moteur Lua/LaTeX : dépendances système (vérifiées dans cet environnement : `texlua`/`lualatex` présents, `latexmk`/`luarocks` absents — à documenter), cohérence de l'interface CLI (sous-commandes, options) au regard des pratiques standards de l'industrie, architecture applicative actuelle (couplages, responsabilités). Ces constats alimentent à la fois l'ADR (étape 6) et la proposition PLN-004 (étape 9).

### 6. Rédaction de l'ADR pour le CLI
Avec `skl-006-adr` et les constats de l'étape 5 : regrouper les choix d'architecture du CLI tel que porté dans ce dépôt (stack LuaLaTeX/Beamer/Lua reprise du dépôt source, dépendances système, emplacement in-repo décidé à l'étape 1).

### 7. Produire `skl-007-script-pdf-presentation` — skill script bash de génération pdf
Informé par l'ADR-001 (étape 6) : encadrer l'écriture/l'évolution du script d'orchestration bash pour ce dépôt (mode strict, parsing d'arguments, `--help` généré, gestion d'erreurs, séparation `workdir/`/`dist/`), stack documentée explicitement comme un choix de ce dépôt, pas une évidence générale.

### 8. Codage du CLI
Copier le script et le moteur Lua/LaTeX dans ce dépôt (emplacement de l'étape 1), adapter les chemins/conventions in-repo, appliquer **uniquement** les améliorations mineures à faible impact sur la robustesse identifiées à l'étape 5 — pas de refactoring en profondeur.

### 9. Proposer `PLN-004`
Nouveau plan (non exécuté ici) portant les interventions plus lourdes suggérées par l'analyse de cohérence CLI et d'architecture applicative de l'étape 5.

### 10. Validation humaine
Ce plan passe au statut *résolu* : les quatre objections agent v1 sont résolues par les réponses de la tâche 2. Deux décisions d'implémentation (étape 1 : emplacement du CLI ; étape 3 : ajout d'ADR au tableau des livrables) ont été prises par l'agent par cohérence directe avec les règles déjà en vigueur — signalées ici pour correction avant exécution plutôt que bloquées en objection, faute de risque concret identifié. Le passage à *approuvé* et l'exécution attendent une confirmation explicite de l'humain dans `.dev/session.md`.

---

## Objections de l'agent IA

1. ~~Lacune du patron source pour la « fiche entreprise »~~ — **résolu** : confirmé par l'humain (tâche 2, point 1), section ajoutée à la spécification de `skl-005`, skill recadré production+vérification.
2. ~~Ambiguïté de portée sur le script~~ — **résolu** : l'humain tranche (tâche 2, point 2) pour un portage complet in-repo, sans gros refactoring, avec analyses reportées vers `PLN-004`.
3. ~~Sur-figement technologique dans le skill~~ — **résolu** : l'humain choisit explicitement de documenter ce figement via un ADR dédié (tâche 2, point 3) avant de rédiger `skl-007-script-pdf-presentation`, ce qui rend le choix de stack traçable plutôt que silencieux.
4. ~~Absence de convention pour un livrable « script » dans ce dépôt~~ — **résolu** : le CLI n'est pas traité comme un livrable-document gouverné (voir étape 1) ; les livrables-documents qui l'entourent (ADR, skills) sont, eux, ajoutés à `CLAUDE.md`/`CONSTITUTION.md` (tâche 2, point 4, étendu à ADR par cohérence directe).

_Aucune objection ouverte actuellement._

---

## Note sur les objections humaines

Les objections de l'humain sur ce plan ne sont pas consignées ici mais dans `.dev/session.md`.
