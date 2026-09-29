---
author: Elisabeth Le Prettre (LePrettre)
title: 01a Les bases
---

# Bloc A — Représenter une donnée

!!! abstract "Au programme"
    Variables et affectation · calculs · affichage · dialogue avec l'utilisateur · chaînes de caractères

!!! info "Séance 1 — Prise en main, variables et calculs"
    Basthon et Capytale, premier programme, variable et affectation, opérateurs arithmétiques.

## <span style="color:#1565c0">Programmer, c'est quoi ?</span>

Avant de traiter une information, il faut la **représenter** d'une manière qu'une machine puisse manipuler : un nombre, un texte, une valeur vraie ou fausse. C'est l'objet de ce premier bloc.

**Programmer**, c'est écrire une suite d'ordres (des *instructions*) qu'un ordinateur exécutera dans l'ordre. Sans programme, une machine ne sait rien faire.

Python est un **langage de programmation** : un ensemble de mots et de règles d'écriture que l'ordinateur sait interpréter.

### <span style="color:#2e7d32">Premier programme</span>

!!! example "Activité 1 — Hello World"
    Par tradition, tout apprenti programmeur commence par afficher un message à l'écran. Dans l'éditeur de Basthon ou de Capytale, recopie puis exécute :

    ```python
    print("Hello World !")
    ```

    Le message doit apparaître dans la console.

    **Question :** remplace les guillemets doubles `"` par des apostrophes `'`. Le programme fonctionne-t-il toujours ?

??? success "Réponse"
    Oui. Python accepte indifféremment `'...'` et `"..."` pour délimiter du texte. Le choix se fait selon le contenu : si le texte contient une apostrophe, on l'entoure de guillemets doubles.

    ```python
    print("C'est parti !")
    ```

!!! question "À toi de jouer 1.1 ⭐"
    Écris un programme qui affiche ton prénom à l'écran.

## <span style="color:#1565c0">Variables et affectation</span>

Une **variable** est l'association :

- d'un **nom**, qui permet de la retrouver ;
- d'un espace en **mémoire** ;
- d'une **valeur** que l'on y stocke.

En Python, l'affectation se fait avec l'opérateur `=` :

```python
note = 15          # stocke l'entier 15
prenom = "Camille" # stocke la chaîne de caractères "Camille"
```

!!! warning "Le piège du signe ="
    En Python, `=` **ne veut pas dire « est égal à »**. Il veut dire « **reçoit** ».

    `note = 15` se lit : *la variable `note` reçoit la valeur 15*.

    On verra plus loin que le test d'égalité, lui, s'écrit `==`.

### <span style="color:#2e7d32">Afficher le contenu d'une variable</span>

!!! example "Activité 2 — Avec ou sans guillemets"
    Teste successivement ces deux programmes :

    ```python
    moyenne = 15
    print(moyenne)
    ```

    ```python
    moyenne = 15
    print("moyenne")
    ```

    **Question :** qu'est-ce qui change, et pourquoi ?

??? success "Réponse"
    - `print(moyenne)` affiche **15** : Python va chercher la *valeur* stockée dans la variable.
    - `print("moyenne")` affiche **moyenne** : entre guillemets, c'est un simple texte, Python ne cherche aucune variable.

    Les guillemets font toute la différence entre **le nom** et **le contenu**.

!!! question "À toi de jouer 1.2 ⭐"
    Écris un programme qui range la note `12` dans une variable nommée `moyenne`, puis affiche cette moyenne.

!!! tip "Bien nommer ses variables"
    Un nom de variable doit **dire ce qu'elle contient**. `moyenne` est un bon nom ; `x`, `truc` ou `a1` n'en sont pas.

    Règles à respecter : pas d'espace, pas d'accent, pas de tiret, et on ne commence pas par un chiffre. On écrit `nombre_eleves`, pas `nombre élèves`.

### <span style="color:#2e7d32">Permuter deux variables</span>

