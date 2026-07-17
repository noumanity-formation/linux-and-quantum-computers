# FND-006 : L'ordinateur quantique IBM de Bromont (PINQ²), description détaillée et rôle de Linux

- **Statut** : Actif
- **Date** : 2026-07-17
- **Objectif** : Décrire en détail l'IBM Quantum System One hébergé à Bromont et opéré par PINQ² (identité, enceinte, cryogénie, processeur, chaîne de contrôle et de lecture), et évaluer en détail où et comment Linux intervient. Appuie la présentation « La place de Linux dans les ordinateurs quantiques » (ancrage local pour l'audience de la Zone quantique de Sherbrooke).

## 1. Note de rigueur

Source principale : le matériel interne `.dev/source-material/poe.com/ordinateur-quantique.md` (revue de littérature technique sourcée, dont chaque affirmation renvoie à une URL crédible : IBM Research, PINQ², Nature, arXiv, IEEE Spectrum). Repris et vérifié ici. L'angle Linux est complété par recherche web (voir FND-005, section 6). Faits datés (mise à niveau de novembre 2025) à revalider (section 8).

**Rectification préalable importante** : il n'existe pas « un ordinateur quantique d'IBM à Bromont » au sens d'une machine exploitée par IBM. C'est un IBM Quantum System One physiquement hébergé dans l'usine IBM de Bromont, mais administré et opéré **exclusivement par PINQ²** (Plateforme d'innovation numérique et quantique du Québec), un OBNL fondé par le ministère de l'Économie du Québec et l'Université de Sherbrooke.

## 2. Cadrage et thèse

**Question** : qu'est-ce précisément que la machine de Bromont, comment est-elle construite, et où Linux intervient-il dans son exploitation ?

**Thèse** : la machine de Bromont est un empilement de couches d'ingénierie (enceinte isolée, cœur cryogénique, processeur supraconducteur, chaîne micro-ondes de contrôle et de lecture) dont le cœur quantique fonctionne près du zéro absolu, mais dont l'exploitation (orchestration, calcul hybride, accès) repose sur une infrastructure classique de type Linux. C'est l'illustration locale parfaite de la thèse de la présentation.

## 3. Identité et statut opérationnel

- **Modèle** : IBM Quantum System One, inauguré le 22 septembre 2023. Premier ordinateur quantique de ce type au Canada.
- **Gouvernance** : opéré exclusivement par PINQ², accès infonuagique pour universitaires et entreprises à travers le Canada.
- **Processeur d'origine (2023 à 2025)** : Eagle r3, 127 qubits (le système est identifié `ibm_quebec`).
- **Mise à niveau critique (novembre 2025)** : passage au processeur **Heron, 156 qubits**. Gains annoncés vs Eagle : erreurs à deux qubits divisées par 2, erreurs de lecture par 3, vitesse de porte par 9, erreurs en couches par 4 ; valeur démontrée sur des charges dépassant 5 000 opérations de porte. Depuis, la machine rivalise avec les meilleures machines du cloud IBM.

## 4. Enceinte physique (System One)

- Le System One (2019) a transformé l'expérience de laboratoire en produit intégré, optimisé pour la stabilité et l'usage continu.
- **Enceinte** : cube scellé de 2,7 m d'arête, panneaux de verre borosilicate d'un demi-pouce, environnement hermétique isolant les composants quantiques des perturbations externes.
- **Découplage structurel** : des cadres indépendants en aluminium et acier découplent le cryostat, l'électronique de contrôle et le boîtier extérieur (isolation vibratoire et blindage électromagnétique). Logique de « pièce dans la pièce » analogue, mais bien plus exigeante, aux principes d'isolation d'un datacenter.

## 5. Cœur cryogénique (réfrigérateur à dilution)

- **Nécessité** : les qubits supraconducteurs doivent opérer à très basse température ; le moindre bruit thermique provoque la décohérence.
- **Principe** : réfrigérateur à dilution exploitant un mélange d'isotopes hélium-3 / hélium-4 pour atteindre le régime du milli-Kelvin. Les systèmes modernes sont « secs » (cryo-refroidisseur mécanique pour le pré-refroidissement à 50 K puis 4 K).
- **Architecture en étages (« chandelier »)** : refroidissement progressif, chaque plateau plus froid que le précédent, jusqu'à la puce à l'étage inférieur.
- **Température cible** : sous 15 millikelvins (environ -269 °C), plus froid que le vide de l'espace.

