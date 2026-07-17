# FND-007 : Utiliser l'ordinateur quantique IBM (Qiskit), du programme à l'exécution, et le rôle de Linux

- **Statut** : Actif
- **Date** : 2026-07-17
- **Objectif** : Expliquer comment on utilise concrètement un ordinateur quantique IBM (dont celui de Bromont via PINQ²) : comment on écrit un programme, comment il fonctionne, comment on le lance, et décrire en détail où et comment intervient Linux. Appuie la présentation « La place de Linux dans les ordinateurs quantiques ».

## 1. Note de rigueur

Source principale : documentation officielle IBM Quantum (Qiskit, Qiskit Runtime) et dépôts Qiskit, complétées par le matériel interne `.dev/source-material/poe.com/ordinateur-quantique.md` (chaîne d'exécution physique) et FND-006 (machine de Bromont). Le workflow décrit correspond à Qiskit et Qiskit Runtime dans leur forme actuelle (primitives V2). Les détails d'API évoluent vite : revalider au-delà de 2026 (section 8).

## 2. Cadrage et thèse

**Question** : quel est le cycle de vie complet d'un programme quantique, de son écriture à son résultat, et quel rôle Linux y joue-t-il ?

**Thèse** : programmer un ordinateur quantique aujourd'hui, c'est écrire du Python (Qiskit) qui construit un circuit, le fait compiler pour une machine cible, puis le soumet à un service d'exécution infonuagique qui l'orchestre auprès du QPU. À chaque étape (poste de développement, compilation, service d'orchestration, co-processeur classique, contrôleurs) l'infrastructure sous-jacente est du Linux. Le quantique ne remplace pas Linux : il s'ajoute comme un accélérateur piloté depuis Linux.

## 3. Le modèle mental : un accélérateur, pas un ordinateur autonome

- Un QPU (Quantum Processing Unit) ne fait pas tourner un système d'exploitation ni un programme séquentiel. Il exécute un **circuit** : une séquence de portes appliquées à des qubits, suivie de mesures.
- On l'utilise comme on utilise un GPU : un hôte classique (sous Linux) prépare le travail, l'envoie à l'accélérateur, récupère le résultat. C'est le modèle du **calcul hybride quantique-classique**.
- Comme un circuit est probabiliste (la mesure projette un état superposé), on exécute le circuit un grand nombre de fois (les « shots ») et on lit une distribution de résultats.

## 4. Écrire un programme (Qiskit)

Qiskit est le SDK open source d'IBM, en Python. Le cycle de développement type :

1. **Installer l'environnement** (sur Linux) : `pip install qiskit qiskit-ibm-runtime`. L'écosystème (Qiskit, PennyLane, Cirq) est en Python et tourne nativement sous Linux.
2. **Construire le circuit** : définir les qubits, appliquer les portes, mesurer.
3. **S'authentifier** au service : `QiskitRuntimeService` avec un jeton d'API.
4. **Choisir une machine cible (backend)** : par nom (par exemple `ibm_quebec` pour Bromont) ou via la moins occupée.
5. **Compiler (transpiler)** le circuit vers l'architecture réelle de la machine.
6. **Exécuter** via une primitive (Sampler ou Estimator).
7. **Récupérer et interpréter** les résultats.

Exemple minimal (état de Bell, deux qubits intriqués) :

```python
from qiskit import QuantumCircuit
from qiskit.transpiler.preset_passmanagers import generate_preset_pass_manager
from qiskit_ibm_runtime import QiskitRuntimeService, SamplerV2 as Sampler

# 2. Construire le circuit
qc = QuantumCircuit(2)
qc.h(0)            # superposition sur le qubit 0
qc.cx(0, 1)        # intrication qubit 0 -> qubit 1
qc.measure_all()   # mesure

# 3-4. Service et machine cible
service = QiskitRuntimeService()
backend = service.backend("ibm_quebec")   # la machine de Bromont, à titre d'exemple

# 5. Transpilation vers l'ISA de la machine
pm = generate_preset_pass_manager(optimization_level=1, backend=backend)
isa_circuit = pm.run(qc)

# 6. Exécution
sampler = Sampler(mode=backend)
job = sampler.run([isa_circuit], shots=4096)
print("job id:", job.job_id())

# 7. Résultats
result = job.result()
print(result[0].data.meas.get_counts())
```

## 5. Comment ça fonctionne (ce qui se passe réellement)

### 5.1 La compilation (transpilation)

Un circuit écrit abstraitement doit être transformé pour ne contenir que des instructions réellement supportées par le QPU cible (le jeu d'instructions, ou ISA). Le transpileur adapte le circuit à la connectivité de la machine (par exemple la maille heavy-hex de Bromont, voir FND-006), remplace les portes non natives, insère les échanges (swaps) nécessaires et optimise. C'est une étape de calcul classique, exécutée sur l'hôte Linux.

### 5.2 Les primitives et le service Runtime

- On ne « parle » pas directement au QPU : on soumet le travail à **Qiskit Runtime**, service d'exécution qui ordonnance les tâches, applique l'atténuation d'erreur et gère le rapprochement calcul classique / QPU. Son architecture est conteneurisée et co-localisée avec le QPU (gain de latence de l'ordre de 100×).
- Deux primitives standard :
  - **Sampler** : renvoie des distributions d'échantillons (les comptes de résultats mesurés).
  - **Estimator** : renvoie des valeurs d'espérance d'observables (utile pour la chimie, l'optimisation, les algorithmes variationnels).
- **Sessions et modes batch** : les tâches d'une même session sont priorisées par l'ordonnanceur, ce qui rend efficaces les boucles itératives (par exemple variationnelles) qui alternent calcul classique et appels au QPU.

### 5.3 De la soumission au signal physique

Une fois la tâche planifiée, le circuit ISA est traduit en une séquence d'impulsions micro-ondes (4 à 7 GHz) qui pilotent les qubits, puis des impulsions de lecture mesurent les états, retraduits en valeurs binaires et renvoyés à l'utilisateur (chaîne physique détaillée dans FND-006, section 7). Le circuit est répété sur de nombreux shots ; le résultat est une distribution.

## 6. Lancer le programme : le cheminement complet

1. **Poste de développement (Linux)** : l'utilisateur exécute son script Python Qiskit ; construction et transpilation du circuit en local.
2. **Soumission au cloud** : le client `qiskit-ibm-runtime` envoie la tâche via HTTPS à l'API IBM Quantum (ou à l'accès PINQ² pour Bromont) ; authentification par jeton.
3. **Files d'attente et ordonnancement (serveurs Linux)** : le service place la tâche en file, la planifie, réserve le QPU.
4. **Exécution Runtime (conteneurs Linux co-localisés)** : le service pilote la calibration, l'atténuation d'erreur et l'interaction avec le contrôleur du QPU.
5. **Contrôleur temps réel (FPGA + Linux embarqué)** : génération des impulsions et lecture (le plan temps réel critique est sur FPGA ; la configuration et la remontée passent par Linux, souvent PREEMPT_RT).
6. **Retour des résultats** : la distribution mesurée remonte la même chaîne jusqu'au script de l'utilisateur.

## 7. Où et comment intervient Linux (récapitulatif détaillé)

| Étape | Rôle de Linux |
|---|---|
| Poste de développement | Exécution du SDK Python (Qiskit), construction et transpilation ; environnement de dev de facto Linux |
| Transpilation | Calcul classique sur l'hôte Linux |
| API et files d'attente | Serveurs web/API infonuagiques sous Linux |
| Service Runtime | Conteneurs (namespaces, cgroups) co-localisés avec le QPU |
| Atténuation d'erreur, décodage, boucles variationnelles | HPC classique sous Linux (calcul hybride, à Sherbrooke pour PINQ²) |
| Contrôleur du QPU | FPGA pour le temps réel ; Linux embarqué (souvent PREEMPT_RT) pour configuration/données |
| Retour et post-traitement | Analyse des résultats en Python sous Linux |

La seule couche qui n'est pas du Linux est le plan strictement temps réel (impulsions à la nanoseconde, sur FPGA) et, bien sûr, le QPU lui-même. Tout le reste (écriture, compilation, orchestration, calcul hybride, accès) est du Linux. C'est exactement la répartition « plan de données temps réel » vs « plan de contrôle » familière aux administrateurs système.

## 8. Synthèse (ce qu'il faut retenir)

1. Programmer le quantique = écrire du Python (Qiskit) qui construit un circuit, le transpile pour la machine cible, puis le soumet à un service d'exécution infonuagique.
2. Le QPU s'utilise comme un accélérateur (à la manière d'un GPU) piloté par un hôte classique ; le calcul est hybride et probabiliste (shots, distributions).
3. Linux est présent à chaque étape sauf le plan temps réel FPGA et le QPU cryogénique : poste de dev, compilation, API/cloud, orchestration conteneurisée, HPC hybride, contrôleurs embarqués.
4. Message de la présentation : à l'ère quantique, le sysadmin Linux ne disparaît pas, il pilote l'accélérateur quantique.

## 9. Limites et péremption

- Non couvert : les algorithmes quantiques eux-mêmes, les détails de l'atténuation et de la correction d'erreur, les autres SDK (PennyLane, Cirq) en profondeur.
- Péremption : l'API Qiskit et les primitives évoluent rapidement (passage aux primitives V2, dépréciations) ; revalider le code et les noms d'API au-delà de 2026. Le nom exact du backend de Bromont et ses conditions d'accès via PINQ² sont à confirmer directement auprès de PINQ².

## 10. Sources

Provenance interne : `.dev/source-material/poe.com/ordinateur-quantique.md` ; FND-006 (chaîne physique de Bromont).

Sources primaires :

- IBM Quantum Documentation, [service Qiskit Runtime](https://quantum.cloud.ibm.com/docs/en/api/qiskit-ibm-runtime/runtime-service), [démarrer avec Sampler](https://quantum.cloud.ibm.com/docs/en/guides/get-started-with-sampler) et [primitives V2](https://quantum.cloud.ibm.com/docs/en/guides/v2-primitives).
- GitHub, [qiskit-ibm-runtime](https://github.com/Qiskit/qiskit-ibm-runtime) et [Qiskit SDK](https://github.com/Qiskit/qiskit).
- PostQuantum, [engineering the Quantum OS stack](https://postquantum.com/quantum-systems-integration/quantum-operating-system-os/) (architecture conteneurisée, latence Runtime).
- Fermilab / QICK, [contrôle FPGA](https://www.electronicsforu.com/news/whats-new/control-system-for-quantum-computers-built-on-an-fpga) ; arXiv, [QubiC (Flask sur machine Linux près du châssis FPGA)](https://ar5iv.labs.arxiv.org/html/2101.00071).
- Linux Journal, [Qiskit sur Ubuntu](https://www.linuxjournal.com/content/harnessing-quantum-potential-quantum-computing-and-qiskit-ubuntu).
