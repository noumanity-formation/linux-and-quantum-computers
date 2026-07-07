# PLN-006 — Correctifs de placement des images sur la slide de titre

**Statut : exécuté**

---

## Changelog

- **v1** : exécution immédiate (aucune objection majeure, voir étape 7). Commande `dev.sh qrcode` ajoutée, modèle `title-qr` créé, `remerciements` étendu avec `qr-image` (rétrocompatible avec `qr-url`), `render_slide.lua` résout génériquement `photo`/`qr-image`. QR unique généré dans `dist/qrcode-repo.png` (logo agrandi, ratio 0.30, correction d'erreur `-l H`), réutilisé identique sur les slides 1 et 3. `dist/presentation.pdf` régénéré et vérifié visuellement : photo/QR de même taille, centrés sous le nom, logo net, titre professionnel à jour, aucun pied de page sur les 3 slides.
- **v2** : correctif de marge de sécurité sur `title-qr` (session.md, tâche 7 + 8) — le titre n'était pas cadré dans la même marge de 1.4cm que le bloc auteur et le bloc événement/date/lieu. `title-qr.tex` corrigé (titre + auteurs regroupés dans un même bloc à 1.4cm de chaque bord, cohérent avec le reste du gabarit). Vérifié visuellement via `pdftoppm` (pas de Python, voir tâche 8).
- **v3** : la marge du haut restait cassée (session.md, tâche 9 — mesurée à **0cm** via `convert -fuzz 8% -trim info:`, ImageMagick, sans Python). Diagnostic : `title-qr.tex` gardait un `\vfill` (colle flexible) hérité de `title.tex` original, mais le contenu fixe ajouté (photo/QR 1.9cm + espacements) dépasse la hauteur de page disponible (9cm) — le `\vfill` s'écrase alors à 0 au lieu de produire une marge, et le titre touche le bord. Correctif : `\vfill` remplacés par des `\vspace{1.4cm}` fixes (haut et bas), garantissant la marge quel que soit le contenu, au lieu d'une glue qui peut s'effondrer silencieusement. Re-mesuré après correctif : marge haute 1.4cm, marge gauche 1.4cm (conforme). Marge basse du bloc événement/date/lieu ~0.2cm : comportement hérité identique à `title.tex`/`plain.tex`/`remerciements.tex` (le bloc y est ancré en absolu via tikz, pas soumis au même risque de collapse) — pas une régression, convention déjà en place partout ailleurs.
- **v4** (courante) : documentation utilisateur du CLI (session.md, tâche 9) créée dans `doc/cli/README.md` (commandes) et `doc/cli/format-contenu.md` (format `content.md`, cascade de configuration, résolution des chemins, modèles disponibles, convention de marge de sécurité).

---

## Intention

Corriger 4 points sur `dist/presentation.pdf` (session.md, tâche 6) : logo du QR trop petit/illisible, QR différent entre slide 1 et slide 3, tailles/positions de la photo et du QR sur la slide 1 non conformes, titre professionnel de l'auteur à mettre à jour.

## Contexte

- Le modèle `title` actuel ne supporte que `logos` (petites images, 1.1cm max, coin bas-droit) — pas de champ pour une photo + QR centrés, grand format, sous le bloc auteur.
- Le modèle `remerciements` génère son QR nativement en LaTeX (macro `\qrcode`) à partir de `qr-url` — ce n'est pas un fichier image, donc pas réutilisable tel quel sur la slide 1.
- `render_slide.lua` (`resolve_asset`) résout déjà n'importe quel chemin d'image générique (png, svg, webp) référencé dans `content.md` — un champ `photo`/`qr-image` de type chemin simple s'intègre sans changement de cette fonction.
- `qrencode` et `convert` (ImageMagick) sont disponibles ; aucune commande CLI dédiée n'existe encore pour générer un QR avec logo composité.

## Spécification du livrable

- Nouvelle commande `dev.sh qrcode URL OUTPUT [--logo PATH] [--ratio N]` : génère `dist/OUTPUT` (QR + logo composité, défaut `src/assets/isotipo-noumanity.png`, ratio logo par défaut agrandi).
- Nouveau modèle `title-qr` (`templates/models/title-qr.tex`/`.yaml`) : variante de `title` avec photo + QR-image (1.9cm, comme le QR de `remerciements`) centrés sous le bloc auteur, au lieu des petits logos bas-droite.
- `remerciements.tex`/`.yaml` étendu d'un champ optionnel `qr-image` (image pré-générée) prioritaire sur `qr-url` (macro native), pour permettre de réutiliser le même fichier QR sur les deux slides.
- `render_slide.lua` (`build_ctx`) étendu pour résoudre les champs génériques `photo` et `qr-image` en chemins réels (même mécanisme que `background`).
- `src/slide-01/content.md` migré vers le modèle `title-qr`, titre professionnel mis à jour, `src/slide-03/content.md` référence la même image QR que `src/slide-01`.
- `dist/presentation.pdf` régénéré et vérifié visuellement.

## Plan proposé

### 1. Ajouter la commande `dev.sh qrcode`
Génère `dist/<OUTPUT>` : QR noir (`qrencode -l H`, correction d'erreur élevée pour tolérer un logo central plus gros) + logo composité (`convert`, ratio par défaut ~0.30 de la largeur du QR, contre ~0.25 illisible constaté précédemment).

### 2. Étendre `render_slide.lua`
Résoudre `photo` et `qr-image` (champs `content:` simples, type chemin) en chemins réels via `resolve_asset`, exposés aux templates comme `photo_path` / `qr_image_path`.

### 3. Créer le modèle `title-qr`
Clone de `title.tex`/`.yaml` : remplace le bloc `logos` (bas-droite, 1.1cm) par `photo_path` + `qr_image_path` (1.9cm chacun), centrés, juste sous le bloc auteur. Conserve `event`/`date`/`location` en bas-gauche (inchangé).

### 4. Étendre `remerciements.tex`/`.yaml`
Ajouter le champ optionnel `qr-image` : si présent, affiche l'image (1.9cm) au lieu de générer le QR nativement via `qr-url`. Comportement existant conservé si `qr-image` absent (rétrocompatibilité).

### 5. Générer le QR unique et mettre à jour les 2 slides concernées
`dev.sh qrcode "https://github.com/noumanity-formation/intentional-dooers-governance" qrcode-repo.png` → `dist/qrcode-repo.png`. `src/slide-01/content.md` : modèle `title-qr`, `photo: "@src/assets/photo-auteur.jpg"`, `qr-image: "@dist/qrcode-repo.png"`, titre professionnel mis à jour (« Stratégie & Leadership des pratiques de sécurité \| DevSecOps »). `src/slide-03/content.md` : `qr-image: "@dist/qrcode-repo.png"` (remplace `qr-url`).

### 6. Régénérer et vérifier
`dev.sh gen` → `dist/presentation.pdf`, conversion en images et inspection visuelle des 3 slides (tailles identiques photo/QR, logo lisible, pas de pied de page, titre à jour).

### 7. Exécution immédiate si aucune objection majeure
Comme pour `PLN-005`, conformément à la consigne explicite de `session.md` (tâche 6).

---

## Objections de l'agent IA

1. **Portée dépasse « correctifs mineurs »** : ce plan modifie le moteur de rendu (`render_slide.lua`) et ajoute un modèle + une commande CLI — plus qu'un simple ajustement de contenu. Risque : si un bug est introduit dans `render_slide.lua`, ça casse potentiellement toutes les slides existantes (`plain`, `remerciements`), pas seulement la slide 1. Mitigation : les nouveaux champs (`photo`, `qr-image`) sont additifs (valeur par défaut `""`, ignorés si absents) — aucun changement de comportement pour les slides qui ne les utilisent pas ; à vérifier à l'étape 6 sur les 3 slides, pas seulement la 1.
2. **Taille du logo dans le QR (ratio 0.30)** est une estimation, pas garantie lisible/scannable pour autant — un logo trop gros dégrade la capacité de correction d'erreur du QR au-delà du seuil `-l H` (~30%). Non bloquant : vérifié visuellement à l'étape 6, ajustable via `--ratio` si besoin.

_Aucune objection majeure : exécution immédiate (voir étape 7)._

---

## Note sur les objections humaines

Les objections de l'humain sur ce plan ne sont pas consignées ici mais dans `.dev/session.md`.
