---
start-at: 2026-07-07 15h47
---

# Intention

Produire le matériel accompagnant ma présentation à la Rencontre Linux au Québec du 7 juillet 2026:

- README.md contenant un abstract de la présentation + ma bio + fiche de mon entreprise
- le pdf de la présentation
- un rapport de recherche



# Contexte

Je donne ma présentation dans une heure. Il faut accélérer.

# Livrables

- README de présentation
- pdf de présentation
- Rapport de recherche

# Tâches

## 1. Gérérer les ressources requises à partir du repo de la dernière présentation au RLQ

Le répertoire $HOME/git/noumanity-communication/review_impact-of-PQC-risks-on-main-Linux-distributions

Contient une présentation donnée au RLQ de Québec.

Analyser le dossier et 

- en déduire un skill spécialisé pour les README.md de présentation
- en déduire un skill spécialisé pour l'écriture d'un script bash de génération de pdf pour présentation
- analyser le script bash cli, le nettoyer/refactorer/améliorer et le mettre dans ce repo

TODO: préparer le plan et critiquer la tâche pour en relever les objections

## 2. Réponse aux objections

### point 1

Oui, effectivement. Il n'y avait pas de section entreprise.
Ceci et un ajout à la spécification. L'inclure dans le skill.

Recadrage. Pour l'instant, la demande n'est pas de produire le fichier README.md. Mais seulement le skill qui encadre sa rédaction / vérification. 

Il est probable qu'il soit écrit par un humain et que l'agent n'ai qu'à en faire la vérification.

### point 2

Le script est fonctionnel. Mais il repose sur un usage local in-repo et sur une convention de nom de fichiers et de répertoires.

Faites le nécessaire pour qu'il soit copier dans ce repo pour un usage in-repo de ce repo '@.'

Ne pas faire un gros refactoring. Analyser le code. Puis:

- apporter les améliorations mineurs qui ont un faible impact sur les fonctionnalités mais améliorent la robustesse.
- Analyser la cohérence de l'interface cli (les commandes) au regard des pratiques standards de l'industrie.
- Analyser l'architectur applicative actuelle
- Proposer un plan d'indervention PLN-003

### point 3

Bien vu. Ajouter dans PLN-002, un skill de rédaction des ADR et la rédarcion d'un ADR regroupant tous les choix d'architecture de ce cli.

La séquence d'exécution dans le plan doit être celle-ci:

Redaction skill adr => analyse du cli => rédaction adr pour cli => redaction skill cli => codage du cli

### point 4

Ajouter, aux harness files CLAUDE.md et CONSTITUTION.md, le nécessaire pour prendre en compte tous les nouveaux livrables:


- README de présentation
- pdf de présentation
- Rapport de recherche


### TODO

adapter le plan et dir es'il reste des objections

## 3. exécuter le plan PLN-002


## 4. Planifier la révision du readme

Le plan PLN-003 ne sera pas exécuté durant cette session. Renommez le PLN-00X.

Créer un plan pour la révision rapide du readme.

Ce qui est important:

- aucune inexactitude
- aucune fautes

objectif de communication: faire reconnaitre la compétence de l'auteur en matière d'organisation de projets open source

audience: acteurs du milieu open source qu Québec

TODO: rédiger le plan


## x.  Planifier la préparation du pdf support à la présentation

La présentation est un atelier pratique de 5 minutes sur le mécanisme de l'objection-sociocratique.

Aucune slide ne doit avoir de pied de page

Slide 1: page de présentation
Contient :
- titre de la présentation
- nom de l'auteur
- photo de l'auteur + Code QR pointant vers: https://github.com/noumanity-formation/intentional-dooers-governance  + aux couleurs de noumanity (code qr noir + logo de noumanity au centre https://github.com/noumanity/imagen/blob/main/assets/isotipo/isotipo%20noumanity-color.png)
- date, nom de l'évènement, lieu de l'évènement
- mention "Organisé par 🐧Martial Bigras"



Slide 2: proposition => Renommer REL pour ReLaQx pour éviter la confusion avec RLQ == Réseau des Lesbiennes du Québec

Slide 3: Remerciement & Questions

Contient: code QR pour le matériel supplémentaire


!!IMPORTANT!!

Voici comment nous allons produire le pdf:

- 1. produire le contenu dans fichier markdown+yaml
- 2. (au besoin) adapter le script bash
- 3. produite le pdf en exécutant le script et mettre dans @dist/**.pdf

TODO: 

Rédiger le plan et si aucune objection majeure => exécuter