!!! example "Activité 3 — L'échange raté"
    On veut échanger les valeurs de deux variables `a` et `b`.

    **Proposition de Luc :**

    ```python
    a = 8
    b = -3
    a = b
    b = a
    ```

    Complète le tableau d'exécution, ligne par ligne :

    | Après la ligne | `a` vaut | `b` vaut |
    | --- | --- | --- |
    | `a = 8` | 8 | *(rien)* |
    | `b = -3` | … | … |
    | `a = b` | … | … |
    | `b = a` | … | … |

    L'échange a-t-il fonctionné ?

??? success "Corrigé"
    | Après la ligne | `a` vaut | `b` vaut |
    | --- | --- | --- |
    | `a = 8` | 8 | *(rien)* |
    | `b = -3` | 8 | -3 |
    | `a = b` | **-3** | -3 |
    | `b = a` | -3 | **-3** |

    **Non.** Dès la ligne `a = b`, la valeur 8 est **écrasée** : elle est définitivement perdue. Les deux variables finissent avec la même valeur.

    L'ordre inverse (`b = a` puis `a = b`) échoue exactement de la même façon, en perdant cette fois la valeur -3.

!!! question "À toi de jouer 1.3 ⭐⭐"
    Propose un programme qui échange **vraiment** les valeurs de `a` et `b`.

    **Indice concret :** tu as deux verres, l'un avec de l'eau, l'autre avec du jus. Comment échanger leur contenu sans changer de verre ?

??? success "Corrigé"
    Il faut un **troisième verre** : une variable temporaire qui met une valeur de côté avant qu'elle soit écrasée.

    ```python
    a = 8
    b = -3

    temporaire = a    # on met 8 de côté
    a = b             # a reçoit -3
    b = temporaire    # b reçoit 8

    print(a, b)       # affiche -3 8
    ```

## <span style="color:#1565c0">Faire des calculs</span>

Python connaît les opérations usuelles :

| Opérateur | Rôle | Exemple | Résultat |
| --- | --- | --- | --- |
| `+` `-` `*` | addition, soustraction, multiplication | `3 * 4` | `12` |
| `/` | division (résultat décimal) | `13 / 4` | `3.25` |
| `//` | quotient de la division euclidienne | `13 // 4` | `3` |
| `%` | reste de la division euclidienne | `13 % 4` | `1` |
| `**` | puissance | `2 ** 3` | `8` |

!!! example "Activité 4 — Que vaut `a` à la fin ?"
    Prédis le résultat **avant** d'exécuter, puis vérifie :

    ```python
    a = 1
    b = -1
    a = a * b
    a = a + b
    print(a)
    ```

??? success "Réponse"
    `a = a * b` donne `a = 1 * (-1) = -1`, puis `a = a + b` donne `a = -1 + (-1) = -2`.

    Le programme affiche **-2**.

    Retiens la mécanique : dans `a = a + b`, Python **calcule d'abord** le membre de droite avec les valeurs actuelles, **puis** range le résultat dans `a`.

!!! example "Activité 5 — Incrémenter"
    ```python
    compteur = 11
    print(compteur)
    compteur = compteur + 1   # incrémentation
    print(compteur)
    ```

    Cette instruction `compteur = compteur + 1` reviendra **constamment** dans le cours : c'est ainsi qu'on compte des choses.

!!! question "À toi de jouer 1.4 ⭐⭐ — Combien d'octets pèse une photo ?"
    Une photo de smartphone fait 4032 pixels de large et 3024 pixels de haut. Chaque pixel est codé sur **3 octets** (un pour le rouge, un pour le vert, un pour le bleu).

    Écris un programme qui calcule et affiche le poids de cette photo **en octets**, puis **en mégaoctets** (1 Mo = 1024 × 1024 octets). Arrondis à l'aide de `round(valeur, 1)`.

??? success "Corrigé"
    ```python
    largeur = 4032
    hauteur = 3024
    octets = largeur * hauteur * 3

    print("Poids brut :", octets, "octets")
    print("Soit :", round(octets / 1024 / 1024, 1), "Mo")
    ```

    Résultat :

    ```text
    Poids brut : 36578304 octets
    Soit : 34.9 Mo
    ```

    !!! note "Lien avec le module Images"
        Une vraie photo JPEG fait plutôt 3 à 5 Mo. L'écart vient de la **compression**, que l'on étudiera dans le module *Images numériques*.