## 6. Le processeur (qubit et puce)

- **Qubit : le transmon** : circuit supraconducteur (deux plaques formant un condensateur) couplé à une jonction Josephson (inducteur non linéaire sans perte), se comportant comme un atome artificiel. Transmon à fréquence fixe, conçu pour minimiser la sensibilité au bruit de charge.
- **Non-linéarité (anharmonicité)** : elle crée un espacement inégal des niveaux d'énergie, permettant d'isoler les deux plus bas comme 0 et 1.
- **Matériaux** : niobium, aluminium et tantale (supraconducteurs) sur substrat de silicium ; la jonction Josephson (isolant très mince entre deux supraconducteurs) fournit la non-linéarité.
- **Topologie heavy-hex (maille hexagonale lourde)** : chaque qubit se connecte à deux ou trois voisins, réduisant les erreurs d'interaction, au prix d'une connectivité réduite (compensée par la compilation et l'atténuation d'erreur).
- **Architecture multi-couches** : la puce empile plan des qubits, plan des résonateurs de lecture, plan de câblage et plan interposeur (intégration 3D), ce qui isole les qubits et a rendu l'échelle possible.

## 7. Chaîne de contrôle et de lecture (interfaces électroniques et « capteurs »)

Il n'y a pas de « capteurs » au sens classique : la mesure est une lecture dispersive via un résonateur couplé, dont le signal est amplifié puis numérisé.

