---
author: Elisabeth Le Prettre (LePrettre)
title: 01b Les conditions et les boucles
---

# Bloc B — Écrire un algorithme

!!! abstract "Au programme"
    Instructions conditionnelles (`if`, `elif`, `else`) · boucle `for` · boucle `while`

!!! info "Séance 4 — Les conditions"
    `if / elif / else`, indentation, opérateurs logiques.

## <span style="color:#1565c0">Les instructions conditionnelles</span>

!!! info "Algorithme ou programme ?"
    Un **algorithme** est une méthode : la suite d'étapes à suivre pour résoudre un problème. On peut l'écrire en français, sur une feuille.

    Un **programme** est la traduction de cet algorithme dans un langage qu'une machine comprend.

    Ce bloc porte sur les deux structures qui permettent d'exprimer n'importe quel algorithme : **choisir** (conditions) et **répéter** (boucles).

Jusqu'ici, nos programmes exécutaient toutes les lignes, dans l'ordre. Une **instruction conditionnelle** permet de n'exécuter certaines instructions **que si** une condition est vraie.

```python
if condition:
    # bloc exécuté si la condition est vraie (True)
```

!!! warning "L'indentation fait le programme"
    En Python, c'est le **décalage vers la droite** (l'*indentation*, 4 espaces) qui délimite le bloc. Toutes les instructions d'un même bloc ont le même décalage.

    Contrairement à d'autres langages, ce n'est pas une question de style : **une mauvaise indentation change le sens du programme**, ou provoque une erreur.

### <span style="color:#2e7d32">`if` … `else`</span>

```python
if condition:
    # bloc exécuté si la condition est vraie
else:
    # bloc exécuté sinon
```

Le bloc `else` est facultatif.

!!! example "Activité 1 — Positif ou négatif"
    Teste ce code avec les valeurs `8`, `-6` puis `0` :

    ```python
    a = int(input("Entre un nombre entier : "))
    if a >= 0:
        print("Nombre positif ou nul :", a)
    else:
        print("Nombre négatif :", a)
    ```

    **Question bonus :** que se passe-t-il si tu saisis le mot `positif` ?

??? success "Réponse"
    Avec `8` et `0` : premier message. Avec `-6` : second message.

    Avec le mot `positif`, le programme **plante** avant même le test :

    ```text
    ValueError: invalid literal for int() with base 10: 'positif'
    ```

    `int()` ne peut pas convertir ce texte en nombre. C'est un rappel utile : **un programme doit anticiper les saisies invalides**.

### <span style="color:#2e7d32">Les opérateurs de comparaison</span>

| Opérateur | Signification |
| --- | --- |
| `==` | est égal à |
| `!=` | est différent de |
| `<` `>` | strictement inférieur / supérieur |
| `<=` `>=` | inférieur / supérieur ou égal |

!!! danger "`=` ou `==` ?"
    - `a = 2` **range** la valeur 2 dans `a` (affectation).
    - `a == 2` **teste** si `a` vaut 2 et renvoie `True` ou `False`.

    Écrire `if a = 2:` provoque une erreur de syntaxe. C'est l'erreur la plus fréquente en début d'apprentissage.

### <span style="color:#2e7d32">`elif` : tester plusieurs cas</span>

```python
if condition1:
    # si condition1 est vraie
elif condition2:
    # sinon, si condition2 est vraie
elif condition3:
    # sinon, si condition3 est vraie
else:
    # si aucune des précédentes n'est vraie
```

!!! tip "L'ordre des tests compte énormément"
    Python teste les conditions **dans l'ordre** et s'arrête **à la première qui est vraie**. Les suivantes ne sont même pas évaluées.

    Conséquence : une condition placée trop tard peut devenir **inatteignable**. C'est l'objet de l'activité suivante.

!!! example "Activité 2 — Le cas inatteignable"
    Voici un programme censé commenter une note :

    ```python
    note = int(input("Ta note en informatique : "))
    if note >= 16:
        print("Excellent !")
    elif note >= 12:
        print("C'est bien")
    elif note < 12:
        print("Il faut travailler")
    elif note == 0:
        print("Oh là là...")
    ```

    Teste avec `17`, `14`, `7` puis **`0`**.

    **Question :** le message « Oh là là… » s'affiche-t-il jamais ? Pourquoi ?

