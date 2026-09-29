---
author: Elisabeth Le Prettre (LePrettre)
title: 06d Générer
---

# Bloc D — Générer

!!! abstract "Au programme"
    Prédire le mot suivant · construire un mini-modèle de langue · le rôle du hasard · pourquoi une IA « hallucine »

!!! info "Séances 6 et 7"
    Séance 6 : faire générer du texte à un programme. Séance 7 : comprendre le hasard et les limites.

!!! quote "Ce qu'on va démystifier"
    Les IA génératives de texte — celles que tu utilises — paraissent magiques. Elles ne le sont pas.

    À la fin de ces deux séances, tu auras écrit un générateur de texte. Le tien sera minuscule ; le principe est le même que celui des grands modèles.

## <span style="color:#1565c0">L'idée centrale : prédire le mot suivant</span>

!!! info "Le principe, sans mathématiques"
    Un modèle de langue fait **une seule chose** : étant donné un début de texte, il prédit le **mot suivant le plus probable**. Puis il recommence, avec ce nouveau mot ajouté. Et encore. Et encore.

    Générer un texte, c'est prédire le mot suivant, des milliers de fois de suite.

C'est tout. Il n'y a pas de compréhension, pas d'intention, pas de plan. Juste : *quel mot vient probablement après ?*

## <span style="color:#1565c0">Apprendre les enchaînements</span>

Comment savoir quel mot suit probablement un autre ? En **comptant**, dans un grand texte, ce qui suit chaque mot.

```python
corpus = "le chat mange le poisson le chat dort le chien mange le pain le chien dort"
mots = corpus.split(" ")
```

!!! question "À toi de jouer D.1 ⭐⭐"
    Écris `suivants(mot)` qui renvoie la liste de tous les mots qui suivent `mot` dans le corpus.

??? success "Corrigé"
    ```python
    def suivants(mot):
        resultat = []
        for i in range(len(mots) - 1):
            if mots[i] == mot:
                resultat.append(mots[i + 1])
        return resultat
    ```

    ```text
    >>> suivants("le")
    ['chat', 'poisson', 'chat', 'chien', 'pain', 'chien']
    >>> suivants("chat")
    ['mange', 'dort']
    >>> suivants("mange")
    ['le', 'le']
    ```

    Le programme a **appris du corpus** ce qui suit chaque mot. Après « le », on trouve surtout « chat » et « chien » ; après « mange », toujours « le ».

    !!! note "C'est de l'apprentissage"
        Aucune règle de grammaire n'a été écrite. Le programme a simplement **observé les régularités** du texte. C'est exactement l'esprit du bloc A.

## <span style="color:#1565c0">Le mot le plus probable</span>

!!! question "À toi de jouer D.2 ⭐⭐ — Le plus fréquent"
    Écris `plus_frequent(liste)` qui renvoie le mot le plus fréquent d'une liste. Quel mot suit le plus souvent « le » ?

??? success "Corrigé"
    ```python
    def plus_frequent(liste):
        compte = {}
        for mot in liste:
            if mot in compte:
                compte[mot] = compte[mot] + 1
            else:
                compte[mot] = 1

        meilleur = None
        record = -1
        for mot in compte:
            if compte[mot] > record:
                record = compte[mot]
                meilleur = mot
        return meilleur


    print(plus_frequent(suivants("le")))
    ```

    ```text
    chat
    ```

    !!! tip "Le dictionnaire"
        `compte = {}` crée un **dictionnaire** : il associe à chaque mot son nombre d'occurrences. C'est une structure très pratique pour compter — plus directe que les listes utilisées jusqu'ici.

        C'est la seule nouveauté technique du module, et elle est facultative : on pourrait le faire avec des listes, en plus long.

## <span style="color:#1565c0">Générer une phrase</span>

On a tout ce qu'il faut : partir d'un mot, prendre un suivant, recommencer.

!!! example "Activité 1 — Le générateur"
    ```python
    import random

    def generer(depart, longueur):
        phrase = [depart]
        mot = depart
        for i in range(longueur):
            possibles = suivants(mot)
            if len(possibles) == 0:
                break
            mot = random.choice(possibles)
            phrase.append(mot)
        return " ".join(phrase)


    print(generer("le", 6))
    ```

    Lance-le plusieurs fois. Que remarques-tu ?

??? success "Résultats possibles"
    ```text
    le chien dort le chat dort le
    le poisson le chat mange le chien
    le chat mange le chat mange le
    le poisson le chat dort le pain
    ```

    Chaque exécution donne une phrase **différente**, et pourtant toujours « à la manière » du corpus : les enchaînements sont plausibles, même si le sens est absent.

    !!! success "Tu viens d'écrire un modèle de langue"
        Minuscule, mais authentique. Le principe des grands modèles est le même :

        - le tien regarde **un** mot en arrière ; les grands en regardent des milliers ;
        - le tien a appris sur **une** phrase ; eux sur des milliards de textes ;
        - le tien choisit parmi quelques mots ; eux pondèrent des dizaines de milliers de possibilités.

        Mais la mécanique de fond — **prédire le mot suivant, encore et encore** — est identique.

