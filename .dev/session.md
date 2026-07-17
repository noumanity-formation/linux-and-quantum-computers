# INTENTION

- Produire une présentation intitulée "La place de Linux dans les ordinateurs numériques"
- Positionner Jérémy Viau-Trudel comme un expert quantique



# CONTEXTE

do it ASAP, je donne la présentation dans 2h30

Dans le cadre de la tournée des Rencontres Linux au Québec de juillet 2026.


- pour une audience primaire de la communauté Linux
- et une audience secondaire d'acteurs la Zone d'innovation Quantique de Sherbrooke
- Sera également présent comme présentateur: Chrytian Guy. Il présentera son concept de X-Minds: neuroypique de haut-niveau

# LIVRABLES

fichier pdf produit à partir du cli


# Tâches

## 1. [revision de l'abstract]

Vérifier le fichier README et en faire une analyse critique

## 2. recherche des infos du triangle Québec - Sherbrooke - Montréal

Rechercher et collecter les informations sur le "Triangle Québec - Montréal - Sherbrooke" dans tous les dossiers (récursivement) à partir de @../../

Exclure toute information confidentielle de noumanity et de ses partenaires d'affaire.

Partez de ces infos et complétez-les avec une recherche de fondation à propos de l'écosystème Québécois du quantique. Mettre l'emphase sur l'écosystème d'innovation de la Zone Quantique de Sherbrooke

## 3. [révision de l'abstract]

## 4. [Recherche de fondation] Linux

faire une recherche de fontation à propos de linux:
- linux le kernel vs les distributions GNU/linux
- présentation de l'architecture du noyau linux: principales fonctionalités et leurs évolutions dans le temps
- intégration linux avec GPU
- intégration linux avec matériel non standard: capteurs, actuateurs (robotique), instruments de recherche, autres notables

## 5. [Recherche de fondation] les ordinateurs quantique et l'ordinateur IBM de Bromont

Lire le fichier @.dev/source-material/poe.com/ordinateur-quantique.md

Étendre la recherche et produire 2 Recherche de fondation:
- les typologie d'ordinateur quantique
- l'ordinateur quantique de IBM à Bromont (description détaillé)

Dans ces 2 cas, évaluer en détail où et comment intervient Linux


## 6. [Recherche de Fondation] Utilisation de l'ordinateur quantique de IBM

Expliquer comment on peut utiliser l'ordinateur quantique de IBM?
Comment on fait un programme, comment celui-ci fonctionne et comment on le lance.

Décrire en détails comment et où intervient linux.


## 7. Plan et premier jet 

Plan de la présentation

- page titre
- plan de la présentation
- partenaires dans projets quantiques
- Qu'est-ce qu'un ordinateur et à quoi sert Linux
  - schéma simplifier: compute + mémoire de travail + stockage information
- Qu'est-ce qu'un ordinateur quantique
  - bit => qbit et autres systèmes de représentation des données
  - typologie d'un ordinateur quantique
  - IBM Quantum System One de Bromont
  - Accès au calcul via PINQ2
- Ambition de noumanity
  - Plateforme Souveraine et Ouverte de Calcul Quantique
- Remerciements

## 8 [améliorations] 

En général => s'assurer que le contenu ne dépasse pas la page

Créer un autre type de diapo pour mettre des images et des diagrammes

### diapo 1: page titre

titre: La place de Linux dans les ordinateurs quantique
code QR: https://github.com/noumanity-formation/linux-and-quantum-computers
(générer code qr dans fichier à part)
contexte: 
  - Rencontre Linux au Québec
  - 17 juillet
  - 

  - bloc 1: titre
  - bloc 2: auteurs: Jérémy Viau-Trudel - Stratégie & Leadership des pratiques de sécurité | DevSecOps | Social Hacker + photo & code qr
  - bloc 3: contexte
  - bloc 4: logo de noumanity + "Studio DeepTech" (en dessous)


### diapo 1.1 

  - André Gerges => Conseiller en recherche en cybersécurité et conformité
  - NationTech => DataCenter miniaturisé et décentralisé
  - QGuard => startup USA, Surveillance dynamique de configurations cryptographique et flux de données cryptés
  - Amera Iot => startup USA chips pour crypto avancée
  - American Binary => startup USA, VPN encryption avancée
  - Jean Auger, Mathématicien, recherche privée en Intelligence Quantique

### diapo 2.1 

Ajouter des images et des schemas. Moins de texte

## 9. améliorations

### 2.2 

Ajouter des images et des schemas. Moins de texte

### 2.3 

mettre un schema

### 2.4 

mettre un schema

### 3.1

- Ambition de noumanity
  - Plateforme Souveraine et Ouverte de Calcul Quantique

3 composants: Datacenter de NationTech + librairie exposant une banque d'algos implémentés en quantique + connexion sécure (VPN American binary) entre 

Souveraine => accélérer l'accès au calcul quantique aux entreprises québécoise

ouvert => participatif + output 100% libre et open source

mettre un schema     DataCenter NationTech <-> Pinq2 <-> IBM Bromont

### remerciement

enlever l'url sous le code QR. Mettre juste Matériel et sources

## 10. améliorations

### logo

Utiliser le fichier "@src/assets/isotipo noumanity-orange-black2.jpg" dans le code QR

Utiliser le fichier @src/assets/logo noumanity-color2.png pour le logo de noumanity sur la page titre

Ajouter le logo de noumanity + "Studio DeepTech" sur la page de remerciement

### expliquer les transmons

Ajouter un schéma expliquant c'est quoi un transmon après la slide 2.2