??? success "Corrigé — un vrai bug de logique"
    **Non, jamais.**

    Quand `note` vaut 0, Python teste dans l'ordre :

    1. `0 >= 16` → faux
    2. `0 >= 12` → faux
    3. `0 < 12` → **vrai** → il affiche « Il faut travailler » et **sort de la structure**

    La branche `note == 0` n'est jamais atteinte, car tout nombre égal à 0 est déjà inférieur à 12.

    **Correction :** placer le cas le plus **spécifique en premier**.

    ```python
    note = int(input("Ta note en informatique : "))
    if note == 0:
        print("Oh là là...")
    elif note >= 16:
        print("Excellent !")
    elif note >= 12:
        print("C'est bien")
    else:
        print("Il faut travailler")
    ```

    !!! quote "À retenir"
        Dans une cascade de `elif`, on va **du cas le plus particulier au plus général**.

### <span style="color:#2e7d32">Combiner des conditions : `and`, `or`, `not`</span>

| Opérateur | Vrai quand… | Exemple |
| --- | --- | --- |
| `and` | **les deux** conditions sont vraies | `age >= 12 and age < 18` |
| `or` | **au moins une** est vraie | `couleur == "bleu" or couleur == "rouge"` |
| `not` | la condition est fausse | `not (age >= 18)` |

!!! example "Activité 3 — Le mot de passe couleur"
    Écris un programme qui demande une couleur. Si c'est `bleu`, `rouge` ou `vert`, il affiche « C'est gagné », sinon « C'est perdu ».

    Teste avec `rouge`, `vert`, `noir`.

??? success "Corrigé"
    ```python
    couleur = input("Donne une couleur : ")
    if couleur == "bleu" or couleur == "rouge" or couleur == "vert":
        print("C'est gagné")
    else:
        print("C'est perdu")
    ```

    **Plus élégant**, avec l'opérateur `in` rencontré page précédente :

    ```python
    couleur = input("Donne une couleur : ")
    if couleur in ["bleu", "rouge", "vert"]:
        print("C'est gagné")
    else:
        print("C'est perdu")
    ```

    !!! warning "Piège fréquent"
        `if couleur == "bleu" or "rouge":` **ne fonctionne pas** comme on l'espère. Python comprend « si couleur vaut bleu, **ou bien** si la chaîne "rouge" est non vide » — ce qui est toujours vrai. Il faut répéter la comparaison entière.

### <span style="color:#2e7d32">Fil rouge : attribuer une mention</span>

!!! question "À toi de jouer 2.1 ⭐⭐ — Les mentions"
    Écris un programme qui demande une note sur 20 et affiche la mention correspondante :

    | Note | Mention |
    | --- | --- |
    | 16 et plus | Très bien |
    | de 14 à moins de 16 | Bien |
    | de 12 à moins de 14 | Assez bien |
    | de 10 à moins de 12 | Admis |
    | moins de 10 | Insuffisant |

    Teste avec 18, 15, 13, 10 et 7.

??? success "Corrigé"
    ```python
    note = float(input("Ta note sur 20 : "))

    if note >= 16:
        print("Très bien")
    elif note >= 14:
        print("Bien")
    elif note >= 12:
        print("Assez bien")
    elif note >= 10:
        print("Admis")
    else:
        print("Insuffisant")
    ```

    Remarque l'ordre : on part du **seuil le plus haut** et on descend. Chaque `elif` n'est atteint que si les précédents ont échoué — inutile donc d'écrire `elif note >= 14 and note < 16`.

    !!! note "Ce programme resservira"
        En page 3, on transformera ce code en **fonction** `mention(note)`, réutilisable sur toute une classe.

!!! info "Séance 5 — La boucle `for`"
    `range`, parcours d'une séquence, accumulateur et compteur.

## <span style="color:#1565c0">La boucle `for`</span>

