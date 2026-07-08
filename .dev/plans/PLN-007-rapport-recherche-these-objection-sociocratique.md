# PLN-007 — Rapport de recherche : la thèse de l'objection-sociocratique comme règle unique

**Statut : résolu**

---

## Changelog

- **v1** : proposition initiale. Lecture du matériel préliminaire (transcript IA non vérifié), verdict provisoire sur la thèse fondé sur ce seul matériel, définition de FND-001/FND-002 nécessaires. Statut *objection* : refus de trancher a priori entre reformuler la thèse ou l'étayer.
- **v2** (courante) : l'humain tranche l'objection (session.md, tâche 14) — ne pas choisir a priori, **faire la recherche d'abord**. `FND-001` et `FND-002` produits avec sources vérifiées indépendamment (recherche web réelle, pas relecture du transcript). Verdict et critique de l'argumentaire ci-dessous mis à jour en conséquence. Conformément à la tâche 14, ce plan ne couvre pas la rédaction de l'article scientifique final (« sera fait plus tard ») — seulement le verdict et la critique demandés.

---

## Intention

Finaliser le rapport de recherche accompagnant la présentation (session.md, tâche « Finaliser la recherche », livrable « Rapport de recherche »). La thèse à étayer :

> « L'adoption de l'objection-sociocratique comme unique règle constitue un framework cohérent et complet pour le fonctionnement de communautés de pratiques intentionnées. »

Cette itération répond aux 5 points demandés : consulter la recherche préliminaire, définir les fondations nécessaires, dire si la thèse tient, critiquer l'argumentaire, et proposer un plan de rédaction — pas encore rédiger le rapport final lui-même.

## Contexte

### Recherche préliminaire consultée

