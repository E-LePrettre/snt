---
author: Elisabeth Le Prettre (LePrettre)
title: 02c Visualiser et interpréter
---

# Bloc C — Visualiser et interpréter

!!! abstract "Au programme"
    Construire un histogramme · répartir en classes · moyenne et médiane · reconnaître un graphique trompeur

!!! info "Séance 4"
    Un graphique n'est pas une image neutre : c'est une **construction**. Ce bloc apprend à en faire, et surtout à s'en méfier.

## <span style="color:#1565c0">Pourquoi visualiser ?</span>

Au bloc B, on a calculé que le temps d'écran moyen de la classe est de **178,5 minutes**. Ce nombre unique ne dit rien de la diversité des situations : elles vont de 60 à 300 minutes.

!!! quote "Le rôle d'un graphique"
    Un tableau donne les valeurs. Un graphique donne la **forme** : est-ce que tout le monde se ressemble, ou y a-t-il deux groupes ? Y a-t-il un cas isolé ?

    Une moyenne résume. Un graphique montre ce que la moyenne a effacé.

## <span style="color:#1565c0">Un histogramme sans rien installer</span>

On peut dessiner un graphique avec des caractères — et ça réinvestit directement la répétition de chaînes vue en M0.

!!! example "Activité 1 — La barre"
    ```python
    print("#" * 6)
    print("#" * 3)
    ```

    Une barre, c'est un caractère répété autant de fois que la valeur l'exige.

!!! question "À toi de jouer C.1 ⭐⭐"
    Écris une fonction `histogramme(etiquettes, valeurs, unite)` qui affiche une barre par valeur. `unite` indique combien vaut un caractère.

??? success "Corrigé"
    ```python
    def histogramme(etiquettes, valeurs, unite):
        for i in range(len(valeurs)):
            barre = "#" * (valeurs[i] // unite)
            print(etiquettes[i], ":", barre, valeurs[i])
    ```

    ```python
    histogramme(prenoms, ecran, 30)
    ```

    ```text
    Camille : ###### 180
    Lou : ######## 240
    Mohamed : ### 90
    Sarah : #### 120
    Tom : ########## 300
    Ines : ##### 150
    Noah : ####### 210
    Lea : ######### 270
    Gabriel : ## 60
    Jade : ##### 165
    ```

    Le `//` (division entière, vue en M0) donne le nombre de caractères : un `#` pour 30 minutes.

    !!! tip "Le choix de l'unité est déjà une décision"
        Avec `unite = 30`, Gabriel a 2 barres et Tom en a 10 : l'écart saute aux yeux. Avec `unite = 120`, Gabriel en aurait 0 et Tom 2 : l'écart paraîtrait dérisoire.

        **Les mêmes données, deux impressions opposées.** On n'a pourtant menti sur rien.

## <span style="color:#1565c0">Le graphique trompeur</span>

!!! example "Activité 2 — L'axe tronqué"
    Voici une variante. Au lieu de partir de zéro, on part de la plus petite valeur observée.

    ```python
    def minimum(liste):
        record = liste[0]
        for valeur in liste:
            if valeur < record:
                record = valeur
        return record


    mini = minimum(ecran)
    ecarts = []
    for valeur in ecran:
        ecarts.append(valeur - mini)

    histogramme(prenoms, ecarts, 30)
    ```

    Compare avec l'affichage précédent. Que constates-tu ?

??? success "Corrigé"
    ```text
    Camille : #### 120
    Lou : ###### 180
    Mohamed : # 30
    Sarah : ## 60
    Tom : ######## 240
    Ines : ### 90
    Noah : ##### 150
    Lea : ####### 210
    Gabriel :  0
    Jade : ### 105
    ```

    **Gabriel a disparu.** Sa barre est vide, comme s'il ne passait aucun temps devant un écran — alors qu'il en passe une heure par jour.

    Et les écarts entre élèves paraissent bien plus violents : Mohamed avec 90 minutes semble maintenant quatre fois moins concerné que Camille, alors qu'en réalité le rapport est de 1 à 2.

    !!! danger "C'est une technique de manipulation courante"
        Un axe vertical qui ne part pas de zéro **exagère les différences**. On la retrouve constamment dans la presse, la publicité et les communications politiques.

        Aucune donnée n'a été falsifiée. Seule la **construction du graphique** a changé.

!!! success "Le réflexe à acquérir"
    Devant tout graphique, trois questions :

    1. **L'axe part-il de zéro ?** Sinon, les écarts sont amplifiés.
    2. **Quelle est l'échelle ?** Une unité mal choisie écrase ou exagère.
    3. **D'où viennent les données, et qui a fait le graphique ?**

## <span style="color:#1565c0">Regrouper en classes</span>

Avec dix élèves, une barre par individu passe. Avec mille, c'est illisible. On regroupe alors les valeurs en **classes**.

!!! question "À toi de jouer C.2 ⭐⭐⭐"
    Écris `repartition(valeurs, largeur, debut, fin)` qui compte combien de valeurs tombent dans chaque tranche, et affiche le résultat.

