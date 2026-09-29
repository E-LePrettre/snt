---
author: Elisabeth Le Prettre (LePrettre)
title: 04 Index
---

# Réseaux sociaux

## <span style="color:#1565c0">Pourquoi ce module ?</span>

Tu utilises des réseaux sociaux tous les jours. Ce module ne cherche pas à te dire ce que tu dois en penser : il cherche à te montrer **comment ils fonctionnent**, pour que tu puisses en juger toi-même.

Trois questions le structurent :

- Comment représente-t-on un réseau de relations ?
- **Qui décide de ce que tu vois** dans ton fil ?
- À quoi sert tout cela, et pour qui ?

!!! abstract "Objectifs du module"
    À la fin de ce module, tu sauras :

    - modéliser un réseau par un **graphe** et calculer un degré, une distance ;
    - écrire toi-même un **algorithme de recommandation** ;
    - montrer que l'ordre d'un fil dépend de ce qu'on décide d'**optimiser** ;
    - expliquer le **modèle économique** d'une plateforme gratuite ;
    - comprendre pourquoi une fausse information circule plus vite qu'un démenti ;
    - connaître le **droit applicable** en ligne.

## <span style="color:#1565c0">Ce que tu réutilises</span>

| Vient de | Quoi |
| --- | --- |
| M0 bloc B | boucles, conditions, la croissance exponentielle du pliage |
| M0 bloc C | listes, fonctions, tri par sélection |
| M0 bloc D | ce qui est fréquent dans les données devient la réponse par défaut |
| M1 bloc C | corrélation n'est pas causalité, lecture critique d'un graphique |
| M1 bloc D | donnée personnelle, valeur des données, biais |

## <span style="color:#1565c0">Le découpage en séances</span>

**6 séances**, réparties en quatre blocs.

| # | Séance | Bloc |
| --- | --- | --- |
| 1 | Modéliser un réseau | [A](04b_modeliser.md) |
| 2 | Se déplacer dans un graphe | [A](04b_modeliser.md) |
| 3 | Qui décide de ce que tu vois ? | [B](04c_recommander.md) |
| 4 | L'économie de l'attention | [C](04d_attention.md) |
| 5 | Pourquoi le faux circule vite | [D](04e_desinformation-et-droit.md) |
| 6 | Droit et responsabilité | [D](04e_desinformation-et-droit.md) |

## <span style="color:#1565c0">Le réseau du module</span>

On travaille sur les mêmes dix élèves qu'au module *Les données*, avec cette fois leurs relations d'amitié :

```python
eleves = ["Camille", "Lou", "Mohamed", "Sarah", "Tom",
          "Ines", "Noah", "Lea", "Gabriel", "Jade"]

liens = [["Camille", "Lou"], ["Camille", "Mohamed"], ["Camille", "Ines"],
         ["Lou", "Sarah"], ["Mohamed", "Sarah"], ["Mohamed", "Tom"],
         ["Sarah", "Ines"], ["Tom", "Noah"], ["Ines", "Lea"],
         ["Noah", "Gabriel"], ["Lea", "Jade"], ["Gabriel", "Jade"]]
```

!!! question "Une question posée maintenant, à laquelle on répondra plus tard"
    *Où sont stockées tes publications, et qui décide de l'ordre de ton fil ?*

    Ce module répond à la seconde moitié. Le module *Internet et le Web* répondra à la première, et le module *Intelligence artificielle* reviendra sur les deux.

## <span style="color:#1565c0">Les blocs</span>

1. [Bloc A — Modéliser un réseau](04b_modeliser.md) — graphes, degré, distance, effet petit monde
2. [Bloc B — Qui décide de ce que tu vois ?](04b_modeliser.md) — recommandation, ordre du fil
3. [Bloc C — L'économie de l'attention](04c_recommander.md) — gratuité, publicité, valeur des données
4. [Bloc D — Désinformation, droit et responsabilité](04e_desinformation-et-droit.md) — viralité, bulles, droit en ligne