!!! info "Séance 2 — Dialoguer avec l'utilisateur"
    Affichage composé, `input`, conversions de type.

## <span style="color:#1565c0">Afficher : la fonction `print`</span>

Une **chaîne de caractères** est un texte, délimité par `"` ou `'`.

`print()` peut afficher plusieurs éléments d'affilée, séparés par des **virgules** :

!!! example "Activité 6"
    ```python
    prenom = "Bob"
    print("Vivement les vacances !")
    print("Mon prénom est :", prenom)
    ```

    Observe : Python ajoute automatiquement une espace à la place de chaque virgule.

!!! question "À toi de jouer 1.5 ⭐"
    Crée trois variables `prenom`, `nom` et `age`, puis affiche une phrase de la forme :

    ```text
    Bonjour, je m'appelle Ada Lovelace, j'ai 36 ans.
    ```

??? success "Corrigé"
    ```python
    prenom = "Ada"
    nom = "Lovelace"
    age = 36

    print("Bonjour, je m'appelle", prenom, nom + ",", "j'ai", age, "ans.")
    ```

    !!! quote "Au fait…"
        Ada Lovelace (1815-1852) est considérée comme **la première personne à avoir écrit un programme informatique**, un siècle avant la construction du premier ordinateur.

## <span style="color:#1565c0">Dialoguer avec l'utilisateur : `input`</span>

La fonction `input()` affiche une question et **récupère ce que l'utilisateur tape au clavier**.

!!! example "Activité 7"
    ```python
    prenom = input("Quel est ton prénom ? ")
    print("Bonjour", prenom)
    ```

!!! danger "Point crucial : `input` renvoie toujours du TEXTE"
    Même si l'utilisateur tape `2`, Python reçoit la **chaîne de caractères** `"2"`, pas le nombre 2.

!!! example "Activité 8 — L'erreur du boulanger"
    Une baguette coûte 1,10 €. Teste ce programme en saisissant `2` :

    ```python
    nombre = input("Combien de baguettes ? ")
    prix = nombre * 1.1
    print("Vous devez payer", prix, "euros.")
    ```

    **Question :** quel message d'erreur obtiens-tu ? Teste maintenant cette version :

    ```python
    nombre = int(input("Combien de baguettes ? "))
    prix = nombre * 1.1
    print("Vous devez payer", round(prix, 2), "euros.")
    ```

??? success "Réponse"
    Le premier programme provoque une erreur du type :

    ```text
    TypeError: can't multiply sequence by non-int of type 'float'
    ```

    Python refuse de multiplier un **texte** par un nombre décimal.

    Dans la seconde version, `int(...)` **convertit** le texte saisi en nombre entier. Le calcul devient possible.

!!! info "Les fonctions de conversion"
    - `int("2")` → `2` (nombre **entier**)
    - `float("2.5")` → `2.5` (nombre **décimal**, appelé *flottant*)
    - `str(2)` → `"2"` (texte)

!!! question "À toi de jouer 1.6 ⭐⭐ — Fil rouge : la fiche élève"
    Écris un programme qui demande à l'utilisateur son **prénom**, puis **deux notes**, et affiche :

    ```text
    Camille, ta moyenne est de 13.5
    ```

    Attention à la conversion des notes !

??? success "Corrigé"
    ```python
    prenom = input("Ton prénom ? ")
    note1 = float(input("Première note ? "))
    note2 = float(input("Deuxième note ? "))

    moyenne = (note1 + note2) / 2

    print(prenom + ", ta moyenne est de", moyenne)
    ```

    On utilise `float` et non `int` : une note peut valoir 13,5.

    **Test** avec `Camille`, `12` et `15` :

    ```text
    Camille, ta moyenne est de 13.5
    ```

!!! question "À toi de jouer 1.7 ⭐⭐ — La borne du parc"
    Tu programmes la borne automatique d'un parc d'attractions. L'entrée coûte **21 €** par adulte et **13 €** par enfant.

    Écris un programme qui demande le nombre d'adultes et le nombre d'enfants, puis affiche le prix total à payer.

