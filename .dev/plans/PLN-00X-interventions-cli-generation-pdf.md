# PLN-004 — Interventions sur le CLI de génération du pdf de présentation

**Statut : proposé**

---

## Changelog

- **v1** : proposition initiale sous le nom `PLN-003` (tâche 3 de `session.md`, exécution de `PLN-002` étape 9).
- **v2** (courante) : renumérotée `PLN-004` (tâche 4 de `session.md`) — le numéro `PLN-003` est libéré pour un plan plus urgent (révision du README avant la présentation, dans l'heure). Contenu inchangé, seule la numérotation et les références croisées sont mises à jour.

---

## Intention

Adresser les constats de cohérence d'interface CLI et d'architecture applicative identifiés lors du portage du CLI de génération de pdf (`PLN-002`, étape 5/8), volontairement laissés de côté à ce stade pour respecter la consigne « pas de gros refactoring » (session.md, tâche 2, point 2). Ce plan est **proposé, pas exécuté** — il doit suivre le cycle objection-sociocratique complet avant toute intervention.

## Contexte

Constats issus de l'analyse du CLI (`scripts/dev.sh` + moteur Lua, porté dans ce dépôt sous `ADR-001-cli-generation-pdf-presentation.md`) et d'un test de fumée effectué pendant le portage (génération réelle d'un pdf de test, réussie) :

**Cohérence de l'interface CLI au regard des pratiques standards de l'industrie**
- Alias court `-h` pour `--help` : **déjà corrigé** pendant le portage (amélioration mineure à faible impact).
- `usage()` (`grep '^#' "$0"`) imprime **tous** les commentaires `#` du fichier, pas seulement le bloc d'en-tête : confirmé empiriquement, la sortie de `--help` inclut des fragments de commentaires internes (« Commandes model », « Emet les champs requis... ») sans rapport avec l'usage.
- Pas de `--version`.
- Codes de sortie non différenciés : toute erreur sort avec `exit 1`, aucune convention type sysexits (erreur d'usage vs échec d'exécution).
- Pas de complétion bash.
- Style mixte verbe-first (`gen`, `clean`) / nom-first (`model ls`, `diapo init`) : pattern courant dans l'industrie (git, docker font pareil) — à documenter comme un choix assumé plutôt qu'un défaut à corriger.

**Architecture applicative actuelle**
- Dispatcher plat dans un unique fichier de ~310 lignes : approprié à la taille actuelle (6 commandes), ne passera pas à l'échelle sans découpage si le nombre de commandes croît significativement.
- Communication bash → Lua pour la pré-passe de numérotation des diapos via parsing de sortie TSV (`compute_numbering.lua`) : aucune validation de schéma, un format de sortie inattendu casserait silencieusement l'association `_sec_nums`/`_slide_nums`.
- Résolution de `config.yaml`/`global-params.yaml` : **déjà corrigée** pendant le portage (déplacée dans `gen()`, ne s'exécute plus pour les commandes qui n'en ont pas besoin).
- `clean()` ne couvre pas tous les artefacts produits par `gen()` : confirmé empiriquement, `workdir/*.sty` (copié depuis `templates/theme/`) et `workdir/theme.generated.tex` (généré par `theme_helper.lua`) subsistent après `dev.sh clean`.
- Aucun test automatisé (unitaire ou d'intégration) sur le CLI bash ni sur les scripts Lua ; la seule vérification à ce jour est le test de fumée manuel de `PLN-002`.
- `assets/branding/` (logos, polices, manuel de marque) du dépôt source **n'a pas été porté** dans ce dépôt (hors périmètre du portage minimal). Le test de fumée a réussi avec les polices ABeeZee/Arimo déjà présentes sur ce poste, sans garantie que ce soit le cas sur un autre poste ou en CI.

## Spécification du livrable

Ce plan-ci ne produit aucun livrable applicatif directement — il propose des interventions sur `scripts/dev.sh` (et éventuellement le moteur Lua) déjà porté dans ce dépôt sous `skl-007-script-pdf-presentation`. Toute intervention retenue sera exécutée en respectant ce skill et, si elle touche au choix de stack, `ADR-001-cli-generation-pdf-presentation.md`.

## Plan proposé

### 1. Corriger `usage()` pour n'imprimer que le bloc d'en-tête
Limiter `grep '^#'` au bloc de commentaires contigu en tête de fichier (ex. s'arrêter à la première ligne non-`#`), pas à tous les `#` du fichier.

### 2. Compléter `clean()`
Ajouter `workdir/*.sty` et `workdir/theme.generated.tex` à la liste des artefacts supprimés, pour que `clean` couvre réellement tout ce que `gen` produit dans `workdir/`.

### 3. Ajouter `--version`
Définir une source de vérité pour la version du CLI (constante dans le script, ou dérivée d'un tag/commit git) et l'exposer via `dev.sh --version`.

### 4. Décider du sort de `assets/branding/`
Trancher : porter les assets de marque (logos, polices, manuel) pour un rendu garanti indépendant des polices déjà présentes par coïncidence sur ce poste, ou documenter explicitement la dépendance aux polices système (ABeeZee, Arimo) comme prérequis d'environnement. Décision humaine requise (voir objection 2).

### 5. Évaluer l'introduction de tests automatisés
Au minimum, un test de fumée scriptable (init d'une diapo `title`, `gen`, vérification qu'un pdf valide est produit, nettoyage) rejouable en CI ou en local, pour fiabiliser les évolutions futures du CLI.

### 6. Fiabiliser l'échange bash ↔ Lua pour la numérotation
Ajouter une validation minimale du format TSV produit par `compute_numbering.lua` avant de peupler `_sec_nums`/`_slide_nums`, pour échouer explicitement plutôt que silencieusement en cas de sortie inattendue.

### 7. Validation humaine
Ce plan reste en statut *proposé*. Aucune intervention ci-dessus n'est exécutée tant que les objections ne sont pas résolues dans `.dev/session.md`.

---

## Objections de l'agent IA

1. **Risque de régression en pleine fenêtre d'usage** : la présentation associée à ce CLI a lieu le jour même de sa mise en place (`ADR-001-cli-generation-pdf-presentation.md`). Si les six interventions sont traitées comme un bloc unique sans priorisation, une régression sur un point structurant (ex. 5 ou 6) risque de rendre le CLI indisponible juste avant l'échéance. Proposition : prioriser 1-2-3 (correctifs locaux, risque de régression faible) avant 4-5-6 (plus structurants) si ce plan est exécuté avant la présentation.
2. **Décision non tranchée sur `assets/branding/`** (étape 4) : porter les assets de marque est un chantier non trivial (fichiers binaires, polices, manuel de marque) dont l'ampleur dépend d'un arbitrage humain (rendu de marque garanti vs dépendance documentée aux polices système). Ce plan ne tranche pas seul cette question.

---

## Note sur les objections humaines

Les objections de l'humain sur ce plan ne sont pas consignées ici mais dans `.dev/session.md`.