Une boucle `for` répète un bloc d'instructions **un nombre de fois connu à l'avance**.

### <span style="color:#2e7d32">`for` avec `range`</span>

```python
for i in range(n):
    # bloc répété n fois, avec i qui prend les valeurs 0, 1, ..., n-1
```

!!! example "Activité 4 — Compter"
    ```python
    for i in range(11):
        print(i)
    ```

    **Question :** combien de nombres s'affichent ? Quel est le premier ? Le dernier ?

??? success "Réponse"
    **11 nombres** s'affichent : de **0** à **10**.

    `range(11)` produit 11 valeurs, mais elles vont de 0 à 10 — pas jusqu'à 11. C'est le même principe que l'indexation des chaînes : on part de 0.

!!! info "Les trois formes de `range`"
    | Écriture | Valeurs prises par `i` |
    | --- | --- |
    | `range(5)` | 0, 1, 2, 3, 4 |
    | `range(2, 6)` | 2, 3, 4, 5 |
    | `range(2, 10, 2)` | 2, 4, 6, 8 |
    | `range(10, 0, -1)` | 10, 9, 8, …, 1 |

    La borne de fin est **toujours exclue**.

!!! example "Activité 5 — Accumuler"
    ```python
    somme = 0
    for i in range(11):
        somme = somme + i
    print(somme)
    ```

    Vérifie que le résultat correspond bien à 0 + 1 + 2 + … + 10.

??? success "Réponse"
    Le programme affiche **55**.

    Ce schéma est fondamental et reviendra sans cesse :

    1. on **initialise** un accumulateur avant la boucle (`somme = 0`) ;
    2. on le **met à jour** à chaque tour (`somme = somme + i`) ;
    3. on l'**utilise** après la boucle.

    !!! danger "Erreur classique"
        Si `print(somme)` est **indenté** dans la boucle, il s'exécute à chaque tour et affiche 11 lignes. L'indentation décide de ce qui est dans la boucle et de ce qui est après.

### <span style="color:#2e7d32">`for` avec `in` : parcourir directement</span>

```python
for element in sequence:
    # bloc exécuté une fois par élément
```

!!! example "Activité 6 — Parcourir un texte"
    ```python
    phrase = "Bonjour à tous"
    for lettre in phrase:
        print(lettre)
    ```

    Ici, `lettre` prend successivement la valeur de chaque caractère.

!!! example "Activité 7 — Compter des occurrences"
    ```python
    citation = "Je ne cherche pas à connaître les réponses, je cherche à comprendre les questions."
    compteur = 0
    for lettre in citation:
        if lettre == "e":
            compteur = compteur + 1
    print(compteur)
    ```

    **Questions :** que fait ce code ? Modifie-le pour compter les `a`.

??? success "Réponse"
    Il compte le nombre de `e` **minuscules** dans la citation (les `E` majuscules ne sont pas comptés — rappel sur la casse).

    Pour les `a`, il suffit de changer le caractère testé :

    ```python
    if lettre == "a":
    ```

    On reconnaît le même schéma qu'à l'activité 5 : **initialiser un compteur, l'incrémenter dans la boucle, l'afficher après**.

!!! question "À toi de jouer 2.2 ⭐⭐ — Compter les voyelles"
    Écris un programme qui demande une phrase à l'utilisateur et affiche son **nombre de voyelles**.

    **Indice :** l'opérateur `in` permet de tester d'un coup l'appartenance à un ensemble de caractères.

??? success "Corrigé"
    ```python
    phrase = input("Écris une phrase : ")
    compteur = 0

    for lettre in phrase:
        if lettre in "aeiouyAEIOUY":
            compteur = compteur + 1

    print("Nombre de voyelles :", compteur)
    ```

    **Test** avec `Sciences numériques et technologie` : 14 voyelles.

    !!! note "Lien avec le module IA"
        Compter des caractères, des mots, des occurrences : c'est exactement ce que fait un programme qui **prépare des données textuelles** avant de les donner à un modèle d'IA. Le module *Intelligence artificielle* reviendra sur cette étape.

### <span style="color:#2e7d32">Exercices sur `for`</span>

