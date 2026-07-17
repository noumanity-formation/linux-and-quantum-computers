# FND-005 : Typologies d'ordinateurs quantiques et rôle de Linux

- **Statut** : Actif
- **Date** : 2026-07-17
- **Objectif** : Établir une base factuelle sourcée sur les grandes familles d'ordinateurs quantiques (porteurs physiques du qubit et paradigmes de calcul), leurs compromis d'ingénierie, et évaluer en détail où et comment Linux intervient dans chacune. Appuie la présentation « La place de Linux dans les ordinateurs quantiques ».

## 1. Note de rigueur

Deux natures de sources :

1. **Matériel source interne** : `.dev/source-material/poe.com/ordinateur-quantique.md` (revue de littérature sourcée, Question 2 notamment), dont les affirmations sont elles-mêmes rattachées à des URL crédibles, repris et vérifiés ici.
2. **Recherche web complémentaire** pour l'angle propre à cette présentation : le rôle de Linux dans le plan de contrôle, non traité par le matériel source.

Domaine à évolution rapide (jalons datés de 2024 à 2026) : revalider au-delà de 2026 (voir section 7). Les appréciations comparatives sont signalées comme telles.

## 2. Cadrage et thèse

**Question** : quelles sont les grandes familles d'ordinateurs quantiques, qu'est-ce qui les distingue, et où Linux s'insère-t-il ?

**Périmètre** : les porteurs physiques du qubit, les deux paradigmes de calcul, les compromis d'ingénierie, et la couche de contrôle classique. Hors sujet : les algorithmes quantiques détaillés, la description machine par machine (voir FND-006 pour Bromont).

**Thèse** : il n'existe pas d'architecture quantique dominante unique ; chaque famille occupe un créneau selon ses compromis (cohérence, vitesse, connectivité, scalabilité, cryogénie). En revanche, un invariant traverse toutes les familles : le processeur quantique n'est exploitable que par une couche de contrôle classique, très largement pilotée par Linux. C'est le point d'ancrage de la présentation.

## 3. Le qubit : ce qui change par rapport au bit

- Un ordinateur classique manipule des bits (0 ou 1) ; un ordinateur quantique manipule des qubits, qui exploitent la superposition (état combinant 0 et 1) et l'intrication (états de plusieurs qubits interdépendants), source d'accélération pour certaines classes de problèmes.
- **Décohérence** : un qubit ne conserve son état que brièvement avant que l'environnement (chaleur, vibrations, champs) ne le perturbe et n'introduise des erreurs. C'est la contrainte d'ingénierie centrale.
- **Qubit physique vs qubit logique** : un qubit logique est une unité corrigée d'erreur, construite en regroupant plusieurs qubits physiques. Le domaine est passé d'une logique « nombre de qubits » à une logique « qualité et correction » : depuis le franchissement du seuil (Google Willow, décembre 2024), ajouter des qubits peut réduire le taux d'erreur au lieu de l'amplifier.

## 4. Deux paradigmes de calcul

- **Modèle universel à portes** : machine généraliste exécutant des circuits de portes quantiques (la voie d'IBM, Google, etc.).
- **Recuit quantique (quantum annealing)** : approche spécialisée qui laisse un système se stabiliser dans son état de plus basse énergie pour résoudre des problèmes d'optimisation et de simulation (la voie de D-Wave). Non universel.

## 5. Typologies matérielles (porteurs physiques)

### 5.1 Supraconducteurs (transmons)

- Circuits macroscopiques se comportant comme des atomes artificiels, à base de jonctions Josephson, opérant près du zéro absolu.
- Force : la vitesse. Malgré des temps de cohérence courts, ils exécutent le plus grand nombre de portes avant décohérence (environ 5 fois plus que les ions piégés, 2,5 fois plus que les atomes neutres).
- Limite : la connectivité fixe (chaque qubit n'interagit qu'avec quelques voisins), ce qui augmente le nombre d'opérations et contraint le choix des codes correcteurs.
- Statut : épine dorsale industrielle du calcul à portes (IBM, Google). C'est l'architecture de la machine de Bromont (voir FND-006).

### 5.2 Ions piégés

- Atomes chargés confinés dans un champ électromagnétique ; l'information est encodée dans les niveaux d'énergie.
- Forces : cohérence longue, et qubits naturellement identiques (pas de variabilité de fabrication).
- Faiblesses : opérations plus lentes, mise à l'échelle difficile (piéger un grand nombre d'ions).