??? success "Corrigé"
    ```python
    adultes = int(input("Nombre d'adultes : "))
    enfants = int(input("Nombre d'enfants : "))

    prix = adultes * 21 + enfants * 13

    print("Total à payer :", prix, "€")
    ```

    **Test** avec 2 adultes et 3 enfants : `Total à payer : 81 €`

!!! info "Séance 3 — Les chaînes de caractères"
    Longueur, appartenance, indexation, slicing.

## <span style="color:#1565c0">Les chaînes de caractères</span>

En Python, le type des textes s'appelle `str` (*string*).

### <span style="color:#2e7d32">Afficher des guillemets et des apostrophes</span>

!!! question "À toi de jouer 1.8 ⭐"
    Fais afficher **exactement** ces deux lignes :

    ```text
    C'est bientôt les vacances
    Bonjour se dit "Hello"
    ```

??? success "Corrigé"
    La règle : on délimite avec le symbole que le texte **ne contient pas**.

    ```python
    print("C'est bientôt les vacances")   # apostrophe dedans → guillemets autour
    print('Bonjour se dit "Hello"')       # guillemets dedans → apostrophes autour
    ```

### <span style="color:#2e7d32">Longueur, appartenance, concaténation</span>

| Opération | Syntaxe | Exemple | Résultat |
| --- | --- | --- | --- |
| Longueur | `len(chaine)` | `len("Bonjour")` | `7` |
| Appartenance | `in` | `"B" in "Bonjour"` | `True` |
| Concaténation | `+` | `"Bon" + "jour"` | `"Bonjour"` |
| Répétition | `*` | `"ab" * 3` | `"ababab"` |

!!! example "Activité 9 — Attention à la casse"
    ```python
    chaine = "Bonjour"
    print("b" in chaine)
    print("B" in chaine)
    ```

    **Question :** pourquoi les deux résultats diffèrent-ils ?

??? success "Réponse"
    Le premier affiche `False`, le second `True`.

    Python distingue **majuscules et minuscules** : `"b"` et `"B"` sont deux caractères différents. On parle de **sensibilité à la casse**.

    Conséquence pratique : un mot de passe `Motdepasse` et `motdepasse` ne sont pas le même.

### <span style="color:#2e7d32">Accéder aux caractères : l'indexation</span>

Les caractères d'une chaîne sont **numérotés à partir de 0** :

```text
 B    o    n    j    o    u    r
 0    1    2    3    4    5    6
-7   -6   -5   -4   -3   -2   -1
```

!!! example "Activité 10"
    ```python
    chaine = "Bonjour"
    print(chaine[0])    # B
    print(chaine[1])    # o
    print(chaine[-1])   # r
    print(chaine[-2])   # u
    ```

!!! warning "Le premier caractère a l'indice 0"
    C'est une source d'erreur classique. Dans une chaîne de longueur `n`, les indices valides vont de `0` à `n - 1`. `chaine[7]` sur `"Bonjour"` provoque une erreur.

### <span style="color:#2e7d32">Extraire un morceau : le *slicing*</span>

La syntaxe `chaine[debut:fin:pas]` extrait les caractères de l'indice `debut` **inclus** à l'indice `fin` **exclu**.

!!! example "Activité 11"
    Prédis chaque affichage, puis vérifie :

    ```python
    chaine = "Bonjour"
    print(chaine[0:2])    # ?
    print(chaine[2:5])    # ?
    print(chaine[1:])     # ?
    print(chaine[::2])    # ?
    print(chaine[::-1])   # ?
    ```

??? success "Réponse"
    ```text
    Bo        les indices 0 et 1 (le 2 est exclu)
    njo       les indices 2, 3, 4
    onjour    de l'indice 1 jusqu'à la fin
    Bnor      un caractère sur deux
    ruojnoB   la chaîne à l'envers (pas négatif)
    ```

!!! question "À toi de jouer 1.9 ⭐⭐⭐ — Anonymiser un prénom"
    Pour publier des résultats sans révéler l'identité des élèves, on veut afficher un prénom sous la forme `C......` : la première lettre, puis autant de points que de lettres restantes.

    Écris un programme qui, à partir de `prenom = "Camille"`, affiche `C......`.

    **Indices :** `len()` donne la longueur, et `"." * 3` produit `"..."`.