??? question "Exercice 1 ⭐ — Les 100 premiers entiers"
    Écris un script qui affiche les 100 premiers entiers **non nuls** (de 1 à 100).

    ??? success "Corrigé"
        ```python
        for i in range(1, 101):
            print(i)
        ```

        Le piège : `range(100)` afficherait de 0 à 99. Il faut donc `range(1, 101)`.

??? question "Exercice 2 ⭐⭐ — Deux sommes"
    Calcule, avec une boucle `for` :

    a) `1 + 2 + 3 + ... + 100`
    b) `1 + 3 + 5 + ... + 99` (les nombres impairs)

    ??? success "Corrigé"
        ```python
        # a) tous les entiers de 1 à 100
        somme = 0
        for i in range(1, 101):
            somme = somme + i
        print("Somme de 1 à 100 :", somme)
        ```

        ```text
        Somme de 1 à 100 : 5050
        ```

        ```python
        # b) les impairs de 1 à 99 : on avance de 2 en 2
        somme = 0
        for i in range(1, 100, 2):
            somme = somme + i
        print("Somme des impairs :", somme)
        ```

        ```text
        Somme des impairs : 2500
        ```

??? question "Exercice 3 ⭐⭐⭐ — La pyramide de billes"
    Inès construit une pyramide à base carrée : l'étage du sommet compte 1 bille, le suivant 2 × 2 = 4 billes, le suivant 3 × 3 = 9 billes, etc.

    a) Combien de billes faut-il pour une pyramide de **100 étages** ?
    b) Modifie le programme pour que l'utilisateur choisisse le nombre d'étages.

    ??? success "Corrigé"
        ```python
        # a)
        total = 0
        for etage in range(1, 101):
            total = total + etage * etage
        print("Il faut", total, "billes")
        ```

        ```text
        Il faut 338350 billes
        ```

        ```python
        # b)
        n = int(input("Nombre d'étages : "))
        total = 0
        for etage in range(1, n + 1):
            total = total + etage * etage
        print("Il faut", total, "billes")
        ```

        Le point délicat est `range(1, n + 1)` : pour aller **jusqu'à `n` inclus**, il faut écrire `n + 1` comme borne.

!!! info "Séance 6 — La boucle `while`"
    Problèmes de seuil, boucle infinie, choix entre `for` et `while`.

## <span style="color:#1565c0">La boucle `while`</span>

Une boucle `while` répète un bloc **tant qu'une condition reste vraie**. On ne connaît pas à l'avance le nombre de tours.

```python
while condition:
    # bloc répété tant que la condition est vraie
```

!!! danger "La boucle infinie"
    Si la condition ne devient jamais fausse, le programme ne s'arrête plus. Il faut donc **toujours** que quelque chose évolue à l'intérieur de la boucle.

    ```python
    # NE JAMAIS FAIRE : compteur ne change pas
    compteur = 0
    while compteur < 10:
        print("Au secours")
    ```

    Sur Basthon, il faut alors recharger la page.

!!! tip "`for` ou `while` ?"
    - Le nombre de répétitions est **connu** → `for`
    - On répète **jusqu'à ce qu'un seuil soit atteint** → `while`

!!! example "Activité 8 — Le rebond de la balle"
    Une balle part de 2 m et perd 10 % de sa hauteur à chaque rebond. Combien de rebonds pour passer sous 1,5 m ?

    ```python
    hauteur = 2
    rebonds = 0
    seuil = 1.5

    while hauteur > seuil:
        rebonds = rebonds + 1
        hauteur = hauteur * 0.9

    print("Nombre de rebonds :", rebonds)
    print("Hauteur atteinte :", round(hauteur, 3))
    ```

    Modifie ensuite les valeurs pour une balle partant de 3 m et un seuil de 2 m.

??? success "Réponse"
    Avec 2 m et un seuil de 1,5 m : **3 rebonds** (hauteur ≈ 1,458 m).

    Avec 3 m et un seuil de 2 m : **4 rebonds** (hauteur ≈ 1,968 m).

    C'est un **problème de seuil** : on ne peut pas connaître le nombre de tours à l'avance, d'où le `while`.

