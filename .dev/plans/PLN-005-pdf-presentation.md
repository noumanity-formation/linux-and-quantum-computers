# PLN-005 — Préparation du pdf support à la présentation

**Statut : exécuté**

---

## Changelog

- **v1** : exécution immédiate (aucune objection majeure, voir étape 6). `dist/presentation.pdf` généré (3 pages), vérifié visuellement par conversion en images. Aucun pied de page sur aucune slide. QR slide 3 (1.9cm, généré nativement par LaTeX) net et lisible. QR slide 1 (généré via `qrencode`+`convert`, logo isotipo composé au centre) visible mais très petit (1.1cm, limite du template) — objection 1 confirmée, à surveiller en salle. Limitation découverte à l'exécution, non anticipée dans le plan : l'emoji 🐧 dans « Organisé par 🐧Martial Bigras » ne s'affiche pas (LuaLaTeX/police du thème sans glyphes emoji) — le texte reste correct sans l'emoji.

---

## Intention

Produire `dist/presentation.pdf`, le support visuel d'un atelier pratique de 5 minutes sur le mécanisme de l'objection-sociocratique, présenté ce soir aux Rencontres Linux du Québec (session.md, tâche 5). Contrainte : temps quasi écoulé, exécution immédiate attendue si aucune objection majeure.

## Contexte

- Le CLI porté (`PLN-002`) est fonctionnel : 3 diapos suffisent, modèles disponibles `title`, `plain`, `remerciements` couvrent exactement les 3 slides demandées.
- Aucune slide ne doit avoir de pied de page : le champ optionnel `section` du modèle `plain` est la seule source de pied de page (`templates/models/plain.tex`, l.9-15) — ne pas le renseigner suffit, aucune modification de thème requise.
- Le modèle `remerciements` génère nativement un QR code depuis une URL (`qr-url` → `\qrcode{...}` en LaTeX, `templates/models/remerciements.tex`) — couvre directement la slide 3.
- Le modèle `title` n'a **pas** de champ QR dédié, seulement `logos` (liste de chemins d'image, bas-droite, hauteur max 1.1cm) et `background`. Pour la slide 1 (photo auteur + QR aux couleurs noumanity), il faut donc **générer les images en amont** (QR noir avec logo isotipo noumanity au centre via `qrencode`+`convert`, et récupérer la photo auteur) puis les passer via `logos`.
- Assets distants vérifiés accessibles (HTTP 200) : logo isotipo noumanity (`raw.githubusercontent.com/noumanity/imagen/.../isotipo%20noumanity-color.png`) et photo de l'auteur (URL LinkedIn déjà utilisée dans `README.md`).
- URL du dépôt pour le QR de la slide 1 (`https://github.com/noumanity-formation/intentional-dooers-governance`) vérifiée identique au remote `origin` du dépôt (`git remote -v`) — pas une faute de frappe, confirmé correct tel quel.
- `qrencode` et `convert` (ImageMagick) sont disponibles dans l'environnement.

## Spécification du livrable

- 3 fichiers `src/slide-01/content.md`, `src/slide-02/content.md`, `src/slide-03/content.md` (modèles `title`, `plain`, `remerciements`).
- Assets générés dans `src/assets/` : photo auteur, QR slide 1 (composite noir + logo isotipo), QR slide 3 (généré nativement par LaTeX, pas d'asset à produire).
- `dist/presentation.pdf`, produit par `scripts/dev.sh gen`.

## Plan proposé

### 1. Générer les assets image de la slide 1
Télécharger la photo auteur et le logo isotipo noumanity dans `src/assets/`. Générer un QR noir (`qrencode`) pointant vers `https://github.com/noumanity-formation/intentional-dooers-governance`, puis composer le logo isotipo au centre (`convert`).

### 2. Rédiger `src/slide-01/content.md` (modèle `title`)
Titre de la présentation, auteur (Jérémy Viau-Trudel, Spécialiste DevSecOps), date/événement/lieu, mention « Organisé par 🐧Martial Bigras » (pas de champ dédié dans le modèle `title` — ajoutée en fin du champ `location`, seule extension possible sans toucher au template). `logos` : photo auteur + QR composite.

### 3. Rédiger `src/slide-02/content.md` (modèle `plain`)
Contenu : proposition de renommer RLQ en ReLaQx pour éviter la confusion avec l'acronyme de la Réseau des Lesbiennes du Québec. Champ `section` volontairement omis (pas de pied de page).

### 4. Rédiger `src/slide-03/content.md` (modèle `remerciements`)
`message`, `focus` (« Questions? »), `qr-url` pour le matériel supplémentaire (URL du dépôt, même cible que slide 1 sauf indication contraire).

### 5. Générer le pdf
`scripts/dev.sh gen` (ou `--prod`) → `dist/presentation.pdf`. Vérifier visuellement l'absence de pied de page et le rendu des 3 slides.

### 6. Exécution immédiate si aucune objection majeure
Conformément à la consigne explicite de `session.md` (tâche 5), ce plan est exécuté dès sa rédaction si les objections ci-dessous ne sont pas majeures — pas de cycle d'approbation séparé, vu la contrainte de temps.

---

## Objections de l'agent IA

1. **QR de la slide 1 illisible à l'échelle du template** : le seul emplacement disponible pour les `logos` (photo + QR) fait 1.1cm de hauteur maximum — un QR à cette taille, projeté en salle, risque de ne pas scanner correctement avec un téléphone à distance. Ce n'est pas une modification de template pour corriger cela avant la présentation vu le temps disponible. **Non bloquant** : appliqué tel quel, à valider visuellement à l'étape 5 ; solution de repli si illisible = agrandir le QR de la slide 3 (remerciements, déjà en 1.9cm) et y répéter le lien du dépôt.
2. **Mention « Organisé par » sans champ dédié** : ajoutée en texte libre à la fin du champ `location` du modèle `title`, faute de champ prévu à cet effet — décision d'implémentation, pas un risque de contenu incorrect.

_Aucune objection majeure : exécution immédiate (voir étape 6)._

---

## Note sur les objections humaines

Les objections de l'humain sur ce plan ne sont pas consignées ici mais dans `.dev/session.md`.