### 5.3 Atomes neutres

- Atomes neutres (rubidium, césium) piégés par des « pinces optiques » (lasers focalisés), arrangeables en motifs.
- Force : scalabilité par construction (ajouter des qubits est surtout un problème d'optique) et géométrie reconfigurable en cours d'exécution.
- Limite actuelle : fidélité et vitesse des portes en retard sur supraconducteurs et ions.

### 5.4 Photonique

- Qubits « volants » (photons) plutôt que fixes.
- Forces : fonctionnement possible à température ambiante, information transmise à la vitesse de la lumière, bonne intégration avec les technologies classiques et les réseaux.
- Défi majeur : la perte de photons (information perdue à chaque composant optique). Voie de Xanadu (Toronto).

### 5.5 Spin sur silicium

- Spin d'un électron dans une boîte quantique en silicium, ou spin nucléaire d'atomes de phosphore.
- Promesse : réutiliser les procédés de l'industrie des semiconducteurs (intégration industrielle), au prix de défis de cohérence. Voie de Photonic Inc. (spins reliés optiquement).

### 5.6 Topologique (fermions de Majorana)

- Approche visant des qubits intrinsèquement protégés du bruit (Microsoft, puce Majorana 1 annoncée en février 2025). Encore au stade de prototype, sans calcul corrigé d'erreur démontré à ce jour.

### 5.7 Synthèse comparative

| Famille | Cohérence | Vitesse de porte | Connectivité | Scalabilité | Cryogénie |
|---|---|---|---|---|---|
| Supraconducteurs | Courte | Très élevée | Fixe, limitée | Bonne (3D) | Extrême (mK) |
| Ions piégés | Longue | Lente | Élevée (all-to-all) | Difficile | Modérée |
| Atomes neutres | Bonne | Moyenne | Reconfigurable | Excellente | Modérée (vide, lasers) |
| Photonique | Élevée | Élevée | Selon circuit | Perte de photons | Ambiante |
| Spin silicium | Variable | Élevée | Locale | Prometteuse | Extrême |

Consensus (David Awschalom, Chicago Quantum Exchange) : ces architectures ne sont pas en compétition frontale ; chacune a ses forces (supraconducteurs rapides, ions stables, atomes neutres scalables, photons intégrables). La question d'architecte n'est pas « quelle modalité est la meilleure ? » mais « quelle pile correspond au modèle de déploiement, au plan de contrôle et au budget d'erreur de ma charge de travail ? ».

## 6. Où et comment intervient Linux (transverse à toutes les familles)

Point clé pour la présentation : quel que soit le porteur physique, un processeur quantique est inutilisable sans une **couche de contrôle classique**, et cette couche est massivement du Linux. Cinq niveaux :

1. **Électronique de contrôle temps réel (FPGA + Linux embarqué)** : les plateformes de contrôle et de lecture (par exemple QICK de Fermilab, ou le système open source QubiC) reposent sur des FPGA pilotés par un processeur (souvent ARM) sous Linux, avec une interface Python. Le FPGA gère la boucle temps réel (impulsions, latence sous la microseconde nécessaire à la correction d'erreur), tandis que Linux gère la configuration et la récupération des données. Les images sont fréquemment construites avec Yocto/OpenEmbedded (Linux minimal pour contrôleurs embarqués), et les laboratoires utilisent des noyaux **PREEMPT_RT** pour un timing déterministe des séquences de contrôle (voir FND-004, section 6.2).
2. **Orchestration et ordonnancement des tâches** : le service qui reçoit, planifie et exécute les programmes (par exemple Qiskit Runtime chez IBM) repose sur une architecture conteneurisée co-localisée avec le QPU. Les conteneurs sont une technologie Linux (namespaces, cgroups ; voir FND-004, section 4.2).
3. **Co-processeur classique et calcul hybride** : les charges quantiques-classiques (algorithmes variationnels, atténuation d'erreur, décodage de correction) s'exécutent sur des serveurs et grappes HPC sous Linux, couplés au QPU.
4. **Accès infonuagique** : l'exposition du QPU via le cloud (files d'attente, API, authentification) repose sur des serveurs Linux, comme la quasi-totalité de l'infrastructure infonuagique.
5. **SDK et poste de développement** : les kits de développement quantiques (Qiskit, PennyLane, Cirq) sont en Python et tournent nativement sous Linux ; l'écosystème de développement quantique est de facto un écosystème Linux (voir FND-007).

Nuance : la couche strictement temps réel la plus critique (impulsions à la nanoseconde) est portée par le FPGA, pas par Linux ; le rôle de Linux est l'orchestration, la configuration, le calcul classique et l'accès. C'est précisément la distinction « plan de données temps réel » vs « plan de contrôle » familière aux ingénieurs infrastructure.

## 7. Synthèse (ce qu'il faut retenir)

1. Pas d'architecture dominante unique ; supraconducteurs, ions, atomes neutres, photonique, spin silicium et topologique se répartissent selon leurs compromis.
2. Deux paradigmes : portes universelles vs recuit spécialisé.
3. Le passage au régime des qubits logiques (post-Willow 2024) est le vrai changement de métrique du domaine.
4. Invariant clé pour la présentation : toute famille exige une couche de contrôle classique largement pilotée par Linux (FPGA embarqué + PREEMPT_RT, orchestration conteneurisée, HPC hybride, cloud, SDK Python).

## 8. Limites et péremption

- Non couvert : le détail des codes correcteurs, les benchmarks quantitatifs (peu comparables entre modalités), la description d'une machine précise (voir FND-006).
- Péremption : jalons datés (Willow 2024, Majorana 1 en 2025) à revalider ; les fondamentaux (typologies, rôle de la couche de contrôle) sont stables.

## 9. Sources

Provenance interne : `.dev/source-material/poe.com/ordinateur-quantique.md` (revue de littérature sourcée).

Sources primaires et sectorielles (typologies) :

- The Quantum Insider, [neutral-atom vs autres modalités](https://thequantuminsider.com/2024/02/22/harnessing-the-power-of-neutrality-comparing-neutral-atom-quantum-computing-with-other-modalities/).
- Medium (M. Sabol), [comparatif des technologies quantiques](https://medium.com/@MichalSabol/quantum-computing-showdown-evaluating-the-quantum-technologies-87d2bc68b736).
- Chicago Quantum Exchange, [pourquoi les modalités ne sont pas en compétition](https://chicagoquantum.org/news/why-quantum-computing-competition-quantum-prairie-strength).
- Inside DeepTech, [état du quantique 2026](https://www.insidedeeptech.com/the-state-of-quantum-computing-2026-a-field-report/).
- Google Research, [correction d'erreur sous le seuil (Willow)](https://research.google/blog/making-quantum-error-correction-work/) ; Nature, [Quantum error correction below the surface code threshold](https://www.nature.com/articles/s41586-024-08449-y).

Sources (rôle de Linux) :

- Fermilab / QICK, [FPGA-based quantum control](https://www.electronicsforu.com/news/whats-new/control-system-for-quantum-computers-built-on-an-fpga) ; arXiv, [QubiC, contrôle FPGA open source](https://ar5iv.labs.arxiv.org/html/2101.00071).
- PostQuantum, [engineering the Quantum OS stack](https://postquantum.com/quantum-systems-integration/quantum-operating-system-os/).
- Linux Journal, [Qiskit sur Ubuntu](https://www.linuxjournal.com/content/harnessing-quantum-potential-quantum-computing-and-qiskit-ubuntu).
