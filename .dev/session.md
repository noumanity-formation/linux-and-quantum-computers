# intention

 Écrire les harness file nécessires "CLAUDE.md" CONSTITUTION.md,  INTENTION.md, etc pour fixer la méthode de travail.

  Pour toute demande, doit tenir compte de 3 ingrédients:
  - l'intention,
  - le contexte, et
  - la spécification du livrable

Afin d'avoir un petit framework léger de travail augmenté par IA


# contexte

Voici comment j'aimerais pouvoir travailler:

  La gouvernance entre IA et humain se fait pas objection-sociocratique:

  - l'humain soumet le problème
  - l'agent IA propose une intervention sous forme d'un plan
  - avant exécution du plan, l'humain peut émettre des objections raisonnées
  - l'agent ne peut pas exécuter le plan tant qu'il y a des objections non résolus

La base de travail sont des documents livrables suivants:

- les plans
- les recherches de fondations
- le harnais (CLAUDE.md, CONSTITUTION.md et INTENTION.md)
- les skills. Chaque type de livrable a un skill asocié qui encadre la production de ce livrable. C'est une spécification+requirement vivante


L'humain n'a qu'un seul point d'entré: session.md  

Et les Objections sont renseignés dans le fichier session.md

L'Agent IA doit soulever des objections. Elles sont consignés dans le plan.

Le objections de l'humain sont consignés dans session.md



# Spécification des livrables


## Plan de travail

Déposé dans @.dev/plans/PLN-<XYZ>-<SLUG>.md

## Les harnais

- @CLAUDE.md
- @CONSTITUTION.md
- @INTENTION.md


## session.md

# Tâches

## 1. planification

Proposer un plan de travail dans le fichier @.dev/plans/PLN-001-setup-methodology.md

## 2. more planif

Prendre en compte les modification à ce document et étendre le plan en conséquense

## 3. réponse aux objections & précisions

- la dépendance FDN-001, donc retirez
- point 2: oui, les fichiers harnais peuvent être appellés à évoluer pour conrriger le comportement ou pour faire évoluer le concept. Ceci est un point central de la méthodologie. C'est fichiers ne sont pas écrits une fois, ils sont vivant et peuvent être appelés à changer. Même si typiquement leur cycle de vie est plus lent.
- point 3: oui. produire le skill plan de travail. On ne l'utilise pas en ce moment parce qu'il n'existe pas. Mais il faut le créer

Tous les livrables "artefact-de-travail" produient ont la même nomenclature et convention:

@.dev/<type>/<TYPE_PREFIX>-<SEQ>-<SLUG>.md

sauf dans les cas où on a de contraintes à respecter comme les skills qui utilisent la convention de skills de Claude

## 4. Exécuter le plan PLN-001

