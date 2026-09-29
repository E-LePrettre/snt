---
author: Elisabeth Le Prettre (LePrettre)
title: 01c Les listes
---

# Bloc C — Traiter un jeu de données

!!! abstract "Au programme"
    Les listes · les fonctions (`def`, `return`) · projet de fin de module

!!! info "Séance 7 — Listes et fonctions"
    Création et parcours d'une liste, définition de fonctions.

## <span style="color:#1565c0">Les listes</span>

Jusqu'ici, une variable ne contenait **qu'une seule valeur**. Pour stocker les 30 notes d'une classe, il faudrait 30 variables — impraticable.

Une **liste** stocke plusieurs valeurs dans une seule structure :

```python
fruits = ["pomme", "orange", "fraise"]
notes = [12, 8, 15, 17, 9]
```

Une liste s'écrit entre **crochets**, les éléments séparés par des **virgules**.

### <span style="color:#2e7d32">Accéder à un élément</span>

Comme pour les chaînes, les éléments sont numérotés **à partir de 0**.

!!! example "Activité 1 — Prédire avant d'exécuter"
    ```python
    fruits = ["pomme", "orange", "fraise"]
    print(fruits[1])
    ```

    Quel est le résultat attendu ? Vérifie.

??? success "Réponse"
    `orange`.

    `fruits[0]` vaut `"pomme"`, `fruits[1]` vaut `"orange"`, `fruits[2]` vaut `"fraise"`.

    Et comme pour les chaînes, `fruits[-1]` renvoie le **dernier** élément.

### <span style="color:#2e7d32">Les opérations sur les listes</span>

| Opération | Syntaxe | Effet |
| --- | --- | --- |
| Longueur | `len(L)` | nombre d'éléments |
| Lire | `L[k]` | l'élément d'indice `k` |
| Modifier | `L[k] = valeur` | remplace l'élément d'indice `k` |
| Ajouter à la fin | `L.append(valeur)` | allonge la liste |
| Retirer | `L.pop(k)` | retire l'élément d'indice `k` et le renvoie |
| Tester la présence | `valeur in L` | `True` ou `False` |

!!! example "Activité 2 — Manipuler une liste"
    Prédis le résultat de **chaque** `print`, puis exécute le programme en entier :

    ```python
    semaine = ["lundi", "mardi", "mercredi", "jeudi", "vendredi"]

    print(len(semaine))

    semaine.append("samedi")
    print(semaine)

    semaine[0] = "LUNDI"
    print(semaine)

    retire = semaine.pop(1)
    print(retire)
    print(semaine)

    print("dimanche" in semaine)
    ```

??? success "Réponse"
    ```text
    5
    ['lundi', 'mardi', 'mercredi', 'jeudi', 'vendredi', 'samedi']
    ['LUNDI', 'mardi', 'mercredi', 'jeudi', 'vendredi', 'samedi']
    mardi
    ['LUNDI', 'mercredi', 'jeudi', 'vendredi', 'samedi']
    False
    ```

    Point important : `pop(1)` fait **deux choses** à la fois — il retire l'élément **et** renvoie sa valeur, qu'on peut donc récupérer dans une variable.

