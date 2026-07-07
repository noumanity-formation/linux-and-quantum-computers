---
name: skl-007-script-pdf-presentation
description: >-
  Encadrer l'écriture et l'évolution du CLI bash qui génère le pdf de présentation de ce dépôt
  (`scripts/dev.sh` et son moteur Lua/LuaLaTeX), informé par `ADR-001-cli-generation-pdf-presentation.md`.
  À utiliser quand une modification du CLI de génération de pdf est demandée (nouvelle commande,
  correctif de robustesse, évolution du moteur de rendu).
---

# Skill - Script bash de génération du pdf de présentation

> Le CLI `scripts/dev.sh` orchestre la génération du pdf de présentation de ce dépôt (Beamer/LuaLaTeX/Lua, décision actée dans `ADR-001-cli-generation-pdf-presentation.md`). Ce skill encadre son évolution — pas son remplacement de stack, qui exige un nouvel ADR.

## Quand l'utiliser

Quand une tâche demande de modifier `scripts/dev.sh` ou un composant de son moteur de rendu (scripts Lua, templates `.tex`/`.yaml`) dans ce dépôt : ajout de commande, correctif de robustesse, évolution mineure. Ne pas utiliser pour changer de stack de rendu (LuaLaTeX/Beamer → autre chose) sans passer d'abord par `skl-006-adr` pour amender ou remplacer `ADR-001`. Ne pas utiliser non plus pour une refonte d'architecture ou d'interface CLI de grande ampleur : ce type d'intervention se propose via un plan dédié (voir `PLN-004`), pas directement dans ce skill.

## Processus

1. Consulter `ADR-001-cli-generation-pdf-presentation.md` avant toute modification : la stack (Beamer/LuaLaTeX/Lua) et l'emplacement in-repo y sont actés — ne pas les remettre en cause sans un nouvel ADR.
2. Respecter les conventions déjà en place dans `dev.sh` : mode strict (`set -euo pipefail`), préfixe `[ERREUR] ...` sur stderr + code de sortie non nul en cas d'échec, préfixe `[OK] ...` en cas de succès.
3. Toute nouvelle commande suit le patron dispatcher existant (`case "${1:-}" in ...)`) et documente son usage dans le bloc de commentaires d'en-tête du script — source unique du `--help` (généré par `grep '^#'`).
4. Séparer strictement `workdir/` (temporaire, régénérable, ignoré par git) de `dist/` (sortie finale, livrable versionné).
5. Pour une amélioration de robustesse à faible impact (validation d'argument, message d'erreur plus clair, alias `-h`), vérifier qu'elle ne change pas le comportement observable en usage normal.
6. Pour toute intervention dépassant l'amélioration mineure (refonte de l'interface, changement d'architecture applicative), ne pas l'exécuter directement : la documenter comme proposition dans un plan dédié.

## Critères de qualité

- Toute commande a une entrée dans le commentaire d'en-tête ET est gérée dans le dispatcher — les deux ne divergent jamais.
- `set -euo pipefail` préservé ; aucune erreur silencieuse (pas de `|| true` sans commentaire justifiant pourquoi l'échec est acceptable).
- `workdir/` et `dist/` ne sont jamais mélangés (un fichier temporaire ne finit pas dans `dist/`, un livrable final ne reste pas seulement dans `workdir/`).
- Aucun changement de stack de rendu sans ADR amendé ou nouvel ADR.
- Le script reste exécutable par simple `bash scripts/dev.sh` après `. activate` — pas de dépendance implicite non documentée dans `ADR-001` ou dans le commentaire d'en-tête.

## Structure du livrable

- **Emplacement** : `scripts/dev.sh` (+ `scripts/*.lua`, `scripts/lib/`, `templates/`, `activate`) à la racine de ce dépôt.

Patron d'ajout d'une commande dans le dispatcher :

```bash
# 1. Ajouter une ligne au bloc de commentaires d'en-tête (source du --help) :
#   dev.sh <commande> [options]        - <description courte>

# 2. Ajouter la fonction dédiée :
ma_commande() {
    local arg="${1:-}"
    if [ -z "$arg" ]; then
        echo "[ERREUR] Usage : dev.sh ma_commande ARG" >&2
        exit 1
    fi
    # ... logique ...
    echo "[OK] ma_commande terminee"
}

# 3. Brancher dans le dispatch principal :
case "${1:-}" in
    gen)         shift; gen "$@" ;;
    clean)       clean ;;
    model)       shift; model_cmd "$@" ;;
    diapo)       shift; diapo_cmd "$@" ;;
    ma_commande) shift; ma_commande "$@" ;;
    --help)      usage ;;
    "")          usage ;;
    *)           echo "[ERREUR] Commande inconnue : $1" >&2; usage ;;
esac
```
