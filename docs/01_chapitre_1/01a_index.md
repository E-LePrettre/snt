---
author: Elisabeth Le Prettre (LePrettre)
title: 01 Index
---

# M0 — Programmer : de la donnée à l'algorithme

## <span style="color:#1565c0">Pourquoi ce module ?</span>

Ce module est le **point de départ** de l'année de SNT. Tous les thèmes qui suivent — les données, les images, les réseaux sociaux, l'intelligence artificielle — supposent de savoir représenter une information et écrire un algorithme qui la traite.

!!! note "Le langage n'est pas le sujet"
    Ce module porte sur des **notions** : représenter une donnée, écrire un algorithme, traiter un jeu de données, porter un regard critique sur un programme. C'est le socle de la **pensée informatique et algorithmique** — décomposer un problème, le résoudre par étapes — que l'on consolidera dans tous les chapitres.

    Le langage utilisé cette année pour les mettre en pratique est **Python**, et l'environnement est **Basthon** ou **Capytale**. Ce sont des outils, choisis parce qu'ils sont simples et gratuits. Ils pourraient changer sans que le contenu du module change.

!!! abstract "Objectifs du module"
    À la fin de ce module, tu sauras :

    - stocker une information dans une **variable** et faire des calculs ;
    - **dialoguer** avec l'utilisateur et manipuler du texte ;
    - faire prendre une **décision** à un programme ;
    - **répéter** un traitement autant de fois que nécessaire ;
    - ranger des données dans une **liste** et écrire tes propres **fonctions** ;
    - **vérifier** un programme produit par une intelligence artificielle, et comprendre ce qu'elle sait et ne sait pas faire.

## <span style="color:#1565c0">Le fil rouge : les données de la classe</span>

Tout au long du module, on travaille sur un même jeu de données : **les prénoms et les notes d'une classe**. Séance après séance, le programme grandit.

| Séance | Ce qu'on ajoute | Le programme sait… |
| --- | --- | --- |
| 1 | Variables, affectation, calculs | stocker une note, calculer le poids d'une image |
| 2 | `input`, conversions | demander deux notes et calculer une moyenne |
| 3 | Chaînes de caractères | anonymiser un prénom |
| 4 | `if / elif / else` | attribuer une mention |
| 6 | `while` | saisir des notes jusqu'à un signal d'arrêt |
| 7 | Listes, fonctions | transformer la mention en fonction réutilisable |
| 8 | Projet | produire le bulletin complet d'une classe |

!!! tip "Où va-t-on ensuite ?"
    La liste de notes et la fonction `moyenne()` construites en séance 5 seront **réutilisées telles quelles** dans le module *Données*. Ce module n'est pas un hors-d'œuvre : c'est la boîte à outils de toute l'année.

## <span style="color:#1565c0">Le découpage en séances</span>

Le module se déroule sur **10 séances**, réparties en quatre blocs.

| # | Séance | Page |
| --- | --- | --- |
| 1 | Prise en main, variables et calculs | [1](1-bases.md) |
| 2 | Dialoguer avec l'utilisateur | [1](1-bases.md) |
| 3 | Les chaînes de caractères | [1](1-bases.md) |
| 4 | Les conditions | [2](2-conditions.md) |
| 5 | La boucle `for` | [2](2-conditions.md) |
| 6 | La boucle `while` | [2](2-conditions.md) |
| 7 | Listes et fonctions | [3](3-listes.md) |
| 8 | Projet et bilan | [3](3-listes.md) |
| 9 | Vérifier un code produit par une IA | [D](D-programmer-avec-ia.md) |
| 10 | Biais, coût, usage éclairé | [D](D-programmer-avec-ia.md) |

Les exercices notés ⭐⭐⭐ servent de parcours d'approfondissement : on les prend dès qu'on a terminé les autres.

## <span style="color:#1565c0">L'environnement de travail</span>

Pour travailler en Python, nous utiliserons principalement **deux outils complémentaires** :

* **Basthon** (`basthon.fr`) pour tester rapidement du code directement dans le navigateur, sans rien installer ;
* **Capytale** pour réaliser certaines activités, exercices et travaux demandés par l'enseignante. Capytale permet notamment de **retrouver son travail, de l'enregistrer et de le transmettre à l'enseignante**.

!!! note "🔄 Capsule d'actualité — l'outil n'est pas le programme"
Basthon et Capytale sont les environnements retenus cette année car ils permettent de programmer directement dans le navigateur, sans installation particulière.

```
Ces outils peuvent évoluer ou être remplacés au fil des années. Si nous devions utiliser demain Thonny, VS Code ou un autre environnement, **les notions de programmation étudiées resteraient exactement les mêmes**.

C'est une idée importante en informatique : **on apprend à programmer en Python, pas à utiliser un logiciel particulier**.
```

### Deux espaces à distinguer dans Basthon

* l'**éditeur de script** : on y écrit un programme composé de plusieurs instructions, puis on l'exécute ;
* la **console** (avec les chevrons `>>>`) : on y teste rapidement une instruction ou une expression, une ligne à la fois.

!!! note "Console ou éditeur ?"
Pour **tester rapidement une instruction ou une fonction**, la console est très pratique.

```
Pour **écrire un programme composé de plusieurs lignes**, on utilise l'éditeur ou une activité Capytale.
```

### Et Capytale ?

Lorsque le cours indique une **activité Capytale**, il faut utiliser le lien ou le code fourni par l'enseignante.

Dans Capytale, tu peux :

* écrire et exécuter du code Python ;
* compléter les exercices proposés ;
* conserver ton travail ;
* reprendre une activité plus tard ;
* permettre à l'enseignante de consulter ton avancement et ton travail.

!!! tip "💡 À retenir"
**Basthon = tester et expérimenter rapidement.**
**Capytale = réaliser et conserver les activités du cours.**

```
Dans les deux cas, le plus important reste le même : **comprendre le programme que tu écris et être capable d'expliquer ce qu'il fait.**
```


## <span style="color:#1565c0">Comment lire les pages du cours</span>

!!! example "Activité"
    Une manipulation guidée : on te donne un code, tu le testes et tu observes.

!!! question "À toi de jouer"
    Un exercice à chercher seul·e. Le niveau est indiqué : ⭐ découverte · ⭐⭐ application · ⭐⭐⭐ approfondissement.

??? success "Corrigé"
    Les corrigés sont repliés. **Cherche d'abord** — un corrigé lu trop tôt ne sert à rien.

## <span style="color:#1565c0">Les pages</span>

1. [Bloc A — Représenter une donnée](01b_bases.md) — variables, calculs, saisie, chaînes
2. [Bloc B — Écrire un algorithme](01c_conditions.md) — `if`, `for`, `while`
3. [Bloc C — Traiter un jeu de données](01d_listes.md) — listes, `def`, projet
4. [Bloc D — Programmer avec une IA](01e_ia.md) — vérifier un code généré, biais, coût, CRCN
