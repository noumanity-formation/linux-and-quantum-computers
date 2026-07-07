---
start-at: 2026-07-07 15h47
---

# Intention

Produire le matériel accompagnant ma présentation à la Rencontre Linux au Québec du 7 juillet 2026:

- README.md contenant un abstract de la présentation + ma bio + fiche de mon entreprise
- le pdf de la présentation
- un rapport de recherche



# Contexte


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