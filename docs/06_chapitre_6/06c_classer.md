---
author: Elisabeth Le Prettre (LePrettre)
title: 06b Classer
---

# Bloc B — Classer

!!! abstract "Au programme"
    Le plus proche voisin · écrire un classifieur · frontière de décision · données d'entraînement et de test · le surapprentissage

!!! info "Séances 2 et 3"
    Séance 2 : écrire un classifieur qui apprend d'exemples. Séance 3 : mesurer s'il a vraiment appris.

## <span style="color:#1565c0">L'idée du plus proche voisin</span>

Comment classer une nouvelle pomme ou orange sans écrire de règle ? L'idée la plus simple qui soit :

!!! quote "Le principe"
    Pour deviner l'étiquette d'un nouveau fruit, on cherche, parmi les exemples connus, **celui qui lui ressemble le plus** — et on lui donne la même étiquette.

    « Se ressembler », ici, veut dire : avoir des mesures proches.

C'est l'algorithme du **plus proche voisin**. Il n'y a rien de plus dans beaucoup de systèmes réels — juste en plus grand.

## <span style="color:#1565c0">Mesurer une ressemblance</span>

Nos fruits ont deux mesures : masse et rugosité. Chaque fruit est donc un **point**. Deux fruits se ressemblent si leurs points sont proches.

La distance entre deux points se calcule comme à l'école — le théorème de Pythagore, croisé en M0 :

!!! example "Activité 1 — La distance"
    ```python
    def distance(a, b):
        return ((a[0] - b[0]) ** 2 + (a[1] - b[1]) ** 2) ** 0.5


    orange = [150, 7]
    pomme = [130, 2]
    inconnu = [145, 6]

    print("distance à l'orange :", round(distance(inconnu, orange), 1))
    print("distance à la pomme :", round(distance(inconnu, pomme), 1))
    ```

??? success "Résultat"
    ```text
    distance à l'orange : 5.1
    distance à la pomme : 15.5
    ```

    L'inconnu est **trois fois plus proche** de l'orange. On parierait donc : orange.

    !!! tip "Le `** 0.5`"
        Élever à la puissance 0,5, c'est prendre la racine carrée. On retrouve le calcul de Pythagore vu en M0 — appliqué ici non pas à une figure, mais à une **ressemblance**.

## <span style="color:#1565c0">Écrire le classifieur</span>

!!! question "À toi de jouer B.1 ⭐⭐⭐"
    Écris `classer(point, exemples)` qui renvoie l'étiquette de l'exemple **le plus proche** du point.

    **Indice :** c'est le schéma du **minimum** de M0, mais on garde l'exemple qui réalise le minimum, pas seulement la distance.

??? success "Corrigé"
    ```python
    exemples = [
     [150, 7, "orange"], [170, 8, "orange"], [140, 6, "orange"], [160, 9, "orange"],
     [130, 2, "pomme"],  [145, 3, "pomme"],  [120, 1, "pomme"],  [155, 2, "pomme"]]


    def classer(point, exemples):
        meilleur = exemples[0]
        d_min = distance(point, meilleur)
        for exemple in exemples:
            d = distance(point, exemple)
            if d < d_min:
                d_min = d
                meilleur = exemple
        return meilleur[2]
    ```

    ```text
    >>> classer([135, 2], exemples)
    'pomme'
    >>> classer([165, 8], exemples)
    'orange'
    >>> classer([148, 5], exemples)
    'orange'
    ```

    !!! success "Tu viens d'écrire une IA"
        Ce programme **apprend d'exemples** : change les exemples, et il classe différemment, sans qu'une seule ligne de code soit modifiée.

        C'est la différence du bloc A, rendue concrète : la connaissance n'est pas dans le code, elle est dans les **données**.

    !!! note "Le lien avec M0"
        Compare avec la fonction `maximum` de M0 : on parcourt, on garde le meilleur candidat, on le renvoie. C'est **exactement** le même schéma. Un classifieur, c'est une recherche de minimum.

## <span style="color:#1565c0">Voir ce que le modèle a appris</span>

On peut visualiser la décision du classifieur sur **tout** l'espace : pour chaque combinaison de masse et de rugosité, quelle étiquette donne-t-il ?

!!! example "Activité 2 — La frontière de décision"
    ```python
    def frontiere(exemples):
        for rugosite in range(10, -1, -1):
            ligne = ""
            for masse in range(115, 176, 5):
                if classer([masse, rugosite], exemples) == "orange":
                    ligne = ligne + "O"
                else:
                    ligne = ligne + "."
            print(str(rugosite).rjust(2), ligne)


    frontiere(exemples)
    ```

