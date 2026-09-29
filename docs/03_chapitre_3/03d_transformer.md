---
author: Elisabeth Le Prettre (LePrettre)
title: 03c Transformer
---


# Bloc C — Transformer une image

!!! abstract "Au programme"
    Négatif · éclaircir · seuillage · miroir · histogramme · détecter une retouche

!!! info "Séance 3"
    Une image est un tableau de nombres. Transformer une image, c'est donc simplement **calculer sur des nombres**.

!!! tip "La structure de tout ce bloc"
    Tous les filtres suivent le même patron :

    ```python
    def filtre(img):
        resultat = []
        for ligne in img:
            nouvelle_ligne = []
            for pixel in ligne:
                nouvelle_ligne.append(...)   # le calcul change ici
            resultat.append(nouvelle_ligne)
        return resultat
    ```

    Seule la ligne du calcul change. Une fois ce patron acquis, tous les filtres se ressemblent.

    Note qu'on construit une **nouvelle** image plutôt que de modifier l'ancienne : la règle du module précédent — une fonction n'abîme pas ce qu'on lui donne — s'applique ici aussi.

## <span style="color:#1565c0">Le négatif</span>

Inverser une image : ce qui était clair devient sombre, et réciproquement.

Avec des valeurs de 0 à 9, l'inverse de `p` est `9 - p`.

!!! question "À toi de jouer C.1 ⭐⭐"
    Écris `negatif(img)` et affiche le résultat.

??? success "Corrigé"
    ```python
    def negatif(img):
        resultat = []
        for ligne in img:
            nouvelle = []
            for pixel in ligne:
                nouvelle.append(9 - pixel)
            resultat.append(nouvelle)
        return resultat


    afficher(negatif(image))
    ```

    ```text
        ########
      ##::::::::##
    ##::@@::::@@::##
    ##::::::::::::##
    ##::::::::::::##
    ##::@@@@@@@@::##
      ##::::::::##
        ########
    ```

    Le visage est toujours là, en inversé : le fond blanc est devenu sombre, les yeux et la bouche sont devenus clairs.

    !!! tip "Une opération réversible"
        Appliquer `negatif` deux fois redonne l'image de départ : `9 - (9 - p) = p`.

        C'est une transformation **sans perte** — au sens du bloc B : aucune information n'est détruite.

## <span style="color:#1565c0">Éclaircir et assombrir</span>

!!! question "À toi de jouer C.2 ⭐⭐"
    Écris `eclaircir(img, n)` qui ajoute `n` à chaque pixel.

    **Attention :** les valeurs doivent rester entre 0 et 9.

??? success "Corrigé"
    ```python
    def eclaircir(img, n):
        resultat = []
        for ligne in img:
            nouvelle = []
            for pixel in ligne:
                valeur = pixel + n
                if valeur > 9:
                    valeur = 9
                nouvelle.append(valeur)
            resultat.append(nouvelle)
        return resultat


    afficher(eclaircir(image, 2))
    ```

    ```text
    @@@@========@@@@
    @@==@@@@@@@@==@@
    ==@@::@@@@::@@==
    ==@@@@@@@@@@@@==
    ==@@@@@@@@@@@@==
    ==@@::::::::@@==
    @@==@@@@@@@@==@@
    @@@@========@@@@
    ```

!!! danger "Éclaircir détruit de l'information"
    Regarde les valeurs. Avant : le fond vaut 9, le contour vaut 7. Après `eclaircir(image, 2)` : le fond vaut toujours 9 (plafonné), le contour vaut 9 aussi.

    **Deux valeurs différentes sont devenues identiques.** Assombrir ensuite de 2 ne les séparera plus : elles sont confondues pour toujours.

    C'est une transformation **avec perte**, comme la compression JPEG du bloc B. Et c'est la raison pour laquelle on ne peut pas « rattraper » une photo surexposée : l'information n'a jamais été enregistrée.

!!! question "À toi de jouer C.3 ⭐⭐ — Vérifier la perte"
    Écris un programme qui applique `eclaircir(image, 2)` puis assombrit de 2, et compare le résultat à l'image d'origine. Combien de pixels ont changé définitivement ?