??? success "Corrigé"
    ```python
    def repartition(valeurs, largeur, debut, fin):
        borne = debut
        while borne < fin:
            effectif = 0
            for valeur in valeurs:
                if valeur >= borne and valeur < borne + largeur:
                    effectif = effectif + 1
            print(borne, "-", borne + largeur - 1, ":", "#" * effectif, effectif)
            borne = borne + largeur


    repartition(ecran, 60, 60, 360)
    ```

    ```text
    60 - 119 : ## 2
    120 - 179 : ### 3
    180 - 239 : ## 2
    240 - 299 : ## 2
    300 - 359 : # 1
    ```

    !!! warning "Le cas frontière, encore"
        `valeur >= borne and valeur < borne + largeur` : la borne basse est **incluse**, la haute **exclue**. Sans cette précaution, une valeur exactement égale à 120 serait comptée deux fois.

        C'est le même raisonnement que dans le bloc D de M0, avec le code où `>` remplaçait `>=`.

## <span style="color:#1565c0">Moyenne ou médiane ?</span>

La **médiane** est la valeur qui coupe la population en deux : autant au-dessus qu'en dessous.

!!! example "Activité 3 — Quand la moyenne ment"
    ```python
    def trier(liste):
        reste = []
        for v in liste:
            reste.append(v)
        resultat = []
        while len(reste) > 0:
            i_min = 0
            for i in range(len(reste)):
                if reste[i] < reste[i_min]:
                    i_min = i
            resultat.append(reste[i_min])
            reste.pop(i_min)
        return resultat


    def mediane(liste):
        t = trier(liste)
        n = len(t)
        if n % 2 == 1:
            return t[n // 2]
        else:
            return (t[n // 2 - 1] + t[n // 2]) / 2


    print("Moyenne :", round(moyenne(ecran), 1))
    print("Médiane :", mediane(ecran))
    ```

    Puis remplace la dernière valeur par 900 (un élève qui déclare 15 h d'écran) et recommence.

??? success "Corrigé"
    Sur les données d'origine :

    ```text
    Moyenne : 178.5
    Médiane : 172.5
    ```

    Les deux sont proches : la population est assez homogène.

    Avec la valeur extrême de 900 :

    ```text
    Moyenne : 252.0
    Médiane : 195.0
    ```

    La moyenne bondit de **74 minutes** à cause d'un seul individu. La médiane ne bouge que de 22.

    !!! tip "Ce qu'il faut en conclure"
        La **moyenne** est sensible aux valeurs extrêmes. La **médiane** y résiste.

        C'est pourquoi on parle de *salaire médian* plutôt que de salaire moyen : quelques très hautes rémunérations suffiraient à donner une image fausse de la situation courante.

        Choisir l'un ou l'autre n'est jamais neutre — c'est déjà une façon de raconter les données.

## <span style="color:#1565c0">Corrélation n'est pas causalité</span>

Au bloc B, on avait trouvé : les élèves en difficulté en maths passent **270 minutes** par jour devant un écran, contre **139** pour les autres.

!!! example "Activité 4 — Trois explications"
    L'écart est réel. Mais il autorise au moins trois lectures différentes. Lesquelles ?

??? success "Corrigé"
    1. **Les écrans font baisser les notes.** Le temps passé devant un écran est du temps qui n'est pas passé à travailler.
    2. **Les difficultés poussent vers les écrans.** Un élève qui décroche cherche ailleurs une activité gratifiante. La cause et l'effet sont inversés.
    3. **Une troisième cause explique les deux.** Un cadre familial peu structuré, des difficultés de sommeil, une situation personnelle difficile peuvent produire simultanément les mauvaises notes et le temps d'écran.

    Les données **ne permettent pas de trancher**. Elles montrent que les deux phénomènes vont ensemble — une **corrélation** — et rien de plus.

    !!! danger "L'erreur de raisonnement la plus répandue"
        Passer de « ces deux choses varient ensemble » à « l'une cause l'autre » est un saut logique, pas une déduction.

        On le rencontre partout : dans la presse, la publicité, les débats publics. Savoir le repérer est une compétence citoyenne autant que scientifique.

    !!! note "Et l'échantillon ?"
        Ici, on tire cette conclusion à partir de **dix élèves**, dont trois dans le premier groupe. C'est beaucoup trop peu pour conclure quoi que ce soit. La taille de l'échantillon est le sujet du bloc D.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc C"
    - Une moyenne **résume** ; un graphique montre ce qu'elle a **effacé**.
    - Le choix de l'échelle et le point de départ de l'axe changent l'impression sans changer les données.
    - Devant un graphique : l'axe part-il de zéro ? quelle échelle ? quelle source ?
    - La **moyenne** est sensible aux valeurs extrêmes, la **médiane** y résiste.
    - **Corrélation n'est pas causalité** : deux phénomènes liés ne prouvent aucun sens de cause.