## <span style="color:#1565c0">Le rôle du hasard</span>

!!! info "Séance 7"

Pourquoi `random.choice` ? Pourquoi ne pas toujours prendre le mot le plus probable ?

!!! example "Activité 2 — Toujours le plus probable"
    ```python
    def generer_prudent(depart, longueur):
        phrase = [depart]
        mot = depart
        for i in range(longueur):
            possibles = suivants(mot)
            if len(possibles) == 0:
                break
            mot = plus_frequent(possibles)
            phrase.append(mot)
        return " ".join(phrase)


    print(generer_prudent("le", 8))
    ```

??? success "Résultat"
    ```text
    le chat mange le chat mange le chat
    ```

    En prenant **toujours** le plus probable, on tombe dans une **boucle** : le chat mange le chat mange le chat… Le texte est correct mais totalement répétitif.

    !!! tip "Le compromis"
        - **Trop de hasard** → du n'importe quoi.
        - **Pas de hasard** → de la répétition sans fin.

        Les vrais modèles règlent ce curseur avec un paramètre appelé **température** :

        - température basse → réponses prudentes, répétitives, prévisibles ;
        - température haute → réponses variées, créatives, parfois incohérentes.

        C'est le même arbitrage que dans ton mini-modèle. Rien de mystérieux : un curseur entre sûreté et variété.

## <span style="color:#1565c0">Pourquoi une IA « hallucine »</span>

!!! danger "Le point le plus important du module"
    Ton générateur produit « le chat mange le pain » aussi facilement que « le chat mange le poisson ». Les deux sont **également plausibles** selon le corpus. Il n'a **aucun moyen de savoir** que l'un est vrai et l'autre douteux.

    Les grands modèles font exactement la même chose, en plus sophistiqué. Quand une IA affirme un fait faux avec assurance — une date inventée, une citation qui n'existe pas, une référence fabriquée — on dit qu'elle **hallucine**.

!!! quote "Ce n'est pas un bug"
    Une hallucination n'est pas une panne. C'est le **fonctionnement normal** d'un système qui produit du plausible.

    Le modèle ne distingue pas le vrai du faux : il produit ce qui **ressemble** à une réponse correcte. Le plus souvent, plausible et vrai coïncident. Parfois non — et rien, dans le mécanisme, ne signale la différence.

    C'est **exactement** ce que tu avais découvert dès le bloc D de M0 : les trois codes étaient plausibles et faux, et aucun ne « plantait ». Un an plus tard, tu comprends maintenant *pourquoi*.

!!! example "Activité 3 — Anticiper les hallucinations"
    Pour chacune de ces demandes à une IA générative, dis si le risque d'hallucination est faible ou élevé, et pourquoi.

    1. « Résume ce texte que je te donne. »
    2. « Donne-moi la date de naissance de mon voisin. »
    3. « Cite trois articles scientifiques sur ce sujet. »
    4. « Réécris ce paragraphe dans un style plus simple. »

??? success "Corrigé"
    1. **Faible.** Toute l'information est fournie ; le modèle reformule ce qu'il a sous les yeux.
    2. **Élevé — et pire, invérifiable.** Le modèle n'a aucune raison de connaître ton voisin. Il produira une date *plausible*, donc probablement fausse.
    3. **Très élevé.** C'est le cas classique : le modèle connaît la *forme* d'une référence scientifique et en fabrique qui ressemblent parfaitement à de vraies — auteurs crédibles, titres vraisemblables — mais qui n'existent pas.
    4. **Faible.** Comme le résumé, le texte est fourni ; le modèle le transforme.

    !!! success "La règle qui découle de tout ça"
        Le risque d'hallucination est **faible** quand le modèle **transforme** une information que tu fournis. Il est **élevé** quand il doit **produire** une information qu'il est censé « savoir ».

        D'où le bon usage : fournir soi-même la matière, et se méfier de tout ce que le modèle avance comme un fait — surtout les chiffres, dates, citations et références.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc D"
    - Un modèle de langue **prédit le mot suivant**, encore et encore. C'est tout.
    - Il apprend les enchaînements en **comptant** dans un grand texte — aucune grammaire n'est écrite.
    - Le **hasard** (la température) règle le curseur entre répétition et incohérence.
    - Une **hallucination** n'est pas un bug : c'est un système qui produit du plausible sans distinguer le vrai du faux.
    - Risque **faible** quand l'IA transforme ce que tu fournis, **élevé** quand elle doit produire un fait — méfie-toi des chiffres, dates, citations.