??? success "Corrigé"
    ```python
    def assombrir(img, n):
        resultat = []
        for ligne in img:
            nouvelle = []
            for pixel in ligne:
                valeur = pixel - n
                if valeur < 0:
                    valeur = 0
                nouvelle.append(valeur)
            resultat.append(nouvelle)
        return resultat


    aller_retour = assombrir(eclaircir(image, 2), 2)

    perdus = 0
    for y in range(len(image)):
        for x in range(len(image[0])):
            if image[y][x] != aller_retour[y][x]:
                perdus = perdus + 1

    print(perdus, "pixels définitivement modifiés")
    ```

    ```text
    12 pixels définitivement modifiés
    ```

    Ce sont exactement les 12 pixels de fond qui valaient 9 : plafonnés à 9 puis ramenés à 7, ils ne retrouvent pas leur valeur.

## <span style="color:#1565c0">Le seuillage</span>

Le **seuillage** ramène l'image à deux valeurs seulement : noir ou blanc.

!!! question "À toi de jouer C.4 ⭐⭐"
    Écris `seuillage(img, seuil)` : tout pixel supérieur ou égal au seuil devient 9, les autres deviennent 0.

??? success "Corrigé"
    ```python
    def seuillage(img, seuil):
        resultat = []
        for ligne in img:
            nouvelle = []
            for pixel in ligne:
                if pixel >= seuil:
                    nouvelle.append(9)
                else:
                    nouvelle.append(0)
            resultat.append(nouvelle)
        return resultat


    afficher(seuillage(image, 5))
    ```

    ```text
    @@@@        @@@@
    @@  @@@@@@@@  @@
      @@  @@@@  @@
      @@@@@@@@@@@@
      @@@@@@@@@@@@
      @@        @@
    @@  @@@@@@@@  @@
    @@@@        @@@@
    ```

    !!! example "Fais varier le seuil"
        Essaie avec 3, puis avec 8. À partir de quelle valeur le visage devient-il illisible ?

    !!! tip "À quoi ça sert vraiment"
        Le seuillage est la première étape de presque tout traitement automatique d'image : lecture d'un code-barres, reconnaissance de caractères, détection de contours.

        Réduire à deux valeurs supprime énormément d'information — mais ce qui reste est beaucoup plus **facile à analyser** par un programme. C'est un compromis délibéré.

## <span style="color:#1565c0">Le miroir</span>

Jusqu'ici, on a changé les **valeurs** des pixels. Cette fois, on change leur **position**.

!!! question "À toi de jouer C.5 ⭐⭐⭐"
    Écris `miroir(img)` qui retourne l'image horizontalement.

??? success "Corrigé"
    ```python
    def miroir(img):
        resultat = []
        for ligne in img:
            nouvelle = []
            for i in range(len(ligne) - 1, -1, -1):
                nouvelle.append(ligne[i])
            resultat.append(nouvelle)
        return resultat
    ```

    Le `range(len(ligne) - 1, -1, -1)` parcourt les indices **à l'envers** : du dernier jusqu'à 0.

    !!! tip "Beaucoup plus court"
        Le slicing de M0 fait la même chose en une ligne :

        ```python
        def miroir(img):
            resultat = []
            for ligne in img:
                resultat.append(ligne[::-1])
            return resultat
        ```

    !!! note "Sur notre image, rien ne change"
        Le visage est **symétrique** : le miroir donne exactement la même image. Teste-le sur une image asymétrique pour t'en convaincre — par exemple en modifiant un seul œil.

!!! question "À toi de jouer C.6 ⭐⭐⭐ — Le miroir vertical"
    Écris `retourner(img)` qui inverse l'ordre des **lignes**. Sur notre visage, quel effet ?

??? success "Corrigé"
    ```python
    def retourner(img):
        return img[::-1]
    ```

    La bouche passe en haut, les yeux en bas. **Le visage devient méconnaissable** alors qu'aucun pixel n'a changé de valeur — seul leur ordre a changé.

    !!! quote "Ce que ça montre"
        L'information d'une image n'est pas seulement dans les valeurs : elle est aussi dans leur **disposition**. C'est ce qui rend le traitement d'image plus difficile que le traitement d'une liste de nombres.

