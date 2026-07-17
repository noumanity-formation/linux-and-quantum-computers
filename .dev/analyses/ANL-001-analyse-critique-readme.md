# ANL-001 : Analyse critique du README de présentation

- **Date** : 2026-07-17
- **Artefact analysé** : `README.md` (racine du dépôt)
- **Source de la demande** : `.dev/session.md`, tâche 1 (« révision de l'abstract »)
- **Nature** : diagnostic, sans modification de l'artefact (voir `skl-008-analyse`)

## A. Erreurs bloquantes à corriger avant diffusion

1. **Ligne 21, trou dans le texte** : `infrastructure ()`, parenthèses vides, contenu manquant. À compléter ou supprimer.
2. **Section André Gerges vide (l. 26 à 28)** : photo et titre présents, mais aucune bio, alors que Jérémy en a une complète. Asymétrie visible.
3. **Incohérence sur le co-présentateur** : `session.md` (CONTEXTE) annonce **Chrytian Guy** présentant *X-Minds : neuroatypique de haut niveau*. Le README liste **André Gerges**. Il faut trancher qui présente réellement, et le README ne mentionne pas du tout X-Minds.

## B. Incohérences de fond

4. **Titre flottant** : `session.md` dit « ordinateurs **numériques** », alors que `README.md`, `INTENTION.md` et le nom du dépôt disent « ordinateurs **quantiques** ». À aligner (« quantiques » semble le bon).
5. **Confusion de catégories dans le résumé (l. 7)** : opposer « le quantique rendra Linux obsolète » compare un paradigme matériel à un OS. Or les calculateurs quantiques actuels s'appuient sur un contrôle classique tournant souvent sous Linux, ce qui est probablement l'angle de la conférence. En l'état, l'abstract pose une fausse dichotomie susceptible d'être relevée par l'audience quantique de Sherbrooke (public secondaire ciblé).
6. **Bio vs positionnement « expert quantique »** (objectif de `session.md`) : la bio étaye une expertise en physique quantique fondamentale (équation de Schrödinger dépendante du temps, interaction laser-molécules), solide, mais pas en informatique quantique. Le pivot vers DevSecOps/Linux depuis 2016 sert l'audience Linux, mais le lien avec le sujet « ordinateurs quantiques » reste implicite.
7. **« 26 ans et 10 mois de recherche-action » (l. 23)** : précision inhabituelle, en Théorie des organisations, déconnectée du reste de la bio (physique puis TI) et du sujet quantique. Risque de paraître gonflé ou hors sujet plutôt que crédibilisant.

## C. Fautes de langue et orthographe

- `Schrodinger` vers **Schrödinger** (nom propre, tréma), l. 19.
- `computationelle` vers **computationnelle**, l. 19.
- `oganisations` vers **organisations**, l. 23.
- `quel sera les rôles` vers **quels seront les rôles**, l. 9.
- `présenté au Paccini` : accord **présentée** ; et vérifier l'orthographe du lieu (**Pacini** ?), l. 3.
- `Plateforme Souveraine et Ouvert en Santé` vers **Ouverte**, l. 46.
- `Numanity` (l. 36) vs `noumanity` partout ailleurs : confirmer si « Groupe Innovation Numanity inc. » est bien la raison sociale voulue, sinon uniformiser.

## D. Ton et cohérence éditoriale

- **Emoji 🤔 répété trois fois dans le résumé** : effet redondant, en garder un seul. Le reste (⚛️🦄💪) passe pour l'audience Linux mais peut détonner pour le public de la Zone d'innovation quantique.
- **Absents du README** : date/heure de la conférence, mention du co-présentateur et de son sujet, mini-plan ou agenda.

## Priorités vu le délai

1. Corriger A1 à A3 (trous et identité du présentateur).
2. Aligner le titre (B4) et lisser le résumé (B5, D).
3. Passer les fautes (C).
4. Le débat de fond sur le positionnement (B6, B7) peut attendre une v2.

## Questions ouvertes à trancher par l'humain

- **A3** : qui présente, André Gerges ou Chrytian Guy (ou les deux), et faut-il intégrer X-Minds au README ?
- **B4** : confirmer « ordinateurs quantiques » comme titre unique.
- **C** : « Numanity » vs « noumanity » dans la raison sociale.