??? success "Résultat"
    ```text
    10 ....OOOOOOOOO
     9 ....OOOOOOOOO
     8 ....OO.OOOOOO
     7 ....OO.OOOOOO
     6 ....OO.O.OOOO
     5 ....OO.O.OOOO
     4 ....OO.O.OOOO
     3 .....O.O..OOO
     2 .....O.O..OOO
     1 .....O....OOO
     0 ..........OOO
    ```

    Les `O` sont les zones classées « orange », les `.` les zones « pomme ». On **voit** la frontière que le modèle a construite — sans qu'on l'ait dessinée.

    !!! warning "Regarde les irrégularités"
        La frontière n'est pas une ligne nette. Il y a des `O` isolés au milieu des `.`, des découpes bizarres.

        Ce sont les endroits où un exemple particulier « attire » son voisinage. Le modèle n'a pas dégagé une loi générale : il a **mémorisé des cas**, et la frontière porte la trace de chaque exemple.

        Cette observation prépare directement la notion de surapprentissage.

## <span style="color:#1565c0">Entraîner et tester</span>

!!! info "Séance 3"

Voici la question qui distingue une démarche sérieuse d'une illusion : **comment sait-on que le modèle a vraiment appris ?**

!!! danger "La faute méthodologique à ne jamais commettre"
    On ne teste **jamais** un modèle sur les exemples qui ont servi à l'entraîner.

    Pourquoi ? Parce que le plus proche voisin d'un exemple d'entraînement, c'est **lui-même** (distance nulle). Testé sur ses propres données, ce classifieur a toujours 100 % de réussite — et cela ne prouve **rien**.

    C'est comme réviser un contrôle avec le corrigé sous les yeux : réussir ne dit rien de ce qu'on a compris.

!!! info "La règle"
    On sépare les exemples en deux groupes :

    - les **données d'entraînement** : le modèle les connaît, il apprend dessus ;
    - les **données de test** : le modèle ne les a **jamais vues**, on mesure sa réussite dessus.

    Seule la réussite sur les données de test compte.

!!! question "À toi de jouer B.2 ⭐⭐"
    Écris `evaluer(entrainement, test)` qui renvoie le nombre de bonnes réponses sur les données de test.

??? success "Corrigé"
    ```python
    def evaluer(entrainement, test):
        bons = 0
        for point in test:
            prediction = classer(point, entrainement)
            if prediction == point[2]:
                bons = bons + 1
        return bons, len(test)


    entrainement = exemples[:6]
    test = [[140, 6, "orange"], [125, 2, "pomme"]]

    print(evaluer(entrainement, test))
    ```

    ```text
    (2, 2)
    ```

    Deux bonnes réponses sur deux : le modèle **généralise** — il classe correctement des fruits qu'il n'avait jamais vus.

    !!! tip "Le vocabulaire officiel"
        - **Entraîner** (ou *apprendre*) : construire le modèle à partir des données d'entraînement.
        - **Tester** (ou *évaluer*) : mesurer sa réussite sur des données réservées.
        - **Généraliser** : bien fonctionner sur des données nouvelles. C'est le seul but qui compte.

## <span style="color:#1565c0">Le surapprentissage</span>

!!! example "Activité 3 — Le piège"
    Un élève propose : « Pour être sûr d'avoir un bon modèle, mettons **tous** les exemples dans l'entraînement. Plus il en voit, mieux c'est. »

    Où est le problème ?

??? success "Corrigé"
    Il ne reste alors **aucune donnée de test**. On ne peut plus mesurer si le modèle généralise — on est revenu à réviser avec le corrigé.

    Le problème plus profond s'appelle le **surapprentissage** (*overfitting*) : un modèle qui colle trop exactement à ses exemples d'entraînement.

    Repense à la frontière de décision, avec ses `O` isolés. Un modèle qui mémorise chaque cas particulier **reproduit parfaitement l'entraînement** mais se trompe sur les données nouvelles, parce qu'il a appris les détails — y compris les accidents — au lieu de la tendance.

    !!! quote "L'analogie qui marche"
        Un élève qui **apprend par cœur** les corrigés des exercices du manuel aura 20/20 sur ces exercices précis, et échouera au contrôle sur des exercices légèrement différents.

        Un élève qui **comprend la méthode** réussira les deux.

        Un bon modèle est comme le second : il a dégagé la règle, pas mémorisé les cas. Et la seule façon de faire la différence, c'est de tester sur des données **nouvelles**.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc B"
    - Le **plus proche voisin** classe un point comme l'exemple connu qui lui ressemble le plus.
    - Un classifieur est une **recherche de minimum** — le même schéma que `maximum` en M0.
    - La connaissance est dans les **données**, pas dans le code : changer les exemples change les décisions.
    - On **entraîne** sur un groupe de données, on **teste** sur un autre, jamais vu. Seul le test compte.
    - Un modèle qui colle trop à ses exemples fait du **surapprentissage** : il mémorise au lieu de généraliser.