`.dev/source-material/SRCM-001-analyse-avec-poe.com/linux-communaute-intention-vs-communaute-pratique` (879 lignes, transcript d'échange avec un assistant IA, pas une source académique primaire). Contenu : revue de littérature sur communautés de pratique (Lave & Wenger, Wenger-Trayner) et communautés d'intention (Kanter, Sargent, Metcalf) avec bibliographie ; panorama des théories et méthodes mobilisées pour les étudier ; positionnement de la sociocratie (généalogie Endenburg/cybernétique + Comte/Ward + Boeke/Quakers) et sa comparaison à l'holacratie ; étude de cas Linux ; revue des modèles de gouvernance organisée en 2 puis 9 familles d'axes (~28 axes, réductibles à 5-6).

**Limite de rigueur importante à documenter dans toute FND qui s'appuiera dessus** : c'est un transcript de conversation avec un assistant IA (Poe.com), qui **admet lui-même** ne pas pouvoir garantir la validité des URLs citées (« je ne peux pas naviguer sur le web [...] je ne peux pas garantir qu'une URL donnée soit aujourd'hui active »). Ce n'est donc pas en l'état une source vérifiée au sens de `skl-002-recherche-de-fondation » (« chaque fait clé est sourcé », « rigueur : qualité des sources »). Utilisable comme point de départ et comme carte conceptuelle, pas comme fondation citable telle quelle.

### La thèse tient-elle ?

**Verdict : non, pas telle qu'énoncée — elle tient à une condition qui n'est pas encore posée dans l'argumentaire.**

Le nœud du problème est que la thèse repose sur une catégorie composite, « communauté de **pratique intentionnée** », qui n'existe dans aucune des deux littératures consultées. Le matériel source établit au contraire, à deux reprises et de façon centrale, que **« nature du lien collectif » (pratique vs intention) et « mode de gouvernance » sont des dimensions analytiquement indépendantes** :

- le cas Linux y est traité comme la démonstration-limite de cette indépendance : Linux est un cas d'école de communauté de pratique (au sens de Wenger) mais **explicitement pas** une communauté d'intention (« Linux n'est donc pas une communauté d'intention ; c'est une communauté de pratique traversée par une couche intentionnelle mince, hétérogène et disputée ») — et sa gouvernance est méritocratique/BDFL, à l'opposé de la sociocratie ;
- la section sur les modèles de gouvernance généralise ce constat : sociocratie et *benevolent dictatorship* sont deux « types idéaux » qui occupent les pôles opposés d'un espace à ~28 axes (concentration, règle de veto, légitimité, frontière, pondération des voix, voix/sortie, etc.), et **rien dans le matériel n'établit qu'un seul de ces axes (le consentement/objection) suffise à couvrir les autres** pour un type de communauté donné.

Autrement dit, le matériel source soutient bien que la sociocratie est **empiriquement dominante** comme outil de gouvernance des communautés d'intention (écovillages, cohousing) — mais il ne soutient à aucun moment l'idée qu'elle serait **nécessaire et suffisante**, ni que son adoption comme **règle unique** couvre la complétude d'un système de gouvernance (frontière d'appartenance, redevabilité, formalisation, temporalité, etc. — les familles D à I du panorama des axes). La thèse, dans sa formulation actuelle, affirme une complétude qu'aucune des deux littératures consultées n'établit ; elle est plausible comme **conjecture à tester**, pas comme constat déjà étayé.

Ce que la thèse peut légitimement revendiquer, en l'état du matériel : que l'objection-sociocratique est un **candidat sérieux et documenté** pour gouverner des communautés qui combinent pratique et intention — pas qu'elle est *la* solution complète et unique par nature. Réviser la formulation (« un framework candidat/prometteur » plutôt que « cohérent et complet ») ou construire l'argument manquant (pourquoi *cette* catégorie composite spécifique n'a besoin que d'*une* règle, quand la littérature générale sur la gouvernance en identifie des dizaines d'axes) est un préalable à la rédaction du rapport.

### Critique de l'argumentaire (session.md, tâche « Finaliser la recherche »)

Point par point :

1. **« Toutes les communautés sont des communautés de pratique ET d'intention »** — affirmation universelle non étayée, et **contredite frontalement** par le matériel source lui-même sur son propre exemple central (Linux, explicitement qualifié de communauté de pratique *sans* être une communauté d'intention). Si ce point d'ancrage tombe, toute la suite de l'argumentaire (qui s'appuie sur Linux comme cas) doit être reformulée : soit on restreint la thèse à un sous-ensemble de communautés (celles qui *ont effectivement* les deux dimensions), soit on argumente pourquoi Linux serait un contre-exemple mal interprété par le matériel source — mais cela ne peut pas rester une affirmation de départ non discutée.
2. **Stallman = communauté d'intention explicite** — cohérent avec le matériel source (intention éthique/politique forte, explicite, fondatrice). Point solide.
3. **« Beaucoup de communautés n'explicitent pas leur intention, mais TOUTES en ont une, sans quoi la communauté ne tient pas »** — reformulation plus forte encore du point 1 (passe de « toutes ont pratique+intention » à « l'intention est la condition de tenue de toute communauté »), toujours sans source. C'est une affirmation testable (elle prédit que les communautés de pratique « pures » sans couche intentionnelle devraient se dissoudre) que le matériel source ne teste pas.
4. **Torvalds aurait « adapté sa gouvernance » à une intention différente de celle de Stallman, exactement le même pattern que Stallman (outil + licence + fondation)** — partiellement soutenu (git, licence, Linux Foundation existent bien ; l'intention pragmatique de Torvalds est documentée) mais la symétrie « exactement le même pattern » surinterprète : le matériel source qualifie la couche intentionnelle de Torvalds de « mince, hétérogène, disputée », à l'opposé du caractère « explicite et clairement assumé » que l'argumentaire attribue lui-même à Stallman au point 2. Présenter les deux comme un seul et même pattern efface la différence que l'argumentaire vient d'établir.
5. **« L'erreur de Torvalds a été de croire qu'il n'avait pas d'intention idéologique ; son intention est de créer un produit industriel révolutionnaire »** — reformulation intéressante mais interprétative, non sourcée dans le matériel consulté ; à traiter comme hypothèse de l'auteur, pas comme fait établi.
6. **« Torvalds a réussi son intention et sa communauté l'a bien intégrée »** — plausible mais non démontré dans le matériel (aucune donnée sur l'« intégration » par la communauté).
7. **« Sa structure de gouvernance (Benevolent Dictatorship) met en péril la viabilité à long terme de Linux »** — c'est l'affirmation la **plus fragile** de l'argumentaire. Le matériel source ne dit rien de tel : il présente au contraire le BDFL comme un « type idéal » cohérent et *vivable*, précisément parce que le droit de sortie (*fork*) y joue le rôle de garde-fou que le consentement joue dans la sociocratie — pas comme un modèle en péril. Affirmer sa fragilité nécessite une preuve distincte (ex. : absence de plan de succession documentée, tensions récentes de gouvernance dans le noyau, burnout des mainteneurs) qui n'est pas apportée. C'est actuellement l'affirmation la plus **exposée à une objection humaine ou externe** si le rapport final la reprend telle quelle.

### Verdict final, informé par les fondations (v2)

`FND-001` et `FND-002` ont été produites avec des sources vérifiées indépendamment (recherche web réelle, pas relecture du transcript IA). Elles **confirment le diagnostic v1 sur le fond, tout en le nuançant sur un point précis** :

- **Points 1 et 3 de la critique (universalité « toute communauté a besoin d'une intention commune ») : confirmés infondés, avec un niveau de preuve renforcé.** `FND-001` ne trouve, dans la littérature vérifiée, aucune catégorie académique de « communauté de pratique intentionnée », et surtout : l'étude la plus directement pertinente qui reteste empiriquement la théorie de Kanter sur des communautés intentionnelles contemporaines (Rubin, Willis & Ludwig, 2019) trouve les mécanismes d'engagement, y compris idéologiques, **faiblement présents** — même dans l'échantillon le plus favorable à la thèse. L'affirmation universelle de l'argumentaire ne tient pas.
- **Point 7 (BDFL met en péril Linux) : la critique v1 était trop catégorique dans l'autre sens.** `FND-002` trouve un niveau de preuve **faible à modéré, pas absent** : deux départs documentés de mainteneurs clés sur le dossier Rust for Linux en 2024-2025 (Wedson Almeida Filho, Hector Martin), explicitement attribués au style de gouvernance de Torvalds ; un tout premier plan de succession formel adopté en 2025 après plus de 30 ans sans mécanisme de continuité documenté ; le précédent Python (transition BDFL de van Rossum en 2018) montrant qu'une telle transition a un coût réel et mesurable (gel de plusieurs mois des décisions majeures). **Ni l'affirmation initiale (« péril pour la viabilité ») ni son rejet pur et simple ne sont défendables** : la formulation à retenir pour le rapport final est « coûts de gouvernance réels et récents » + « point de défaillance unique resté sans plan de continuité pendant l'essentiel de l'histoire du projet », pas « péril ».

**Conclusion globale, désormais fondée sur sources vérifiées plutôt que sur le seul matériel préliminaire** : la thèse ne tient pas dans sa formulation actuelle (« framework cohérent et complet »), pour la raison structurelle déjà identifiée en v1 (catégorie composite non établie, complétude non démontrée face à un espace de gouvernance à ~28 axes) — un diagnostic que la recherche indépendante **renforce** plutôt qu'elle ne l'infirme. Le point empirique le plus attaquable de l'argumentaire (l'affirmation sur le péril du BDFL) est en revanche **partiellement récupérable** moyennant reformulation : les deux fondations ouvrent la voie à une version révisée, plus modeste et mieux défendable, de la thèse et de l'argumentaire — pas à leur abandon.

### Fondations nécessaires

Deux `FND` distincts, pas un seul, car les questions à traiter sont de nature différente (l'une conceptuelle, l'autre empirique) :

- **FND-001 — « Communauté de pratique intentionnée » : définition et statut conceptuel.** Objectif : construire et justifier (ou infirmer) la catégorie composite au cœur de la thèse, en s'appuyant sur Wenger/Lave, Kanter/Sargent/Metcalf et sur l'indépendance pratique/intention établie par le cas Linux du matériel source — en vérifiant/complétant les sources primaires (le matériel source n'est pas citable tel quel, voir limite de rigueur ci-dessus).
- **FND-002 — Le *Benevolent Dictatorship* de Linux : viabilité à long terme, état des lieux.** Objectif : vérifier empiriquement l'affirmation n°7 ci-dessus (recherche de sources primaires sur la gouvernance récente du noyau Linux : succession, tensions documentées, avis de mainteneurs) — condition pour pouvoir conserver ou devoir amender cette affirmation dans le rapport final.

## Spécification du livrable

- `.dev/fondations/FND-001-communaute-pratique-intentionnee.md` et `.dev/fondations/FND-002-bdfl-linux-viabilite.md` (`skl-002-recherche-de-fondation`).
- `Rapport de recherche` final — au sens de la table des livrables de `CLAUDE.md`, c'est une recherche de fondation (`.dev/fondations/FND-003-rapport-recherche-objection-sociocratique.md` ou renommé selon le titre retenu), qui s'appuie sur FND-001 et FND-002 et statue explicitement sur la thèse (la confirme, la restreint, ou la reformule) et répond point par point à la critique de l'argumentaire ci-dessus.

## Plan proposé

### 1. Trancher le statut de la thèse et de l'argumentaire (décision humaine requise)
Avant de lancer FND-001/002 : la thèse doit-elle être reformulée maintenant (ex. « framework candidat » plutôt que « cohérent et complet »), ou les fondations doivent-elles chercher à construire l'argument manquant pour la sauver telle quelle ? Ce choix détermine l'angle des deux FND. Voir objection 1.

### 2. Produire FND-001 (communauté de pratique intentionnée) — fait
Sources vérifiées indépendamment (Lave & Wenger 1991, Wenger 1998, Kanter 1972 — une erreur d'ISBN du matériel préliminaire y a été détectée et corrigée —, Sargent 1994, Metcalf 2004), plus recherche ciblée sur le terrain empirique du croisement pratique/intention. Voir « Verdict final » ci-dessus.

### 3. Produire FND-002 (BDFL Linux, viabilité) — fait
Recherche empirique (succession, tensions Rust for Linux 2024-2025, comparaison Python/WordPress). Voir « Verdict final » ci-dessus.

### 4. Rédiger le rapport de recherche final — hors périmètre de ce plan
Conformément à `.dev/session.md` (tâche 14) : « le plan ne concerne que la rédaction d'un article scientifique qui nécessitera plus de travail et qui sera fait plus tard ». Reporté à une itération distincte, avec son propre cycle objection-sociocratique, une fois la thèse et l'argumentaire reformulés à la lumière du verdict ci-dessus.

### 5. Validation humaine
Objection 1 (v1) résolue par la décision de l'humain (tâche 14 : faire la recherche avant de trancher, plutôt que choisir a priori entre reformuler ou étayer). Le verdict et la critique ci-dessus répondent aux 4 premiers points demandés en tâche 13/14. Reste ouverte la décision de reformulation de la thèse elle-même avant toute rédaction — décision humaine, pas agent.

---

## Objections de l'agent IA

1. ~~La thèse n'est pas soutenue par le matériel préliminaire, et le choix entre reformuler/étayer n'appartient pas à l'agent~~ — **résolu** : l'humain a tranché (tâche 14) qu'il fallait faire la recherche d'abord plutôt que choisir a priori ; fait, verdict rendu ci-dessus.
2. ~~L'affirmation n°7 (BDFL met en péril Linux) est la plus exposée pour un public averti~~ — **résolu** : `FND-002` fournit un niveau de preuve réel (faible à modéré) et une reformulation défendable (« coûts de gouvernance réels », pas « péril »).
3. **Nouvelle objection non bloquante** : la thèse énoncée en tâche 13 (« framework cohérent et complet ») reste, après recherche, non défendable telle quelle — voir « Verdict final ». Si une future itération rédige l'article sans amender l'énoncé de la thèse elle-même, le rapport final répétera une affirmation que ses propres fondations ne soutiennent pas. Ce n'est pas bloquant pour *ce* plan (dont le périmètre s'arrête au verdict, par instruction explicite de la tâche 14), mais devra être tranché avant la tâche de rédaction.

_Aucune objection bloquante sur le périmètre de ce plan (verdict + critique). L'objection 3 concerne la future itération de rédaction, pas celle-ci._

---

## Note sur les objections humaines

Les objections de l'humain sur ce plan ne sont pas consignées ici mais dans `.dev/session.md`.
