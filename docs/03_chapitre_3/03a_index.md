---
author: Elisabeth Le Prettre (LePrettre)
title: 03 Index
---


# Images numériques

## <span style="color:#1565c0">Pourquoi ce module ?</span>

Une image n'est pas une image, pour une machine : c'est un **tableau de nombres**. Comprendre cela change tout — car ce qui est un nombre peut être calculé, transformé, et **fabriqué de toutes pièces**.

Ce module va de la lumière qui entre dans un capteur jusqu'aux images générées par une intelligence artificielle.

!!! abstract "Objectifs du module"
    À la fin de ce module, tu sauras :

    - expliquer ce qu'est un **pixel** et comment se code une couleur ;
    - calculer le **poids** d'une image et comprendre à quoi sert la compression ;
    - écrire toi-même des **filtres** : négatif, seuillage, miroir ;
    - dire ce que révèlent les **métadonnées** d'une photo ;
    - expliquer, sans technicité excessive, comment une IA **génère** une image ;
    - connaître les repères juridiques : droit à l'image, droits d'auteur.

## <span style="color:#1565c0">Ce que tu réutilises</span>

| Vient de | Quoi |
| --- | --- |
| M0 bloc B | boucles imbriquées — indispensables pour parcourir une image |
| M0 bloc C | listes, listes de listes, fonctions |
| M0 bloc D | « une IA produit du plausible, pas du vrai » |
| M1 bloc A | poids en octets, formats, métadonnées |
| M1 bloc D | biais des données d'entraînement, donnée personnelle |

## <span style="color:#1565c0">Le découpage en séances</span>

**4 séances**, réparties en quatre blocs.

| # | Séance | Bloc |
| --- | --- | --- |
| 1 | L'image est un tableau de nombres | [A](03b_image-donnee.md) |
| 2 | De la lumière au fichier | [B](03c_capteur-et-fichier.md) |
| 3 | Transformer une image | [C](03d_transformer.md) |
| 4 | Images générées | [D](03e_images-generees.md) |

## <span style="color:#1565c0">L'image du module</span>

On travaille sur une image minuscule — **8 pixels sur 8** — pour pouvoir la lire entièrement à l'œil nu.

```python
image = [
 [9,9,2,2,2,2,9,9],
 [9,2,7,7,7,7,2,9],
 [2,7,0,7,7,0,7,2],
 [2,7,7,7,7,7,7,2],
 [2,7,7,7,7,7,7,2],
 [2,7,0,0,0,0,7,2],
 [9,2,7,7,7,7,2,9],
 [9,9,2,2,2,2,9,9]]
```

!!! tip "Pourquoi si petit ?"
    Une photo de téléphone contient plus de **douze millions** de pixels. Impossible d'observer ce qui s'y passe.

    Avec 64 pixels, tu vois **chaque nombre** et son effet. Les algorithmes que tu vas écrire sont exactement ceux qui tournent sur les vraies images : seule la taille change.

## <span style="color:#1565c0">Les blocs</span>

1. [Bloc A — L'image est un tableau de nombres](03b_image-donnee.md) — pixels, niveaux de gris, RGB, résolution
2. [Bloc B — De la lumière au fichier](03c_capteur-et-fichier.md) — capteur, poids, compression, métadonnées
3. [Bloc C — Transformer une image](03d_transformer.md) — négatif, seuillage, miroir, histogramme
4. [Bloc D — Images générées](03e_images-generees.md) — comment une IA fabrique une image, deepfakes, droit