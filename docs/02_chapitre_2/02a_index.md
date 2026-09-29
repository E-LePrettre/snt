---
author: Elisabeth Le Prettre (LePrettre)
title: 02 Index
---

# M1 — Les données

## <span style="color:#1565c0">Pourquoi ce module ?</span>

Tout ce que fait le numérique repose sur des **données** : ce que tu publies, ce que mesure un capteur, ce sur quoi une intelligence artificielle s'entraîne. Comprendre ce qu'est une donnée — comment on la structure, ce qu'elle vaut, ce qu'elle révèle — est la clé de tous les modules qui suivent.

!!! abstract "Objectifs du module"
    À la fin de ce module, tu sauras :

    - reconnaître un **format de données** (CSV, JSON) et dire ce que représente une colonne ;
    - **traiter** un vrai jeu de données avec les fonctions que tu as écrites en M0 ;
    - **filtrer**, **trier** et **compter** pour répondre à une question ;
    - construire un graphique et surtout le **lire de façon critique** ;
    - repérer un **biais** dans un jeu de données ;
    - dire ce qu'est une **donnée personnelle** et pourquoi l'anonymisation est plus difficile qu'elle n'en a l'air.

## <span style="color:#1565c0">Ce que tu réutilises de M0</span>

Ce module ne repart pas de zéro. Les fonctions que tu as écrites en fin de module précédent servent ici **telles quelles** :

| Fonction de M0 | Usage en M1 |
| --- | --- |
| `moyenne(liste)` | moyenne d'une colonne |
| `maximum(liste)` | valeur record d'une colonne |
| `nb_admis(liste)` | compter les valeurs au-dessus d'un seuil |
| l'anonymisation d'un prénom | bloc D — et on découvrira ses limites |

!!! tip "Si tu as oublié"
    Retourne voir le [bloc C de M0](../01_chapitre_1/01d_listes.md). Tu n'as pas besoin de les réécrire : copie-les au début de ton programme.

## <span style="color:#1565c0">Le découpage en séances</span>

Le module se déroule sur **6 séances**, réparties en quatre blocs.

| # | Séance | Bloc |
| --- | --- | --- |
| 1 | Qu'est-ce qu'une donnée ? | [A](02b_qu-est-ce-qu-une-donnee.md) |
| 2 | Traiter un jeu de données | [B](02c_traiter.md) |
| 3 | Interroger : filtrer, trier, compter | [B](02c_traiter.md) |
| 4 | Visualiser et interpréter | [C](02d_visualiser.md) |
| 5 | Quand les données trompent | [D](02e_biais-et-protection.md) |
| 6 | Protéger les données | [D](02e_biais-et-protection.md) |

## <span style="color:#1565c0">Le jeu de données du module</span>

On travaille toute l'année sur le même type de données, mais on change d'échelle. En M0, c'était une liste de notes. Ici, c'est un **tableau** :

```text
prenom,maths,francais,ecran
Camille,12,14,180
Lou,8,11,240
Mohamed,15,13,90
...
```

Quatre colonnes : un prénom, deux notes, et un temps d'écran quotidien en minutes.

!!! warning "Ces données sont fictives — et c'est important"
    Elles ressemblent à des données réelles d'élèves : des noms, des résultats scolaires, une habitude personnelle. Si elles l'étaient, on n'aurait **pas le droit** de les utiliser ainsi.

    Pourquoi, exactement ? C'est la question du bloc D.

## <span style="color:#1565c0">Les blocs</span>

1. [Bloc A — Qu'est-ce qu'une donnée ?](02b_qu-est-ce-qu-une-donnee.md) — types, tables, formats CSV et JSON
2. [Bloc B — Traiter un jeu de données](02c_traiter.md) — lire, extraire, filtrer, trier, compter
3. [Bloc C — Visualiser et interpréter](02d_visualiser.md) — construire un graphique, et le lire de façon critique
4. [Bloc D — Biais, protection et souveraineté](02e_biais-et-protection.md) — échantillons trompeurs, données personnelles, RGPD