### <span style="color:#2e7d32">Exercices sur `while`</span>

??? question "Exercice 4 ⭐⭐ — Plier une feuille"
    Une feuille de papier a une épaisseur de 0,1 mm. À chaque pliage, l'épaisseur **double**.

    Combien de pliages faut-il au minimum pour dépasser 400 mm ?

    ??? success "Corrigé"
        ```python
        epaisseur = 0.1
        pliages = 0

        while epaisseur <= 400:
            epaisseur = epaisseur * 2
            pliages = pliages + 1

        print("Nombre de pliages :", pliages)
        print("Épaisseur atteinte :", round(epaisseur, 1), "mm")
        ```

        ```text
        Nombre de pliages : 12
        Épaisseur atteinte : 409.6 mm
        ```

        !!! quote "Croissance exponentielle"
            En 12 pliages seulement, on passe de 0,1 mm à plus de 40 cm. En 42 pliages théoriques, on atteindrait la Lune. Cette croissance très rapide se retrouvera dans le module *Données* (croissance du volume de données produites) et dans le module *IA* (taille des modèles).

??? question "Exercice 5 ⭐⭐⭐ — La consommation d'un data center"
    La consommation électrique d'un centre de données augmente de **8 % par an**.

    En combien d'années cette consommation aura-t-elle **doublé** ? On partira d'une consommation de référence égale à 100.

    ??? success "Corrigé"
        Augmenter de 8 %, c'est multiplier par 1,08.

        ```python
        conso = 100
        annees = 0

        while conso < 200:
            conso = conso * 1.08
            annees = annees + 1

        print("Doublement atteint en", annees, "ans")
        print("Consommation :", round(conso, 1))
        ```

        ```text
        Doublement atteint en 10 ans
        Consommation : 215.9
        ```

        !!! warning "Le point qui fait rater cet exercice"
            Il ne suffit pas de faire tourner la boucle : il faut **compter les tours** avec un compteur incrémenté à l'intérieur (`annees = annees + 1`). Sans lui, le programme calcule bien la consommation finale mais ne répond pas à la question posée.

        !!! note "Lien avec les modules Internet et IA"
            Ce n'est pas un exercice abstrait : la consommation des centres de données, tirée notamment par l'IA, est un enjeu environnemental majeur. On y reviendra dans les modules *Internet et le Web* et *Intelligence artificielle*.

??? question "Exercice 6 ⭐⭐ — Fil rouge : saisir des notes jusqu'à l'arrêt"
    Écris un programme qui demande des notes à l'utilisateur **une par une**, jusqu'à ce qu'il saisisse `-1`. Le programme affiche alors le **nombre de notes** saisies et leur **moyenne**.

    ??? success "Corrigé"
        ```python
        somme = 0
        nombre = 0

        note = float(input("Une note (-1 pour terminer) : "))

        while note != -1:
            somme = somme + note
            nombre = nombre + 1
            note = float(input("Une note (-1 pour terminer) : "))

        if nombre > 0:
            print("Nombre de notes :", nombre)
            print("Moyenne :", round(somme / nombre, 2))
        else:
            print("Aucune note saisie.")
        ```

        Deux points importants :

        - la **première saisie a lieu avant la boucle**, sinon la condition ne peut pas être testée au premier tour ;
        - le test `if nombre > 0` évite une **division par zéro** si l'utilisateur saisit `-1` immédiatement. Anticiper ce cas limite fait partie du métier.

        La valeur `-1`, qui signale la fin sans être une donnée, s'appelle une **valeur sentinelle**.

??? question "Exercice 7 ⭐⭐⭐ — Les deux comètes"
    La comète de Halley passe près du Soleil tous les **76 ans** ; son dernier passage date de **1986**.
    La comète 55P/Tempel-Tuttle passe tous les **33 ans** ; son dernier passage date de **1998**.

    Quelle sera la prochaine année où **les deux** passeront ?

    ??? success "Corrigé"
        L'idée : on avance toujours celle qui est « en retard », jusqu'à ce que les deux années coïncident.

        ```python
        halley = 1986
        tempel = 1998

        while halley != tempel:
            if halley < tempel:
                halley = halley + 76
            else:
                tempel = tempel + 33

        print("Prochaine année commune :", halley)
        ```

        ```text
        Prochaine année commune : 3582
        ```

