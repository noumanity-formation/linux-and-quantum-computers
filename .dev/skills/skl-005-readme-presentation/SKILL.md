---
name: skl-005-readme-presentation
description: >-
  Produire ou vérifier un README.md de présentation (`README.md` à la racine du dépôt de la
  présentation concernée) : titre, résumé, bio des auteurs, fiche entreprise. À utiliser quand
  une tâche demande de rédiger ou de vérifier le README accompagnant une présentation publique
  (conférence, meetup). Le README est le plus souvent rédigé par un humain ; ce skill couvre
  aussi bien sa production par l'agent que sa vérification d'un texte déjà écrit.
---

# Skill - README de présentation

> Un README de présentation annonce et contextualise une intervention publique (titre, résumé, auteurs, entreprise). Ce skill encadre sa production **et** sa vérification par l'agent, le second cas étant le plus fréquent.

## Quand l'utiliser

Quand une tâche demande d'écrire ou de vérifier le `README.md` d'un dépôt de présentation (conférence, meetup, événement professionnel). Ne pas confondre avec un README de dépôt logiciel classique (documentation d'installation/usage d'un projet) : ce skill couvre uniquement le README qui *annonce* une présentation. Par défaut, préférer le mode **vérification** (un humain rédige, l'agent contrôle la conformité au patron) sauf demande explicite de rédaction complète par l'agent.

## Processus

1. Identifier le contexte de la présentation : titre, événement, date, auteurs — depuis `session.md` ou les instructions de la tâche.
2. Déterminer le mode : **production** (rédiger de zéro) ou **vérification** (contrôler un README déjà écrit par un humain).
3. En mode production : rédiger les quatre sections obligatoires dans l'ordre du patron (titre, résumé, auteurs, fiche entreprise — voir Structure du livrable).
4. En mode vérification : comparer le README existant section par section contre le patron ; **signaler** les sections manquantes, incomplètes ou mal placées plutôt que les réécrire d'autorité sans validation humaine.
5. Résumé/abstract : 2-3 paragraphes narratifs, sans jargon non expliqué, qui posent le sujet, l'angle et l'enjeu de la présentation.
6. Section Auteurs : un sous-titre par auteur (nom, rôle), un lien professionnel (LinkedIn ou équivalent), une bio courte (2-4 paragraphes).
7. Section Fiche entreprise : nom, activité, positionnement en une ou deux phrases, lien — **distincte** de la bio des auteurs (ne pas la laisser noyée dans une bio individuelle).
8. Exclure ou signaler tout contenu périssable non vérifié (ex. URLs d'images à jetons temporaires) plutôt que de le reconduire sans validation.

## Critères de qualité

- Les quatre sections obligatoires sont présentes : titre, résumé, auteurs, fiche entreprise.
- Chaque auteur listé a un rôle et une bio, pas seulement un nom.
- La fiche entreprise est une section à part, pas une mention noyée dans une bio d'auteur.
- En mode vérification, le rapport produit signale les écarts section par section et ne modifie pas le fichier sans validation humaine explicite.
- Aucune URL à contenu périssable (jeton d'expiration, lien temporaire) n'est introduite sans le signaler.
- Markdown strict (voir `CLAUDE.md`).

## Structure du livrable

- **Emplacement** : `README.md` à la racine du dépôt de la présentation concernée (pas un artefact-de-travail : pas de préfixe/séquence, un README = un fichier standard).

```markdown
# <Titre accrocheur de la présentation>

Présentation préparée pour [<Événement>](<lien>), édition du <date>.

## Résumé

<Abstract narratif, 2-3 paragraphes : sujet, angle, enjeu.>

## Auteurs

### [<Nom>](<lien LinkedIn ou équivalent>) - <Rôle>

<img src="<url photo>" alt="<Nom>" width="200" />

<Bio, 2-4 paragraphes.>

## Entreprise

### [<Nom entreprise>](<lien>)

<Positionnement en une ou deux phrases : activité, spécialité.>
```