!!! warning "`append` modifie la liste, il ne la renvoie pas"
    On écrit `L.append(5)`, **jamais** `L = L.append(5)`. Cette seconde écriture détruit la liste (elle la remplace par `None`, c'est-à-dire « rien »).

### <span style="color:#2e7d32">Parcourir une liste</span>

C'est ici que les listes et les boucles se rejoignent.

!!! example "Activité 3 — Deux façons de parcourir"
    ```python
    notes = [12, 8, 15, 17, 9]

    # Parcours par élément — le plus lisible
    for note in notes:
        print(note)

    # Parcours par indice — utile quand on a besoin de la position
    for i in range(len(notes)):
        print("Note n°", i, ":", notes[i])
    ```

??? success "Quand utiliser l'un ou l'autre ?"
    - **Par élément** (`for note in notes`) : dès qu'on veut juste lire les valeurs. C'est la forme à privilégier.
    - **Par indice** (`for i in range(len(notes))`) : quand on a besoin de la **position** de l'élément, ou qu'on veut **modifier** la liste.

## <span style="color:#1565c0">Les fonctions</span>

Une **fonction** est un bloc de code qu'on écrit **une fois** et qu'on réutilise autant qu'on veut, avec des valeurs différentes.

```python
def nom_de_la_fonction(parametre1, parametre2):
    # bloc d'instructions
    return valeur
```

- `def` annonce la définition ;
- les **paramètres** sont les valeurs que la fonction reçoit ;
- `return` indique **ce que la fonction renvoie**.

!!! example "Activité 4 — Une première fonction"
    ```python
    def carre(x):
        return x ** 2
    ```

    Exécute ce code, puis teste **dans la console** :

    ```text
    >>> carre(2)
    >>> carre(9)
    ```

??? success "Réponse"
    ```text
    4
    81
    ```

    En mathématiques on écrit `f(x) = x²` et on calcule `f(2)`. En Python, c'est exactement la même logique.

    Remarque : rien ne s'affiche quand on exécute la **définition** seule. Une fonction ne fait rien tant qu'on ne l'**appelle** pas.

!!! danger "L'erreur n°1 : oublier le `return`"
    Compare ces deux fonctions :

    ```python
    def double_affiche(x):
        print(x * 2)      # affiche, mais ne renvoie rien

    def double_renvoie(x):
        return x * 2      # renvoie une valeur utilisable
    ```

    Teste :

    ```python
    a = double_affiche(5)    # affiche 10, puis a vaut None
    b = double_renvoie(5)    # n'affiche rien, mais b vaut 10
    print(a + 1)             # ERREUR
    print(b + 1)             # affiche 11
    ```

    **`print` montre à l'humain. `return` donne au programme.** Une fonction sans `return` ne peut pas être réutilisée dans un calcul.

!!! example "Activité 5 — Une fonction à deux paramètres"
    ```python
    def somme(a, b):
        return a + b
    ```

    ```text
    >>> somme(3, 5)
    8
    >>> somme(1.5, 2.5)
    4.0
    ```

    **Question :** que renvoie `somme("Bon", "jour")` ? Pourquoi ?

??? success "Réponse"
    `"Bonjour"`.

    L'opérateur `+` fonctionne aussi bien sur les nombres (addition) que sur les chaînes (concaténation). La fonction ne vérifie pas le type de ce qu'elle reçoit.

    C'est souple, mais aussi une **source de bugs** : `somme("3", "5")` renvoie `"35"` et non `8`.

### <span style="color:#2e7d32">Fil rouge : la fonction `mention`</span>

!!! question "À toi de jouer 3.1 ⭐⭐ — Transformer un programme en fonction"
    Reprends le programme des mentions de la page précédente et transforme-le en une **fonction** `mention(note)` qui **renvoie** la mention sous forme de texte.

    Elle doit fonctionner ainsi :

    ```text
    >>> mention(18)
    'Très bien'
    >>> mention(7)
    'Insuffisant'
    ```

??? success "Corrigé"
    ```python
    def mention(note):
        if note >= 16:
            return "Très bien"
        elif note >= 14:
            return "Bien"
        elif note >= 12:
            return "Assez bien"
        elif note >= 10:
            return "Admis"
        else:
            return "Insuffisant"
    ```

    Test sur plusieurs valeurs :

    ```python
    for n in [18, 15, 13, 10, 7]:
        print(n, "->", mention(n))
    ```

    ```text
    18 -> Très bien
    15 -> Bien
    13 -> Assez bien
    10 -> Admis
    7 -> Insuffisant
    ```

    !!! tip "Pourquoi `return` et pas `print` ?"
        Parce qu'on veut **réutiliser** le résultat : l'afficher, mais aussi le comparer, le stocker, l'ajouter à une liste. Une fonction qui se contente d'afficher ferme toutes ces portes.

        Remarque aussi qu'ici, `return` sort **immédiatement** de la fonction : dès qu'une mention est renvoyée, les tests suivants ne sont pas évalués.

## <span style="color:#1565c0">Exercices corrigés</span>

??? question "Exercice 1 ⭐ — Fonction cube"
    Écris une fonction `cube(x)` qui renvoie le cube de `x`. Teste avec `cube(2)`, qui doit renvoyer 8.

    ??? success "Corrigé"
        ```python
        def cube(x):
            return x ** 3
        ```

        ```text
        >>> cube(2)
        8
        >>> cube(5)
        125
        ```

??? question "Exercice 2 ⭐ — Périmètre d'un rectangle"
    Écris une fonction `perimetre(l, L)` qui renvoie le périmètre d'un rectangle.

    ??? success "Corrigé"
        ```python
        def perimetre(l, L):
            return 2 * (l + L)
        ```

        ```text
        >>> perimetre(5, 12)
        34
        ```

??? question "Exercice 3 ⭐⭐ — Le minimum de deux nombres"
    Écris une fonction `mini(a, b)` qui renvoie le plus petit des deux nombres.

    ??? success "Corrigé"
        ```python
        def mini(a, b):
            if a < b:
                return a
            else:
                return b
        ```

        ```text
        >>> mini(12, 9)
        9
        >>> mini(4, 4)
        4
        ```

??? question "Exercice 4 ⭐⭐ — Somme des n premiers entiers"
    Écris une fonction `somme(n)` qui renvoie `1 + 2 + ... + n`.

    ??? success "Corrigé"
        ```python
        def somme(n):
            total = 0
            for i in range(n + 1):
                total = total + i
            return total
        ```

        ```text
        >>> somme(8)
        36
        >>> somme(100)
        5050
        ```

        Le `n + 1` dans `range` est indispensable pour inclure `n` lui-même.

??? question "Exercice 5 ⭐⭐⭐ — Le signe d'un produit"
    Écris une fonction `signe_prod(a, b)` qui renvoie `True` si le produit de `a` par `b` est strictement positif, `False` sinon. **Sans calculer le produit.**

    ??? success "Corrigé"
        Le produit est strictement positif si les deux nombres sont de **même signe**, tous deux non nuls.

        ```python
        def signe_prod(a, b):
            if (a > 0 and b > 0) or (a < 0 and b < 0):
                return True
            else:
                return False
        ```

        ```text
        >>> signe_prod(-12, -4)
        True
        >>> signe_prod(1, -5)
        False
        >>> signe_prod(0, 5)
        False
        ```

        Les parenthèses ne sont pas obligatoires (`and` est prioritaire sur `or`) mais rendent l'intention **beaucoup** plus lisible.

        **Version plus courte** : une condition renvoie déjà `True` ou `False`, on peut donc la renvoyer directement.

        ```python
        def signe_prod(a, b):
            return (a > 0 and b > 0) or (a < 0 and b < 0)
        ```

??? question "Exercice 6 ⭐⭐⭐ — À la manière de Perec"
    L'écrivain Georges Perec a écrit un roman entier, *La Disparition*, sans jamais employer la lettre « e ».

    Écris une fonction `sans_e(phrase)` qui remplace tous les « e » d'une phrase par une espace et **renvoie** la nouvelle phrase.

    ??? success "Corrigé"
        On construit une **nouvelle** chaîne caractère par caractère : les chaînes ne se modifient pas sur place.

        ```python
        def sans_e(phrase):
            resultat = ""
            for lettre in phrase:
                if lettre == "e":
                    resultat = resultat + " "
                else:
                    resultat = resultat + lettre
            return resultat
        ```

        ```text
        >>> sans_e("Je suis un eleve de seconde et j'apprends le python")
        "J  suis un  l v  d  s cond   t j'appr nds l  python"
        ```

        !!! danger "L'erreur à ne pas commettre"
            Si on oublie la ligne `return resultat`, la fonction construit correctement la phrase… puis la **jette**. `sans_e(...)` renvoie alors `None`.

            Une fonction qui ne renvoie rien ne sert à rien : c'est le bug le plus fréquent sur ce type d'exercice.

??? question "Exercice 7 ⭐⭐⭐ — Remplir une cuve"
    Une cuve de récupération d'eau a une contenance de **1000 litres**.

    a) Écris une fonction `remplir()` qui renvoie le nombre de jours nécessaires pour la remplir, sachant qu'elle reçoit **3 litres par jour**.
    b) Écris une fonction `remplir(quantite)` où `quantite` est le nombre de litres reçus par jour.

    ??? success "Corrigé"
        On ne connaît pas le nombre de jours à l'avance → boucle `while`.

        ```python
        # a) version simple
        def remplir():
            cuve = 0
            jours = 0
            while cuve < 1000:
                cuve = cuve + 3
                jours = jours + 1
            return jours
        ```

        ```text
        >>> remplir()
        334
        ```

        334 et non 333 : après 333 jours la cuve contient 999 L, il faut donc un jour de plus.

        ```python
        # b) version paramétrée
        def remplir(quantite):
            cuve = 0
            jours = 0
            while cuve < 1000:
                cuve = cuve + quantite
                jours = jours + 1
            return jours
        ```

        ```text
        >>> remplir(3)
        334
        >>> remplir(5)
        200
        ```

        !!! tip "L'intérêt du paramètre"
            La version b) contient la version a) : `remplir(3)` donne le même résultat. Un **paramètre** transforme un programme qui répond à une question en un programme qui répond à toute une famille de questions.

        !!! warning "Attention au cas limite"
            Que se passe-t-il avec `remplir(0)` ? La cuve ne se remplit jamais : **boucle infinie**. Une fonction robuste devrait le prévoir :

            ```python
            def remplir(quantite):
                if quantite <= 0:
                    return "Impossible : il faut une quantité positive"
                cuve = 0
                jours = 0
                while cuve < 1000:
                    cuve = cuve + quantite
                    jours = jours + 1
                return jours
            ```