??? question "Exercice 8 ⭐⭐⭐ — Des petits trous…"
    Écris les scripts qui affichent chacun de ces motifs.

    **Motif A**

    ```text
    o
    oo
    ooo
    oooo
    ooooo
    ```

    **Motif B**

    ```text
    ooooo
    oooo
    ooo
    oo
    o
    ```

    **Motif C**

    ```text
        o
       oo
      ooo
     oooo
    ooooo
    ```

    **Motif D — le sapin**

    ```text
        o
       ooo
      ooooo
     ooooooo
    ooooooooo
    ```

    **Indice :** `"o" * 3` produit `"ooo"`, et `" " * 2` produit deux espaces.

    ??? success "Corrigé"
        **Motif A** — on augmente le nombre de `o` :

        ```python
        for k in range(1, 6):
            print("o" * k)
        ```

        **Motif B** — on diminue :

        ```python
        for k in range(5, 0, -1):
            print("o" * k)
        ```

        **Motif C** — on ajoute des espaces devant, en nombre décroissant :

        ```python
        for k in range(1, 6):
            print(" " * (5 - k) + "o" * k)
        ```

        **Motif D** — les lignes ont 1, 3, 5, 7, 9 caractères : à l'étage `k` (à partir de 0), il y a `2 * k + 1` symboles et `4 - k` espaces :

        ```python
        for k in range(5):
            print(" " * (4 - k) + "o" * (2 * k + 1))
        ```

        !!! tip "Méthode"
            Pour ce type d'exercice, écris d'abord **le tableau** : numéro de ligne, nombre d'espaces, nombre de `o`. La formule apparaît alors d'elle-même.

            | Ligne `k` | Espaces | Symboles |
            | --- | --- | --- |
            | 0 | 4 | 1 |
            | 1 | 3 | 3 |
            | 2 | 2 | 5 |
            | 3 | 1 | 7 |
            | 4 | 0 | 9 |

## <span style="color:#1565c0">Exercices corrigés — récapitulatif</span>

??? question "Exercice 9 ⭐ — Majeur ou mineur"
    Demande l'âge d'une personne et affiche si elle est majeure ou mineure.

    ??? success "Corrigé"
        ```python
        age = int(input("Quel est votre âge ? "))
        if age < 18:
            print("Vous êtes mineur·e")
        else:
            print("Vous êtes majeur·e")
        ```

??? question "Exercice 10 ⭐⭐ — Tarifs de cinéma"
    Un cinéma applique trois tarifs **pour deux personnes** :

    - les deux mineures : 7 € chacune ;
    - une seule mineure : tarif groupe de 15 € ;
    - les deux majeures : 18 € au total.

    Demande l'âge de chacune et affiche le prix à payer.

    ??? success "Corrigé"
        ```python
        age1 = int(input("Âge de la première personne : "))
        age2 = int(input("Âge de la deuxième personne : "))

        if age1 < 18 and age2 < 18:
            print("Vous payez 7 € chacun, soit 14 €")
        elif age1 >= 18 and age2 >= 18:
            print("Vous payez 18 € en tout")
        else:
            print("Vous payez le tarif groupe de 15 €")
        ```

        Le `else` final couvre exactement le cas « une seule mineure » : inutile de l'écrire explicitement, puisque les deux autres cas ont été éliminés.

