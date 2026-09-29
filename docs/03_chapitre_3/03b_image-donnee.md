---
author: ELP
title: 03a Image
---

# Bloc A — L'image est un tableau de nombres

!!! abstract "Au programme"
    Pixel · niveaux de gris · listes de listes · coordonnées · couleurs RGB · résolution et définition

!!! info "Séance 1"
    Découvrir qu'une image, pour une machine, n'est rien d'autre qu'un tableau de nombres — et apprendre à s'y déplacer.

## <span style="color:#1565c0">Le pixel</span>

Approche ton œil très près d'un écran : l'image se décompose en minuscules carrés colorés. Chacun s'appelle un **pixel** (de l'anglais *picture element*).

!!! info "L'idée fondamentale"
    Une image numérique est une **grille de pixels**. À chaque pixel correspond un **nombre** (ou plusieurs, pour une image en couleur).

    Une image n'est donc pas « une photo » pour un ordinateur. C'est un **tableau de nombres**, exactement comme la table de données du module précédent.

## <span style="color:#1565c0">Les niveaux de gris</span>

Commençons par le plus simple : une image en noir et blanc, où chaque pixel vaut un nombre de **0** (noir) à **9** (blanc).

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

C'est une **liste de listes** : chaque élément de `image` est une **ligne**, elle-même une liste de pixels.

!!! example "Activité 1 — Afficher l'image"
    Sans écran graphique, on peut représenter chaque niveau par un caractère plus ou moins dense.

    ```python
    RAMPE = " .:-=+*#%@"

    def afficher(img):
        for ligne in img:
            texte = ""
            for pixel in ligne:
                texte = texte + RAMPE[pixel] * 2
            print(texte)


    afficher(image)
    ```

    Que vois-tu ?

??? success "Résultat"
    ```text
    @@@@::::::::@@@@
    @@::########::@@
    ::##  ####  ##::
    ::############::
    ::############::
    ::##        ##::
    @@::########::@@
    @@@@::::::::@@@@
    ```

    Un **visage** : deux yeux à la ligne 2, une bouche à la ligne 5.

    !!! tip "Comment ça marche"
        `RAMPE[pixel]` va chercher le caractère d'indice `pixel` dans la chaîne — c'est l'**indexation des chaînes** vue en M0. Le caractère est doublé (`* 2`) parce qu'un caractère est plus haut que large à l'écran ; sans cela, l'image serait aplatie.

        Les deux boucles imbriquées — une pour les lignes, une pour les pixels — sont la structure de **tous** les programmes de traitement d'image.

## <span style="color:#1565c0">Se repérer dans l'image</span>

!!! warning "L'ordre des indices surprend toujours"
    On écrit `image[y][x]` : **d'abord la ligne, ensuite la colonne**.

    C'est l'inverse des coordonnées mathématiques `(x, y)`. La raison est simple : `image` est une liste de **lignes**, donc le premier indice choisit une ligne.

    Autre différence : l'axe vertical est orienté **vers le bas**. Le pixel `[0][0]` est en haut à gauche.

!!! example "Activité 2 — Lire des pixels"
    Prédis chaque valeur, puis vérifie :

    ```python
    print(image[0][0])   # ?
    print(image[2][2])   # ?
    print(image[5][3])   # ?
    print(len(image))    # ?
    print(len(image[0])) # ?
    ```

??? success "Réponse"
    ```text
    9    coin haut-gauche : blanc
    0    l'œil gauche : noir
    0    la bouche : noir
    8    le nombre de lignes = la hauteur
    8    le nombre de colonnes = la largeur
    ```

    Retiens les deux dernières :

    ```python
    hauteur = len(image)
    largeur = len(image[0])
    ```

!!! question "À toi de jouer A.1 ⭐⭐ — Compter les pixels"
    Écris une fonction `dimensions(img)` qui affiche la largeur, la hauteur et le nombre total de pixels.

??? success "Corrigé"
    ```python
    def dimensions(img):
        hauteur = len(img)
        largeur = len(img[0])
        print(largeur, "x", hauteur, "=", largeur * hauteur, "pixels")


    dimensions(image)
    ```

    ```text
    8 x 8 = 64 pixels
    ```

!!! question "À toi de jouer A.2 ⭐⭐ — Compter les pixels noirs"
    Écris `compter(img, valeur)` qui compte combien de pixels valent exactement `valeur`. Combien de pixels noirs (`0`) dans notre visage ?

??? success "Corrigé"
    ```python
    def compter(img, valeur):
        total = 0
        for ligne in img:
            for pixel in ligne:
                if pixel == valeur:
                    total = total + 1
        return total


    print(compter(image, 0), "pixels noirs")
    ```

    ```text
    6 pixels noirs
    ```

    Deux yeux (2 pixels) et une bouche (4 pixels).

    On reconnaît le schéma **initialiser → parcourir → renvoyer** de M0, avec cette fois **deux boucles imbriquées** parce que la structure a deux dimensions.

## <span style="color:#1565c0">La couleur</span>

Un pixel de couleur ne se code pas avec un nombre, mais avec **trois** : les quantités de **rouge**, de **vert** et de **bleu** qui le composent. C'est le codage **RVB** (ou **RGB** en anglais).

Chaque composante va généralement de **0 à 255**.

