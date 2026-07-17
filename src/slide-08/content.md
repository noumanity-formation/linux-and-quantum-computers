---
diapo:
  model: plain
content:
  title: "Accéder au calcul quantique via PINQ²"
  section: "Ordinateur quantique"
---

Un QPU s'utilise comme un **accélérateur** (à la manière d'un GPU), piloté par un hôte classique.

Un programme (Qiskit, en Python) :

- on **écrit** un circuit, on le **transpile** pour la machine
- on le **soumet** au cloud ; il devient des impulsions micro-ondes
- on **récupère** une distribution de résultats

**Linux** est présent partout, sauf le temps réel FPGA et le QPU : dev, compilation, cloud, orchestration, HPC hybride.

À l'ère quantique, le sysadmin ne disparaît pas : **il pilote l'accélérateur quantique.**