??? question "Exercice 11 ⭐⭐ — Catégories de rugby"
    Une école de rugby répartit les joueurs en quatre groupes :

    | Groupe | Âge |
    | --- | --- |
    | U8 | de 8 à moins de 10 ans |
    | U10 | de 10 à moins de 12 ans |
    | U12 | de 12 à moins de 14 ans |
    | U14 | de 14 à moins de 16 ans |

    Écris un programme qui demande l'âge et renvoie la catégorie.

    ??? success "Corrigé"
        ```python
        age = int(input("Âge du joueur : "))

        if 8 <= age < 10:
            print("Catégorie U8")
        elif 10 <= age < 12:
            print("Catégorie U10")
        elif 12 <= age < 14:
            print("Catégorie U12")
        elif 14 <= age < 16:
            print("Catégorie U14")
        else:
            print("Aucune catégorie ne correspond à cet âge")
        ```

        !!! warning "Ne jamais oublier le `else` final"
            Sans lui, un âge de 6 ou 20 ans ne déclenche **aucun affichage** : l'utilisateur croit à un plantage. Un programme doit toujours répondre quelque chose.

        Noter au passage l'écriture `8 <= age < 10`, plus lisible que `age >= 8 and age < 10`.

??? question "Exercice 12 ⭐⭐ — Abonnement de théâtre"
    Un théâtre applique un tarif dégressif :

    - jusqu'à 2 pièces : 15 € la séance ;
    - de 3 à 5 pièces : 12 € la séance ;
    - à partir de 6 pièces : 10 € la séance.

    Demande le nombre de pièces et affiche le **prix total** de la saison.

    ??? success "Corrigé"
        ```python
        nombre = int(input("Combien de pièces voulez-vous voir ? "))

        if nombre <= 2:
            tarif = 15
        elif nombre <= 5:
            tarif = 12
        else:
            tarif = 10

        total = nombre * tarif
        print("Tarif :", tarif, "€ la séance")
        print("Total pour la saison :", total, "€")
        ```

        Astuce de structure : plutôt que d'écrire un `print` dans chaque branche, on **stocke le tarif** dans une variable et on n'écrit le calcul qu'une seule fois. Le programme est plus court et plus facile à modifier.

??? question "Exercice 13 ⭐⭐ — Table de multiplication"
    Affiche tous les produits de deux entiers compris entre 0 et 10.

    ??? success "Corrigé"
        Il faut une boucle **dans** une boucle (on parle de boucles *imbriquées*) :

        ```python
        for i in range(11):
            for j in range(11):
                print(i, "x", j, "=", i * j)
        ```

        La boucle intérieure effectue ses 11 tours complets **pour chaque** valeur de `i` : au total 11 × 11 = 121 lignes.

        Pour un affichage plus lisible, une ligne par table :

        ```python
        for i in range(11):
            print("--- Table de", i, "---")
            for j in range(11):
                print(i, "x", j, "=", i * j)
        ```

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. Quelle est la différence entre `=` et `==` ?
    2. Dans une cascade de `elif`, dans quel ordre placer les conditions ?
    3. Quelles valeurs prend `i` dans `for i in range(3, 8)` ?
    4. Quand préférer `while` à `for` ?
    5. Qu'est-ce qu'une boucle infinie, et comment l'éviter ?
    6. Que produit `print(" " * 3 + "o" * 2)` ?

??? success "Réponses"
    1. `=` **affecte** une valeur à une variable ; `==` **teste** une égalité et renvoie `True` ou `False`.
    2. Du cas **le plus spécifique** au cas **le plus général** — sinon certaines branches deviennent inatteignables.
    3. 3, 4, 5, 6, 7 (la borne 8 est exclue).
    4. Quand le nombre de répétitions n'est **pas connu à l'avance** : on répète jusqu'à ce qu'un seuil soit atteint.
    5. Une boucle dont la condition ne devient jamais fausse. On l'évite en s'assurant qu'une variable de la condition **évolue** à chaque tour.
    6. Trois espaces suivis de `oo`, soit `   oo`.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel de la page"
    - L'**indentation** délimite les blocs : elle fait partie du code, pas de la mise en forme.
    - Dans une cascade `if / elif / else`, l'**ordre** des conditions est décisif.
    - `for` : nombre de tours **connu**. `while` : on répète **jusqu'à un seuil**.
    - Schéma universel : **initialiser** un compteur ou un accumulateur → le **mettre à jour** dans la boucle → l'**utiliser** après.
    - Toujours prévoir le **cas limite** (aucune donnée, saisie invalide, division par zéro).