| Couleur | R | V | B |
| --- | --- | --- | --- |
| Rouge | 255 | 0 | 0 |
| Vert | 0 | 255 | 0 |
| Bleu | 0 | 0 | 255 |
| Jaune | 255 | 255 | 0 |
| Blanc | 255 | 255 | 255 |
| Noir | 0 | 0 | 0 |

!!! info "Pourquoi ces trois couleurs ?"
    Parce que l'œil humain possède trois types de récepteurs sensibles à la couleur, dont les sensibilités maximales se situent approximativement dans le rouge, le vert et le bleu.

    Les écrans n'imitent donc pas la lumière réelle : ils imitent **ce que notre œil sait percevoir**. C'est une contrainte biologique devenue une norme technique.

!!! warning "Ne pas confondre avec la peinture"
    En peinture, mélanger le rouge et le vert donne un brun. Sur un écran, cela donne du **jaune**.

    La différence : un écran **émet** de la lumière et les couleurs s'additionnent ; une peinture **absorbe** la lumière et les couleurs se soustraient. Ce sont deux mécanismes opposés.

!!! example "Activité 3 — Une image couleur"
    ```python
    couleur = [
     [[255,0,0], [0,255,0], [0,0,255]],
     [[255,255,0], [255,255,255], [0,0,0]]]
    ```

    1. Quelles sont les dimensions de cette image ?
    2. Que vaut `couleur[0][1]` ? Et `couleur[1][0]` ?
    3. Combien de nombres au total contient-elle ?

??? success "Corrigé"
    1. **3 de large, 2 de haut** — 6 pixels.
    2. `couleur[0][1]` vaut `[0, 255, 0]`, du vert. `couleur[1][0]` vaut `[255, 255, 0]`, du jaune.
    3. 6 pixels × 3 composantes = **18 nombres**.

    On a maintenant **trois** niveaux d'indices : `couleur[y][x][c]`, où `c` vaut 0 pour le rouge, 1 pour le vert, 2 pour le bleu.

    ```python
    print(couleur[0][0][0])   # 255 : le rouge du premier pixel
    ```

!!! question "À toi de jouer A.3 ⭐⭐⭐ — De la couleur au gris"
    Pour convertir un pixel couleur en niveau de gris, on ne fait pas la moyenne des trois composantes : l'œil est **beaucoup plus sensible au vert** qu'au bleu. La formule usuelle est :

    `gris = 0,299 × R + 0,587 × V + 0,114 × B`

    Écris `vers_gris(pixel)` et applique-la à l'image couleur.

??? success "Corrigé"
    ```python
    def vers_gris(pixel):
        return round(0.299 * pixel[0] + 0.587 * pixel[1] + 0.114 * pixel[2])


    for ligne in couleur:
        resultat = []
        for pixel in ligne:
            resultat.append(vers_gris(pixel))
        print(resultat)
    ```

    ```text
    [76, 150, 29]
    [226, 255, 0]
    ```

    !!! tip "Ce que révèlent ces nombres"
        Le rouge pur donne 76, le vert pur 150, le bleu pur 29. **En noir et blanc, un vert paraît deux fois plus clair qu'un rouge, et cinq fois plus clair qu'un bleu.**

        Les coefficients ne sont pas arbitraires : ils décrivent la sensibilité de l'œil humain. Un choix technique qui encode une caractéristique biologique.

## <span style="color:#1565c0">Définition et résolution</span>

Deux mots souvent confondus.

| Terme | Ce que c'est | Unité |
| --- | --- | --- |
| **Définition** | le nombre total de pixels | 4032 × 3024 pixels |
| **Résolution** | le nombre de pixels par unité de longueur | points par pouce (ppp / dpi) |

!!! example "Activité 4 — Le même fichier, deux tailles"
    Une image de 4032 × 3024 pixels est affichée deux fois : sur un timbre-poste de 3 cm, puis sur une affiche de 3 m.

    1. Sa **définition** change-t-elle ?
    2. Sa **résolution** change-t-elle ?
    3. Laquelle des deux paraîtra nette ?

??? success "Corrigé"
    1. **Non** — c'est le même fichier, les mêmes 12 millions de pixels.
    2. **Oui** — sur 3 cm, les pixels sont minuscules et serrés ; sur 3 m, ils sont énormes et espacés.
    3. Le **timbre**. Sur l'affiche, on distinguerait les pixels à courte distance.

    !!! tip "L'erreur à ne plus commettre"
        « Augmenter la résolution » d'une image existante ne crée **aucune information nouvelle** : on ne peut pas inventer des détails qui n'ont jamais été enregistrés.

        Les outils qui prétendent le faire ne les inventent pas : ils les **fabriquent de façon plausible**. Nous verrons au bloc D ce que cela signifie exactement — et pourquoi c'est un vrai problème quand l'image sert de preuve.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc A"
    - Une image est une **grille de pixels**, donc un **tableau de nombres**.
    - En Python : une **liste de listes**, parcourue par deux boucles imbriquées.
    - On écrit `image[y][x]` — **ligne d'abord**, et l'axe vertical descend.
    - Une couleur se code par **trois** nombres : rouge, vert, bleu.
    - Le codage RVB imite non pas la lumière, mais **ce que l'œil sait percevoir**.
    - **Définition** = nombre de pixels ; **résolution** = pixels par unité de longueur.