??? success "Corrigé"
    ```python
    prenom = "Camille"
    anonyme = prenom[0] + "." * (len(prenom) - 1)
    print(anonyme)
    ```

    Résultat : `C......`

    On prend la première lettre `prenom[0]`, puis on répète le point `len(prenom) - 1` fois.

    !!! note "Lien avec le module Données"
        C'est une forme très simple de **pseudonymisation**. On verra dans le module *Données* pourquoi cette technique reste insuffisante pour protéger réellement une identité : dans une classe, `C......` de 7 lettres suffit souvent à retrouver la personne.

## <span style="color:#1565c0">Exercices corrigés</span>

??? question "Exercice 1 ⭐ — Suivre une affectation"
    Que vaut `a` à la fin de ce script ? Réponds **sans exécuter**, puis vérifie.

    ```python
    a = 5
    a = 2 * a
    b = 2 * a
    a = a * a
    a = a - b + 1
    ```

    ??? success "Corrigé"
        Ligne par ligne :

        | Instruction | `a` | `b` |
        | --- | --- | --- |
        | `a = 5` | 5 | — |
        | `a = 2 * a` | 10 | — |
        | `b = 2 * a` | 10 | 20 |
        | `a = a * a` | 100 | 20 |
        | `a = a - b + 1` | **81** | 20 |

        Pour vérifier, on peut insérer des `print` :

        ```python
        a = 5
        a = 2 * a
        print("a devient", a)
        b = 2 * a
        print("b vaut", b)
        a = a * a
        print("a devient", a)
        a = a - b + 1
        print("a devient", a)
        ```

??? question "Exercice 2 ⭐ — Une fiche de contact"
    Crée trois variables `prenom`, `nom` et `num_tel`, puis affiche :

    ```text
    Bonjour, je veux joindre Mélusine Hamphaïte au 0665432100
    ```

    ??? success "Corrigé"
        ```python
        prenom = "Mélusine"
        nom = "Hamphaïte"
        num_tel = "0665432100"

        print("Bonjour, je veux joindre", prenom, nom, "au", num_tel)
        ```

        !!! warning "Pourquoi le numéro est-il entre guillemets ?"
            Parce qu'un numéro de téléphone **n'est pas un nombre** : on ne fait pas de calcul dessus, et le `0` initial disparaîtrait s'il était stocké comme entier (`0665432100` deviendrait `665432100`).

            C'est un premier réflexe de **modélisation des données** : le type qu'on choisit dépend de l'usage, pas de l'apparence.

??? question "Exercice 3 ⭐⭐ — La même chose, avec saisie"
    Reprends l'exercice 2, mais cette fois les trois informations sont **demandées à l'utilisateur**.

    ??? success "Corrigé"
        ```python
        prenom = input("Prénom : ")
        nom = input("Nom : ")
        num_tel = input("Numéro : ")

        print("Bonjour, je veux joindre", prenom, nom, "au", num_tel)
        ```

        Ici, **aucune conversion** n'est nécessaire : les trois valeurs restent du texte.

??? question "Exercice 4 ⭐⭐ — Billetterie de concert"
    Un concert applique trois tarifs : **10 €** par adulte, **8 €** par adolescent de 12 à 18 ans, **gratuit** pour les moins de 12 ans.

    Écris un programme qui demande le nombre de personnes de chaque catégorie et affiche le prix total.

    ??? success "Corrigé"
        ```python
        adultes = int(input("Nombre d'adultes : "))
        ados = int(input("Nombre d'ados (12-18 ans) : "))
        enfants = int(input("Nombre d'enfants (moins de 12 ans) : "))

        prix = adultes * 10 + ados * 8 + enfants * 0

        print("Le prix à payer est", prix, "€")
        ```

        **Test** avec 2, 3 et 1 :

        ```text
        Le prix à payer est 44 €
        ```

        Le terme `enfants * 0` est inutile au calcul, mais on le garde pour que le programme **documente le tarif** : un lecteur voit immédiatement que la gratuité a été prise en compte.