- **Principe de contrôle** : les qubits sont pilotés par des impulsions micro-ondes de 4 à 7 GHz. Un programme (portes et circuits) est traduit en impulsions séquencées, distribuées vers les qubits ; des impulsions de lecture récupèrent les états, retraduits en valeurs binaires.
- **Voie descendante (génération)** : à température ambiante, une électronique de contrôle sur mesure synthétise les formes d'onde en modulant une porteuse gigahertz par un signal d'un AWG (générateur de formes d'onde arbitraires). Électronique modulaire côté IBM.
- **Atténuation et filtrage cryogénique** : en descendant les étages, les signaux passent par atténuateurs et filtres pour supprimer le bruit thermique ; câblage coaxial et circuits imprimés flexibles à faible diaphonie.
- **Voie montante (lecture et amplification)** : le signal réfléchi par le résonateur de lecture traverse un amplificateur paramétrique Josephson (JPA), puis un isolateur cryogénique, un amplificateur HEMT, enfin un amplificateur à température ambiante. Paramètres clés : χ (couplage qubit-résonateur) et κ (fuite des photons du résonateur).
- **Multiplexage (clé de la scalabilité)** : environ une chaîne de lecture pour 8 qubits, ce qui réduit drastiquement l'électronique et le câblage dans le cryostat.
- **Problème du câblage** : à plus de 100 qubits, amener et sortir les fils devient un « problème d'immobilier ». Tendance : rapprocher l'électronique des qubits (contrôle CMOS cryogénique à l'étage 4 K, avec CPU cryogénique, générateurs de formes d'onde et discriminateurs d'état).

## 8. Eagle vs Heron (ce qui a changé à Bromont)

- **Eagle r3 (jusqu'en 2025)** : portes d'intrication de type ECR (résonance croisée échoée) sur transmons à fréquence fixe ; durées de porte et de mesure allongées pour la stabilité.
- **Heron (depuis novembre 2025)** : introduction des **coupleurs accordables (tunable couplers)**, qui expliquent les gains (vitesse de porte 9×, fidélité à deux qubits 2×). Puce nettement plus stable et rapide.

## 9. Où et comment intervient Linux (à Bromont)

Le cœur quantique (transmons, cryostat, FPGA de contrôle temps réel) n'est pas « du Linux » ; Linux intervient dans toutes les couches d'exploitation autour, ce qui recoupe le modèle général de FND-005, section 6 :

1. **Électronique de contrôle** : la synthèse des impulsions à la nanoseconde est portée par du matériel dédié (AWG, FPGA). Ces contrôleurs embarqués s'appuient typiquement sur un processeur sous Linux embarqué (souvent avec noyau PREEMPT_RT pour le déterminisme) pour la configuration, la calibration et la remontée de données. Le plan temps réel critique est sur FPGA ; le plan de contrôle est Linux.
2. **Orchestration des tâches** : l'exécution des programmes soumis par le cloud passe par un service d'ordonnancement (type Qiskit Runtime) à architecture conteneurisée co-localisée avec le QPU, donc reposant sur des primitives Linux (conteneurs, cgroups, namespaces).
3. **Calcul hybride classique** : PINQ² couple le System One à un HPC classique à Sherbrooke pour offrir des services de calcul hybride quantique-classique. Ces grappes HPC tournent sous Linux ; c'est là que s'exécutent l'atténuation d'erreur, le décodage et les boucles variationnelles.
4. **Accès infonuagique** : les files d'attente, l'API, l'authentification et la distribution des résultats à l'écosystème canadien (IVADO, Université de Sherbrooke, Quantum Algorithms Institute, Concordia, etc.) reposent sur une infrastructure serveur Linux.
5. **Côté utilisateur** : les chercheurs et entreprises soumettent leurs circuits depuis des postes et serveurs sous Linux via des SDK Python (voir FND-007).

Formule pour la présentation : à Bromont, l'ordinateur quantique fonctionne à -269 °C, mais on le **pilote, l'orchestre et l'exploite depuis Linux**.

## 10. Synthèse (ce qu'il faut retenir)

1. Machine = IBM Quantum System One à Bromont, opérée par PINQ² (pas par IBM), Heron 156 qubits depuis novembre 2025 (après Eagle r3 127 qubits).
2. Empilement : cube borosilicate découplé, réfrigérateur à dilution sous 15 mK, processeur transmon supraconducteur multi-couches en heavy-hex, chaîne micro-ondes 4-7 GHz (AWG → descente atténuée → JPA/HEMT/RT), multiplexage de lecture (~8 qubits/chaîne).
3. Le cœur est quantique et cryogénique ; l'exploitation (orchestration conteneurisée, HPC hybride, cloud, contrôleurs embarqués) est du Linux.

## 11. Limites et péremption

- Non couvert : spécifications exactes du Heron, feuille de route vers System Two, modalités contractuelles d'accès.
- Péremption : la génération de processeur (Eagle → Heron) et les chiffres de performance évoluent ; revalider au-delà de 2026.
- Le degré de détail du rôle de Linux dans les contrôleurs propriétaires d'IBM est inféré du modèle général de l'industrie (QICK/QubiC, contrôle CMOS cryogénique) ; IBM ne publie pas l'intégralité de sa pile logicielle bas niveau.

## 12. Sources

Provenance interne : `.dev/source-material/poe.com/ordinateur-quantique.md`.

Sources primaires et sectorielles :

- IBM Research, [premier IBM Quantum System One au Canada](https://research.ibm.com/blog/ibm-pinq2-quantum-computer-install) ; PINQ², [mise à niveau vers le processeur Heron](https://www.pinq2.com/en/actu/pinq2-updates-canadas-first-ibm-quantum-system-one-with-latest-heron-processor/) et [inauguration](https://www.pinq2.com/en/presse/inauguration-du-ibm-quantum-system-one-du-quebec/).
- Grokipedia, [IBM Q System One](https://grokipedia.com/page/IBM_Q_System_One) ; Wikipedia, [IBM Q System One](https://en.wikipedia.org/wiki/IBM_Q_System_One).
- IBM Quantum, [cryostat et concept Goldeneye](https://www.ibm.com/quantum/blog/goldeneye-cryogenic-concept-system), [processeur Eagle 127 qubits](https://www.ibm.com/quantum/blog/127-qubit-quantum-processor-eagle) et [performance/atténuation d'erreur Eagle](https://www.ibm.com/quantum/blog/eagle-quantum-error-mitigation).
- IEEE Spectrum, [coupleurs accordables et vision supercalcul quantique](https://spectrum.ieee.org/ibm-quantum-computer-2668978269) ; Popular Science, [au cœur d'un ordinateur quantique IBM](https://www.popsci.com/technology/in-photos-journey-to-the-center-of-a-quantum-computer/).
- Nature Communications, [générateur d'impulsions micro-ondes cryogénique](https://www.nature.com/articles/s41467-024-50333-w) ; arXiv, [contrôle CMOS cryogénique](https://arxiv.org/html/2302.11538).
- Inside Quantum Technology, [System One de Bromont pour PINQ²](https://www.insidequantumtechnology.com/news-archive/canadas-first-ibm-quantum-system-one-goes-to-quebecs-pinq%C2%B2/).