??? question "Exercice 8 ⭐⭐ — Population d'un village"
    Un village compte 2300 habitants et gagne 120 habitants par an.

    Écris une fonction `population(n)` qui renvoie la population au bout de `n` années.

    ??? success "Corrigé"
        ```python
        def population(n):
            habitants = 2300
            for i in range(n):
                habitants = habitants + 120
            return habitants
        ```

        ```text
        >>> population(0)
        2300
        >>> population(1)
        2420
        >>> population(10)
        3500
        ```

        Vérifie toujours ta fonction avec `n = 0` : c'est le cas limite qui révèle les erreurs de boucle.

## <span style="color:#1565c0">Fil rouge : les notes de la classe</span>

On arrive au bout du fil rouge. On dispose maintenant de tout ce qu'il faut pour traiter un vrai jeu de données.

```python
notes = [12, 8, 15, 17, 9, 11, 14, 6, 18, 13]
```

??? question "Exercice 9 ⭐⭐ — La moyenne"
    Écris une fonction `moyenne(liste)` qui renvoie la moyenne des valeurs d'une liste.

    ??? success "Corrigé"
        ```python
        def moyenne(liste):
            somme = 0
            for valeur in liste:
                somme = somme + valeur
            return somme / len(liste)
        ```

        ```text
        >>> notes = [12, 8, 15, 17, 9, 11, 14, 6, 18, 13]
        >>> moyenne(notes)
        12.3
        ```

        On retrouve le schéma **initialiser → accumuler → renvoyer**, exactement comme avec les boucles page 2. La seule nouveauté : le résultat est **renvoyé** au lieu d'être affiché.

        !!! note "Cette fonction va resservir"
            `moyenne()` sera **réutilisée telle quelle** dans le module *Données*, appliquée cette fois à un fichier de données réelles.

