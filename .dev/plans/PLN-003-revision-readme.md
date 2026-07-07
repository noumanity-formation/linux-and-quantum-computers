# PLN-003 — Révision rapide du README de présentation

**Statut : exécuté**

---

## Changelog

- **v1** : exécution suite à l'approbation express de l'humain (« oui, tout est ok. GO! ») — les deux affirmations factuelles (l.27, l.31) sont confirmées exactes telles quelles. Corrections appliquées : nom de l'ÉTS, « vous chercher à » → « vous cherchez à », « atteimdre » → « atteindre », « ascerbe » → « acerbes » (accord), « technicalité » → « aspects techniques », « et une un Studio DeepTech » → « est un Studio DeepTech », « bootstraped » → « bootstrappé », « !00% » → « 100% » (×2), « connaisances » → « connaissances », « technologie » → « technologies » (accord), « rendues disponible » → « rendues disponibles » (accord).

---

## Intention

Réviser rapidement le `README.md` déjà rédigé par l'humain pour la présentation du 2026-07-07, qui a lieu dans moins d'une heure (session.md, tâche 4). Objectif : aucune inexactitude factuelle, aucune faute d'orthographe/grammaire, un texte qui sert l'objectif de communication (faire reconnaître la compétence de l'auteur en organisation de projets open source) pour l'audience visée (acteurs du milieu open source du Québec).

## Contexte

- Le `README.md` actuel (44 lignes, racine du dépôt) a déjà été rédigé par l'humain — conforme au recadrage de la tâche 2 (« un humain rédige, l'agent vérifie ») et suit déjà globalement le patron de `skl-005-readme-presentation` (titre, résumé, section auteur, section « Financé par noumanity » qui joue le rôle de fiche entreprise).
- **Contrainte de temps sévère** : présentation dans moins d'une heure.
- Relecture rapide déjà effectuée par l'agent en préparant ce plan (aucune correction appliquée à ce stade) :
  - fautes probables repérées : « atteimdre » (l.11), « vous chercher à » (accord verbal, l.11), « ascerbe » (l.15), « technicalité » (calque de l'anglais, l.15), « et une un Studio DeepTech » (l.31), « bootstraped » (anglicisme non francisé, l.31), « !00% » (l.39), « connaisances » (l.39), « technologie !00% libres » (accord pluriel manquant, l.39), « rendues disponible » (accord manquant, l.39), « École de Technologies Supérieur de Montréal » (nom de l'établissement mal orthographié : le nom exact est « École de technologie supérieure », l.3).
  - affirmations factuelles à faire confirmer par l'humain, non vérifiables par l'agent seul : noumanity « le premier [studio DeepTech] dans la ville de Québec et probablement le seul bootstrapé/auto-financé au Canada » (l.31) ; « 26 ans et 10 mois de recherche-action » (l.27).

## Spécification du livrable

`README.md` corrigé à la racine du dépôt (édition sur place, pas de nouveau fichier), conforme à `skl-005-readme-presentation` en mode **vérification**.

## Plan proposé

### 1. Relecture orthographique et grammaticale complète
Ligne par ligne, lister chaque correction avant de l'appliquer — pas de réécriture silencieuse de contenu au-delà des fautes pures.

### 2. Vérification des affirmations factuelles
Corriger directement ce qui est vérifiable de façon univoque (ex. nom exact de l'ÉTS). Signaler à l'humain, sans les modifier, les affirmations que l'agent ne peut pas vérifier seul (chiffres et claims propres à noumanity/l'auteur).

### 3. Vérifier la conformité structurelle au patron `skl-005`
Confirmer qu'aucune section obligatoire (titre, résumé, auteur, fiche entreprise) n'est manquante — déjà globalement le cas.

### 4. Appliquer les corrections non ambiguës
Fautes d'orthographe/grammaire pures : correction directe. Points nécessitant un arbitrage (exactitude d'un chiffre, ton/emojis) : signalés, non modifiés d'autorité.

### 5. Validation humaine express
Étant donné la contrainte de temps, une confirmation courte dans `.dev/session.md` (ex. « go », comme pour `PLN-002` tâche 3) suffit à déclencher l'exécution immédiate.

---

## Objections de l'agent IA

1. **Tension entre le cycle d'objection complet et la fenêtre de temps restante (moins d'une heure)** : si ce plan suit le cycle standard sans réponse rapide de l'humain, risque concret que la révision ne soit pas terminée avant le début de la présentation. Mitigation proposée : approbation express (étape 5) plutôt que le cycle complet.
2. **Deux affirmations factuelles non vérifiables par l'agent** (l.27, l.31) : si elles sont fausses et que l'agent les laisse telles quelles faute de confirmation humaine à temps, le README publié contiendra une inexactitude malgré l'exigence explicite « aucune inexactitude ». L'agent ne les corrigera pas d'autorité sans réponse humaine.

---

## Note sur les objections humaines

Les objections de l'humain sur ce plan ne sont pas consignées ici mais dans `.dev/session.md`.
