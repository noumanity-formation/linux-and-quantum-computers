# FND-004 : Linux, du noyau aux distributions et à l'intégration matérielle

- **Statut** : Actif
- **Date** : 2026-07-17
- **Objectif** : Établir une base factuelle sourcée sur Linux (distinction noyau / distributions GNU/Linux, architecture et évolution du noyau, intégration GPU, intégration de matériel non standard) pour appuyer la présentation « La place de Linux dans les ordinateurs quantiques », notamment l'argument selon lequel Linux est la couche de contrôle des systèmes avancés, y compris quantiques.

## 1. Note de rigueur

Sujet technique largement documenté et stable dans ses fondamentaux. Sources privilégiées : documentation officielle du noyau (`docs.kernel.org`, `dri.freedesktop.org`), Wikipedia pour la chronologie versionnée, et sources spécialisées reconnues (Bootlin, Analog Devices) pour les sous-systèmes matériels. Les faits d'actualité (numéros de version récents) sont datés et à revalider (voir section 7). Les points d'appréciation (importance relative d'une version, tendance) sont signalés comme tels.

## 2. Cadrage et thèse

**Question** : qu'est-ce que Linux, comment son noyau est-il structuré et comment s'intègre-t-il au matériel, du GPU jusqu'aux dispositifs non standard ?

**Périmètre** :

- Dans le sujet : distinction noyau / distribution, sous-systèmes du noyau et leur évolution, pile graphique (GPU), intégration de capteurs, d'actionneurs et d'instruments.
- Hors sujet : l'histoire détaillée des distributions, l'administration système, la comparaison avec d'autres OS.

**Thèse** : Linux n'est pas d'abord un système d'exploitation « de bureau » ; c'est un noyau monolithique modulaire, pilote universel de matériel, qui s'est imposé comme couche de contrôle des ordinateurs à haute performance et des instruments scientifiques et industriels. Cette universalité matérielle est précisément ce qui le place au coeur des infrastructures quantiques.

## 3. Le noyau Linux vs les distributions GNU/Linux

### 3.1 Le noyau (Linux au sens strict)

- « Linux » désigne d'abord le noyau, démarré par Linus Torvalds en 1991, écrit principalement en C (et, depuis peu, en partie en Rust). Le noyau gère le matériel et expose des services aux programmes via les appels système. Il ne constitue pas, à lui seul, un système utilisable.

### 3.2 GNU/Linux et les distributions

- Un système utilisable combine le noyau avec un espace utilisateur : les outils du projet GNU (compilateur, bibliothèque C, coreutils, shell), un système d'initialisation, des bibliothèques et des applications. D'où l'appellation « GNU/Linux » défendue par la Free Software Foundation.
- Une **distribution** est un assemblage cohérent et maintenu : noyau (souvent une version choisie puis rétro-patchée par le distributeur), espace utilisateur, gestionnaire de paquets, politique de mise à jour et de sécurité. Exemples : Debian, Ubuntu, Fedora, Red Hat Enterprise Linux, Arch, SUSE.
- Conséquence importante : le **versionnage du noyau** (par exemple 6.12) est distinct du **versionnage de la distribution** (par exemple Ubuntu 24.04). Une même version de noyau peut se retrouver, patchée différemment, dans plusieurs distributions ; une distribution « entreprise » fige souvent un noyau et le maintient des années (noyaux LTS).

## 4. Architecture du noyau et évolution

### 4.1 Un noyau monolithique modulaire

- Linux est un **noyau monolithique** : ordonnanceur, gestion mémoire, pilotes, pile réseau et système de fichiers virtuel s'exécutent dans un même espace d'adressage privilégié (espace noyau). Ce choix maximise le débit et minimise la latence entre composants, au prix d'une base de confiance plus large qu'un micro-noyau.
- Il est néanmoins **modulaire** grâce aux modules noyau chargeables (LKM) : on ajoute ou retire dynamiquement des fonctionnalités (pilotes, systèmes de fichiers) sans redémarrer.

### 4.2 Principaux sous-systèmes

- **Gestion des processus et ordonnancement** : création, planification et gestion des tâches concurrentes ; ordonnanceur historique CFS, remplacé par EEVDF dans les noyaux récents.
- **Gestion mémoire** : mémoire virtuelle, pagination, espaces d'adressage protégés par processus.
- **Système de fichiers virtuel (VFS)** : interface uniforme au-dessus de systèmes de fichiers hétérogènes (ext4, XFS, Btrfs, etc.).
- **Pile réseau** : implémentation complète de TCP/IP et de nombreux protocoles ; centrale pour les serveurs et les réseaux (dont les réseaux quantum-safe, voir FND-003).
- **Pilotes de périphériques** : traduisent des requêtes génériques du noyau en commandes matérielles ; ils forment la majeure partie du code source du noyau.
- **Communication inter-processus, appels système, sécurité** : IPC, interface d'appels système, et cadres de sécurité (Linux Security Modules, SELinux, AppArmor, seccomp).
- **Virtualisation et conteneurs** : namespaces et cgroups fournissent l'isolation qui sous-tend les conteneurs (Docker, Podman, Kubernetes) et une grande partie de l'infonuagique.

### 4.3 Évolution dans le temps (jalons)

- **1991** : version 0.01, annonce initiale de Torvalds.
- **1994, 1.0** : environ 170 000 lignes ; pile réseau TCP/IP.
- **1996, 2.0** : multiprocesseur symétrique (SMP), gestion de plusieurs CPU.
- **2001, 2.4** puis **2003, 2.6** : 2.6 est un tournant (meilleur ordonnanceur, montée en charge, portage vers de nombreuses architectures, adoption embarquée et serveur massive).
- **2011, 3.0** : franchissement symbolique du numéro pour le 20e anniversaire, sans rupture technique (Torvalds insiste : « rien » de nouveau sur le fond).
- **2015, 4.0** : correctifs à chaud (live patching) du noyau sans redémarrage.
- **2019, 5.0** : élargissement continu du support matériel, dont GPU et accélérateurs.
- **2022, 6.0** puis **6.1** : intégration de l'infrastructure **Rust** dans le noyau (premiers pilotes en Rust), amorçant une évolution du langage au-delà du C.
- **Noyaux 6.x récents** : ordonnanceur EEVDF (6.6) ; intégration en tronc du travail temps réel **PREEMPT_RT** (aboutie autour de 6.12, fin 2024), aboutissement de près de deux décennies d'efforts.
- **2026, 7.0** : nouveau franchissement de numéro majeur (publié le 12 avril 2026), à nouveau sans rupture architecturale, selon la logique de numérotation « cosmétique » assumée par Torvalds.

**Modèle de développement** : cycles courts (environ neuf à dix semaines), fenêtre de fusion puis stabilisation ; noyaux LTS maintenus des années ; l'un des plus grands projets logiciels collaboratifs au monde (milliers de contributeurs, entreprises et bénévoles).

## 5. Intégration avec les GPU

### 5.1 Une pile en deux domaines

La pile graphique Linux se divise entre espace noyau (gestion du matériel) et espace utilisateur (traduction des API en instructions machine).

- **DRM (Direct Rendering Manager)** : sous-système du noyau qui arbitre l'accès au GPU et expose un noeud de périphérique (`/dev/dri/cardX`, plus les *render nodes*) auquel l'espace utilisateur soumet ses tampons de commandes.
- **KMS (Kernel Mode Setting)** : partie de DRM qui configure les modes d'affichage côté noyau (résolution, sorties) dès le démarrage et dynamiquement.
- **GEM** : gestion de la mémoire vidéo côté noyau.

### 5.2 Pilotes noyau et espace utilisateur

- **Pilotes noyau** : `i915` puis `xe` (Intel), `amdgpu` (AMD), `nouveau` (NVIDIA libre) ; NVIDIA fournit aussi désormais des modules noyau ouverts en complément de sa pile propriétaire.
- **Espace utilisateur** : `Mesa 3D` implémente OpenGL et Vulkan (pilotes RADV, ANV, radeonsi, iris) ; `libdrm` encapsule les appels `ioctl` vers le sous-système DRM.

### 5.3 Calcul GPU (au-delà de l'affichage)

- Le GPU sert massivement au calcul parallèle (HPC, IA, simulation). Les piles de calcul reposent sur Linux : CUDA (NVIDIA), ROCm (AMD), oneAPI (Intel).
- Pertinence quantique : la **simulation** d'ordinateurs quantiques et l'entraînement des modèles associés s'exécutent sur des grappes GPU sous Linux ; c'est un pont direct entre l'audience Linux et le calcul avancé.

## 6. Intégration avec du matériel non standard

C'est le point le plus structurant pour la présentation : Linux est un pilote universel, bien au-delà du PC.

### 6.1 Capteurs : le sous-système IIO

- **Industrial I/O (IIO)** couvre les dispositifs de type « capteur » : convertisseurs analogique-numérique (ADC), centrales inertielles (IMU), capteurs de température, accéléromètres, capteurs de pression, de lumière, de proximité, etc.
- Ces dispositifs se connectent typiquement via SPI ou I2C, mais IIO couvre aussi des acquisitions à haute vitesse (DMA, interfaces synchrones, périphériques FPGA), ce qui le rend pertinent pour l'instrumentation scientifique.

### 6.2 Actionneurs et robotique

- **GPIO** (avec l'interface moderne `libgpiod`), **PWM**, bus **SPI/I2C**, et **SocketCAN** (bus CAN) permettent de piloter des actionneurs, moteurs et automates.
- **PREEMPT_RT** transforme Linux en système temps réel à latence prévisible en réécrivant des parties du noyau pour prioriser les tâches critiques, au prix d'un léger débit. C'est l'élément clé pour la robotique et le contrôle de mouvement : « quand le robot doit agir, l'OS n'hésite pas ».
- **ROS 2** (Robot Operating System), intergiciel open source dominant en robotique, s'appuie sur Linux (souvent avec PREEMPT_RT) pour cobots, véhicules autonomes, manipulateurs industriels, boucles de trajectoire.

### 6.3 Instruments de recherche et acquisition de données

- Linux est le socle logiciel de nombreuses grandes infrastructures scientifiques : systèmes de contrôle d'accélérateurs et d'installations (par exemple l'écosystème EPICS), acquisition de données (Comedi), pilotage d'instruments de laboratoire (USB-TMC / VISA).
- **Pont quantique** : les électroniques de contrôle des qubits (souvent à base de FPGA), la supervision des cryostats, la synchronisation temporelle et l'orchestration des expériences quantiques tournent très largement sous Linux. Autrement dit, l'ordinateur quantique se pilote depuis Linux, ce qui rejoint directement la thèse de la présentation et les infrastructures décrites dans FND-003 (PINQ², Kirq).

## 7. Synthèse (ce qu'il faut retenir)

1. « Linux » = un noyau ; une distribution = ce noyau plus un espace utilisateur (GNU) assemblé et maintenu. Versionnage du noyau et de la distribution sont distincts.
2. Le noyau est monolithique mais modulaire ; ses sous-systèmes (processus, mémoire, VFS, réseau, pilotes, sécurité, conteneurs) couvrent tout le spectre d'un OS de production.
3. Son évolution (SMP, 2.6, live patching, Rust, temps réel mainline, 7.0 en 2026) montre une trajectoire d'élargissement continu du matériel et des usages supportés, sans rupture architecturale.
4. La pile GPU (DRM/KMS côté noyau, Mesa côté utilisateur) et les piles de calcul (CUDA, ROCm, oneAPI) font de Linux le socle du calcul intensif, dont la simulation quantique.
5. Via IIO, GPIO, PREEMPT_RT, ROS et les cadres d'instrumentation, Linux est le pilote universel des capteurs, actionneurs et instruments, y compris des électroniques de contrôle quantique. C'est l'argument central de la présentation.

## 8. Limites et péremption

- Non couvert : détail des distributions, systemd et l'espace utilisateur, sécurité applicative, comparaison avec BSD/Windows.
- Péremption : les numéros de version récents (7.0, ordonnanceur, état de Rust et de PREEMPT_RT) évoluent ; revalider les jalons datés au-delà de 2026. Les fondamentaux d'architecture restent stables.
- Points d'appréciation signalés : l'importance relative attribuée à certaines versions (2.6, temps réel) reflète un consensus courant mais reste interprétatif.

## 9. Sources

- The Linux Kernel documentation, [architecture et sous-systèmes](https://docs.kernel.org/) ; Linux Kernel Labs, [introduction](https://linux-kernel-labs.github.io/refs/heads/master/lectures/intro.html).
- Wikipedia, [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel) et [Linux kernel version history](https://en.wikipedia.org/wiki/Linux_kernel_version_history) ; Kernel Newbies, [LinuxVersions](https://kernelnewbies.org/LinuxVersions).
- The Linux Kernel documentation, [GPU Driver Developer's Guide](https://dri.freedesktop.org/docs/drm/gpu.html) et [pilote i915](https://docs.kernel.org/gpu/i915.html) ; ArchWiki, [Kernel mode setting](https://wiki.archlinux.org/title/Kernel_mode_setting).
- Bootlin, [the backbone of a Linux Industrial I/O driver](https://bootlin.com/blog/the-backbone-of-a-linux-industrial-i-o-driver/) ; Analog Devices Wiki, [Linux Industrial I/O Subsystem](https://wiki.analog.com/software/linux/docs/iio/iio).
- Sur PREEMPT_RT et la robotique : [Real-Time Linux Kernels in Robotics (PREEMPT_RT)](https://medium.com/@hammadzahid1010/real-time-linux-kernels-in-robotics-why-preempt-rt-is-the-unsung-hero-of-autonomous-systems-b9edb871dff8) ; LinuxGizmos, [RT Linux et ROS 2](https://linuxgizmos.com/arm-based-robotics-module-and-gripper-bot-run-rt-linux-and-ros-2-0/).