??? question "Exercice 5 ⭐⭐⭐ — Jouer avec les chaînes"
    À partir de `chaine1 = "algorithmique"`, construis :

    - `chaine2` : le premier et le dernier caractère ;
    - `chaine3` : les deux premiers suivis des deux derniers ;
    - `chaine4` : les caractères d'indice **pair** ;
    - `chaine5` : les caractères d'indice **impair** ;
    - `chaine6` : la chaîne inversée.

    ??? success "Corrigé"
        ```python
        chaine1 = "algorithmique"

        chaine2 = chaine1[0] + chaine1[-1]
        chaine3 = chaine1[:2] + chaine1[-2:]
        chaine4 = chaine1[::2]
        chaine5 = chaine1[1::2]
        chaine6 = chaine1[::-1]

        print(chaine2)
        print(chaine3)
        print(chaine4)
        print(chaine5)
        print(chaine6)
        ```

        Résultat :

        ```text
        ae
        alue
        agrtmqe
        loihiu
        euqimhtirogla
        ```

??? question "Exercice 6 ⭐⭐⭐ — Pourquoi il ne faut pas comparer deux nombres décimaux"
    Saisis ce code, **prédis** l'affichage, puis exécute :

    ```python
    a = 3
    b = 4
    c = 5
    print(c ** 2 == a ** 2 + b ** 2)
    ```

    Complète maintenant avec :

    ```python
    a = a / 10
    b = b / 10
    c = c / 10
    print(a, b, c)
    print(c ** 2 == a ** 2 + b ** 2)
    ```

    Que constates-tu ? Comment l'expliquer ?

    ??? success "Corrigé"
        Le premier test affiche `True` : (3, 4, 5) est un triplet pythagoricien.

        Le second affiche… `False`, alors que **mathématiquement** l'égalité reste vraie : si `c² = a² + b²`, alors `(c/10)² = (a/10)² + (b/10)²`.

        **Explication.** L'ordinateur représente les entiers de façon exacte, mais **pas les nombres décimaux**. Ces derniers sont stockés sous forme de *flottants*, en base 2, avec un nombre fini de chiffres. Or 0,3 n'a pas d'écriture finie en base 2 : la valeur stockée est une **approximation**.

        On peut le voir directement :

        ```python
        print(0.1 + 0.2)
        ```

        ```text
        0.30000000000000004
        ```

        !!! danger "Règle à retenir"
            **On ne compare jamais deux flottants avec `==`.** On teste plutôt si leur écart est très petit :

            ```python
            from math import isclose
            print(isclose(c ** 2, a ** 2 + b ** 2))   # True
            ```

        Cette limite n'est pas un défaut de Python : elle est commune à tous les langages, et elle est une conséquence directe du fait qu'un ordinateur travaille en **binaire** avec une mémoire finie.

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. Que fait l'instruction `age = 15` ?
    2. Quelle est la différence entre `print(note)` et `print("note")` ?
    3. Que renvoie `input()` : un nombre ou du texte ?
    4. Que vaut `len("SNT")` ?
    5. Que vaut `"Python"[0]` ? Et `"Python"[-1]` ?
    6. Pourquoi `int(input(...))` est-il souvent nécessaire ?

??? success "Réponses"
    1. Elle **range** la valeur 15 dans une variable nommée `age` (le `=` signifie « reçoit »).
    2. `print(note)` affiche la **valeur** contenue dans la variable ; `print("note")` affiche le **mot** « note ».
    3. Toujours du **texte** (type `str`), même si l'utilisateur tape des chiffres.
    4. `3`.
    5. `"P"` et `"n"`.
    6. Parce que `input` renvoie du texte : sans conversion, aucun calcul arithmétique n'est possible.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel de la page"
    - Une **variable** associe un nom à une valeur ; `=` signifie « reçoit », pas « est égal à ».
    - `print()` affiche ; les **virgules** séparent les éléments affichés.
    - `input()` renvoie **toujours du texte** → convertir avec `int()` ou `float()` pour calculer.
    - Les caractères d'une chaîne sont indexés **à partir de 0**.
    - On ne compare **jamais** deux nombres décimaux avec `==`.