??? question "Exercice 10 ⭐⭐ — La meilleure note"
    Écris une fonction `maximum(liste)` qui renvoie la plus grande valeur d'une liste, **sans utiliser** la fonction `max` de Python.

    ??? success "Corrigé"
        L'idée : on retient un « champion » provisoire, qu'on remplace dès qu'on trouve mieux.

        ```python
        def maximum(liste):
            record = liste[0]
            for valeur in liste:
                if valeur > record:
                    record = valeur
            return record
        ```

        ```text
        >>> maximum(notes)
        18
        ```

        !!! warning "Pourquoi initialiser avec `liste[0]` et pas avec 0 ?"
            Avec `record = 0`, la fonction donnerait un résultat faux sur une liste de nombres **tous négatifs** (elle renverrait 0, qui n'est pas dans la liste).

            En partant du premier élément, on garantit que le résultat appartient bien à la liste.

??? question "Exercice 11 ⭐⭐ — Combien d'élèves ont la moyenne ?"
    Écris une fonction `nb_admis(liste)` qui renvoie le nombre de notes supérieures ou égales à 10.

    ??? success "Corrigé"
        ```python
        def nb_admis(liste):
            compteur = 0
            for note in liste:
                if note >= 10:
                    compteur = compteur + 1
            return compteur
        ```

        ```text
        >>> nb_admis(notes)
        7
        ```

        Pour obtenir un **pourcentage** :

        ```python
        def taux_admis(liste):
            return round(nb_admis(liste) / len(liste) * 100, 1)
        ```

        ```text
        >>> taux_admis(notes)
        70.0
        ```

        Remarque : `taux_admis` **appelle** `nb_admis`. Construire des fonctions à partir d'autres fonctions, c'est le principe même de la programmation.

??? question "Exercice 12 ⭐⭐⭐ — Anonymiser une liste de prénoms"
    On veut publier les résultats de la classe sans révéler les identités.

    Écris une fonction `anonymise(prenoms)` qui reçoit une liste de prénoms et renvoie une **nouvelle liste** où chaque prénom est réduit à son initiale suivie de points.

    ```text
    >>> anonymise(["Camille", "Lou", "Mohamed"])
    ['C......', 'L..', 'M......']
    ```

    ??? success "Corrigé"
        ```python
        def anonymise(prenoms):
            resultat = []
            for prenom in prenoms:
                resultat.append(prenom[0] + "." * (len(prenom) - 1))
            return resultat
        ```

        ```text
        >>> anonymise(["Camille", "Lou", "Mohamed"])
        ['C......', 'L..', 'M......']
        ```

        On reconnaît le schéma de construction d'une liste : **liste vide → `append` dans la boucle → renvoyer**.

        !!! quote "Est-ce vraiment anonyme ?"
            Non. Dans une classe de 30 élèves, un prénom commençant par `M` et comptant 7 lettres n'en désigne souvent qu'un seul.

            C'est une **pseudonymisation**, pas une anonymisation. La distinction est juridique autant que technique : le RGPD considère les données pseudonymisées comme **toujours personnelles**. On y reviendra dans le module *Données*.

!!! info "Séance 8 — Projet et bilan"
    Réinvestissement complet du module, ouverture vers le module Données.

## <span style="color:#1565c0">Projet de fin de module</span>

!!! question "Avant de programmer : d'où viennent ces données ?"
    Le jeu de données ci-dessous représente une classe réelle. Avant d'écrire la moindre ligne, réponds à ces trois questions :

    1. Que représente exactement chaque colonne ? Une note sur combien ? De quelle matière ?
    2. Qui a le droit de consulter ces données ? L'élève, ses parents, ses camarades ?
    3. Pourrait-on publier ce tableau tel quel sur le site du lycée ? Et une fois les prénoms anonymisés ?

    Ces questions ne sont pas un préambule : **elles font partie du traitement**. On les retrouvera dans le module *Les données*.

!!! success "Projet — Traiter un jeu de données ⭐⭐⭐"
    En réunissant tout ce que tu as construit, écris un programme complet qui :

    1. part de deux listes, `prenoms` et `notes`, de même longueur ;
    2. affiche pour chaque élève son prénom **anonymisé** et sa **mention** ;
    3. affiche la **moyenne** de la classe, la **meilleure note** et le **taux de réussite**.

    ```python
    prenoms = ["Camille", "Lou", "Mohamed", "Sarah", "Tom",
               "Inès", "Noah", "Léa", "Gabriel", "Jade"]
    notes   = [12, 8, 15, 17, 9, 11, 14, 6, 18, 13]
    ```

??? success "Corrigé du projet"
    ```python
    prenoms = ["Camille", "Lou", "Mohamed", "Sarah", "Tom",
               "Inès", "Noah", "Léa", "Gabriel", "Jade"]
    notes   = [12, 8, 15, 17, 9, 11, 14, 6, 18, 13]


    def anonymise(prenom):
        return prenom[0] + "." * (len(prenom) - 1)


    def mention(note):
        if note >= 16:
            return "Très bien"
        elif note >= 14:
            return "Bien"
        elif note >= 12:
            return "Assez bien"
        elif note >= 10:
            return "Admis"
        else:
            return "Insuffisant"


    def moyenne(liste):
        somme = 0
        for valeur in liste:
            somme = somme + valeur
        return somme / len(liste)


    def maximum(liste):
        record = liste[0]
        for valeur in liste:
            if valeur > record:
                record = valeur
        return record


    def nb_admis(liste):
        compteur = 0
        for note in liste:
            if note >= 10:
                compteur = compteur + 1
        return compteur


    # --- Bulletin individuel ---
    print("=== BULLETIN DE LA CLASSE ===")
    for i in range(len(prenoms)):
        print(anonymise(prenoms[i]), ":", notes[i], "->", mention(notes[i]))

    # --- Statistiques ---
    print()
    print("=== STATISTIQUES ===")
    print("Effectif        :", len(notes))
    print("Moyenne         :", round(moyenne(notes), 2))
    print("Meilleure note  :", maximum(notes))
    print("Taux de réussite:", round(nb_admis(notes) / len(notes) * 100, 1), "%")
    ```

    ```text
    === BULLETIN DE LA CLASSE ===
    C...... : 12 -> Assez bien
    L.. : 8 -> Insuffisant
    M...... : 15 -> Bien
    S.... : 17 -> Très bien
    T.. : 9 -> Insuffisant
    I... : 11 -> Admis
    N... : 14 -> Bien
    L.. : 6 -> Insuffisant
    G...... : 18 -> Très bien
    J... : 13 -> Assez bien

    === STATISTIQUES ===
    Effectif        : 10
    Moyenne         : 12.3
    Meilleure note  : 18
    Taux de réussite: 70.0 %
    ```

    !!! tip "Pourquoi un parcours par indice ici ?"
        Parce qu'on lit **deux listes en parallèle** : à l'indice `i`, `prenoms[i]` et `notes[i]` désignent la même personne. C'est le cas typique où `for i in range(len(...))` s'impose.

    !!! note "Prolongements possibles"
        - Trier les élèves par note décroissante.
        - Compter le nombre d'élèves par mention.
        - Charger les données depuis un **fichier CSV** plutôt que de les écrire en dur → c'est exactement le point de départ du module *Données*.

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. Quel est l'indice du premier élément d'une liste ?
    2. Quelle différence entre `L.append(5)` et `L = L.append(5)` ?
    3. Quelle différence entre `print` et `return` dans une fonction ?
    4. Que renvoie une fonction qui n'a pas de `return` ?
    5. Quand faut-il parcourir une liste **par indice** plutôt que par élément ?
    6. Pourquoi initialiser `maximum` avec `liste[0]` plutôt qu'avec 0 ?

??? success "Réponses"
    1. **0**.
    2. La première **modifie** la liste (c'est la bonne écriture) ; la seconde **détruit** la liste, qui devient `None`.
    3. `print` **affiche** à l'écran, à destination de l'humain. `return` **renvoie** une valeur au programme, qui peut la réutiliser.
    4. `None`, c'est-à-dire « rien ».
    5. Quand on a besoin de la **position**, ou qu'on parcourt **deux listes en parallèle**.
    6. Parce que 0 donnerait un résultat faux sur une liste ne contenant que des valeurs négatives.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du module"
    - Une **liste** regroupe plusieurs valeurs ; on y accède par un indice, **à partir de 0**.
    - Une **fonction** s'écrit une fois et se réutilise : `def`, paramètres, `return`.
    - `print` montre à l'humain, **`return` donne au programme**.
    - Schéma récurrent : **initialiser → parcourir → renvoyer** (somme, compteur, maximum, nouvelle liste).
    - Tester une fonction, c'est aussi tester ses **cas limites** : liste vide, valeur nulle, valeurs négatives.

!!! abstract "Et maintenant ?"
    Tu sais désormais écrire, lire et tester un programme. Le [bloc D](01e_ia.md) te propose de t'en servir pour juger du code produit par une **intelligence artificielle**.

    Plus loin dans l'année, les fonctions `moyenne()`, `maximum()` et `nb_admis()` que tu viens d'écrire seront **reprises telles quelles** dans le module *Les données*, appliquées cette fois à un vrai fichier.




