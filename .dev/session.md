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


## 5.  Planifier la préparation du pdf support à la présentation

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

## 6. Correctifs placement des images sur la page présentation


Voici les 4 correctifs:

- Le logo sur le codeQR doit être plus gros. Il est actuellement illisible.
- Utiliser le même code QR sur la page de présentation et la page finale.
- La photo et le code QR de la page de présentation doivent être de la même taille que le code qr de la dernière slide. Ils doivent être positionné au centre, juste  en dessous du nom + titre professionnel de l'auteur
- le titre du présentateur est le suivant => "Stratégie & Leadership des pratiques de sécurité | DevSecOps"

Recommandations:
  - Utiliser un outil cli pour générer le code QR.
  - créer une variante de template pour ce nouveau type de page de présentation
Contrainte: Ajouter une commande "qrcode" dans le cli et générer le code QR dans le répertoire dist.


TODO: 

Rédiger le plan et si aucune objection majeure => exécuter


## 7. minor fix

Dans la slide 1: respecter la "marge de sécurité" (bordures minimales requise pour toutes les slides)

Ajuster le code

Corriger la slide 1

## 8. Fix comportement des agents

Dans le script bash, il ne doit pas y avoir de code en python. 

Pourquoi l'agent tente-t-il de générer du code python?

Vérifier les harness files (incluant les skills) et l'ADR.

Inclure la règle "utiliser uniquement les outils (stack techno) décrit dans ADR-001"

Diagnostiquer pourquoi cela n'a pas été respecté.

Apporter les changements au fichiers approprié

Continuer l'exécution de la tâche 7


## 9. doubler les valeurs de la marge de sécurité

Générer la doc utilisateur du cli et du système de respésentation à l'intention des utilisateurs. Mettre ça dans @doc/cli/**.md

La marge de sécurité ne semble pas marcher sur la slide 1

Diagnostiquer. Dire ce qui se passe

recommendation pour disgnostiquer: faire varier les paramèetres de marge et regarder l'effet sur le PDF.

TODO: fix this shit ASAP please.

## 10. fix marge bas de la page de présentation

la page de présentation a une marge inférique qui semble trop petite.

Diminuer la taille des informations en bas des images

Assurer une valeur minimale par défaut suffisante pour la marge du bas.

Utiliser la même méthode que la tâche 9 pour diagnostiquer.

## 11. l'alignement vertical est à chier...

s'assurer d'un bon alignement vertical et d'un espacement cohérent pour mettre en valeur les éléments selon leur importance.

Voici les blocs d'information selon leur importance:

bloc 1: titre
bloc 2: photo + codeQR
bloc 3: nom et titre de l'auteur
bloc 4: infos sur la présentation ( date, nom de l'évènement, lieu de l'évènement, mention "Organisé par 🐧Martial Bigras")

Ajouter l'émoji pingouin près du nom de Martiel

Faire du bloc 4 un bloc cohérent en diminuant l'espace entre les 2 lignes

Imposer un espacement égal entre bloc 2 et les blocs adjacents (haut + bas) 

## 12. confusion à proposs de l'ordre d'affichage (placement) et l'ordre d'importance communicationnel


Il ne fallait pas changer le positionnement des blocs d'information.

ce sont 2 dimensions distinctes:

Ordre d'apparition vertical

- 1. bloc 1
- 2. bloc 3
- 3. bloc 2
- 4. bloc 4 

Ordre d'importance communicationnelle


- 1. bloc 1
- 2. bloc 2
- 3. bloc 3
- 4. bloc 4 

Corriger

## 13. Finaliser la recherche

**Thèse de la recherche**:  "L'adoption de l'objection-sociocratique comme unique règle constitut un framework cohérent et complet pour le fonctionnement de communautés de pratiques intentionnés"

**Argumentaire**:

- Toute les communautés sont des communautés de pratiques ET d'intention
- Richard Stallman a créé une communauté d'intention clairement assumé: Liberté de faire comme principe fondateur
- Beaucoup de communauté n'explicitent pas leurs intentions. Mais TOUTEs les commaunautés ont une intention partagée. C'est la raison d'être de la communauté. Si il n'y a pas d'intention commune, la communauté ne tient pas.
- Linus Torval avait une intention autre que celle de Richard Stallman. Il a donc adapté la gouvernance de sa communauté pour prendre en compte cette intention différente. Aussi, il a créé un outil (git) + de nouvelles licence + fondation. Exactement le même pattern que Stallman avait fait avant lui.
- l'erreur de Torval a été de croire qu'il n'avait pas d'intention idéologique. Son intention idéologique et de créer un produit industriel révolutionnaire.
- Torval a réussi son intention et sa communauté l'a bien intégré
- Malheureusement, sa structure de gouvernance (Benevolent Dictatorship) met en péril la viabilité à long terme de Linux



TODO:

- Consulter la recherche préliminaire dans @.dev/source-material/SRCM-001-analyse-avec-poe.com/linux-communaute-intention-vs-communaute-pratique
- Définir les recherches de fondations nécessaires pour étailler la Thèse et l'Argumantaire 
- Dire si la thèse tient ou pas
- Formuler une critique de l'argumentaire et émettre des objections
- rédiger un plan pour la rédaction

## 14. Réaliser la recherche avant de se prononcer

Effectuer les tâches suivantes:

- Consulter la recherche préliminaire dans @.dev/source-material/SRCM-001-analyse-avec-poe.com/linux-communaute-intention-vs-communaute-pratique
- Définir les recherches de fondations nécessaires pour étailler la Thèse et l'Argumantaire 
- Dire si la thèse tient ou pas
- Formuler une critique de l'argumentaire et émettre des objections

Le plan ne concerne que la rédaction d'un article scientifique qui nécessitera plus de travail et qui sera fait plus tard