## <span style="color:#1565c0">L'histogramme</span>

L'**histogramme** d'une image compte combien de pixels ont chaque valeur.

!!! question "À toi de jouer C.7 ⭐⭐"
    Écris `histogramme(img)` qui affiche, pour chaque niveau de 0 à 9, le nombre de pixels concernés — sous forme de barres, comme au module *Les données*.

??? success "Corrigé"
    ```python
    def histogramme(img):
        effectifs = []
        for i in range(10):
            effectifs.append(0)

        for ligne in img:
            for pixel in ligne:
                effectifs[pixel] = effectifs[pixel] + 1

        for i in range(10):
            print(i, ":", "#" * effectifs[i], effectifs[i])
    ```

    ```text
    0 : ###### 6
    1 :  0
    2 : #################### 20
    3 :  0
    4 :  0
    5 :  0
    6 :  0
    7 : ########################## 26
    8 :  0
    9 : ############ 12
    ```

    !!! success "Ce que l'histogramme raconte"
        Quatre valeurs seulement sont utilisées : 0, 2, 7 et 9. Les niveaux intermédiaires sont vides.

        C'est la signature d'une image **dessinée**, pas photographiée. Une vraie photo présente une répartition étalée sur presque toutes les valeurs.

        Un histogramme permet donc de dire quelque chose sur l'**origine** d'une image sans même la regarder.

    !!! tip "Le lien avec le module précédent"
        C'est exactement l'histogramme du bloc C de *Les données* — même fonction, appliquée cette fois à des pixels. Ce qui change n'est pas l'outil, mais ce qu'on regarde.

## <span style="color:#1565c0">Détecter une retouche</span>

!!! example "Activité 1 — L'image trafiquée"
    Quelqu'un a modifié notre image : il a effacé la bouche.

    ```python
    # on fabrique la version retouchée
    retouchee = []
    for ligne in image:
        copie = []
        for pixel in ligne:
            copie.append(pixel)
        retouchee.append(copie)

    for x in range(2, 6):
        retouchee[5][x] = 7

    afficher(retouchee)
    ```

    Écris `differences(a, b)` qui renvoie la liste des pixels modifiés, avec leur position et leurs deux valeurs.

??? success "Corrigé"
    ```python
    def differences(a, b):
        resultat = []
        for y in range(len(a)):
            for x in range(len(a[0])):
                if a[y][x] != b[y][x]:
                    resultat.append([x, y, a[y][x], b[y][x]])
        return resultat


    ecarts = differences(image, retouchee)
    print(len(ecarts), "pixels modifiés")
    for e in ecarts:
        print("  position", e[0], e[1], ":", e[2], "->", e[3])
    ```

    ```text
    4 pixels modifiés
      position 2 5 : 0 -> 7
      position 3 5 : 0 -> 7
      position 4 5 : 0 -> 7
      position 5 5 : 0 -> 7
    ```

    !!! warning "Ce que cette activité prouve — et ce qu'elle ne prouve pas"
        Comparer deux images révèle immédiatement la retouche… **à condition de posséder l'original**.

        Dans la vraie vie, on ne l'a jamais. C'est tout le problème : détecter une modification sans référence est infiniment plus difficile.

        On cherche alors des indices indirects : incohérences d'éclairage, ruptures dans l'histogramme, traces de compression différentes selon les zones, métadonnées mentionnant un logiciel de retouche.

    !!! quote "Vers le bloc D"
        Tu viens de modifier une image en changeant quatre nombres. Une IA générative fait la même chose — changer des nombres — mais sur douze millions de pixels, et en produisant un résultat **cohérent**.

        C'est l'objet de la dernière séance.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc C"
    - Transformer une image, c'est **calculer sur des nombres** : tous les filtres suivent le même patron à deux boucles.
    - Certaines transformations sont **réversibles** (négatif, miroir), d'autres **détruisent de l'information** (éclaircir, seuillage).
    - Changer la **position** des pixels change l'image autant que changer leurs valeurs.
    - L'**histogramme** renseigne sur l'origine d'une image sans la regarder.
    - Détecter une retouche est facile **avec** l'original, très difficile sans.
