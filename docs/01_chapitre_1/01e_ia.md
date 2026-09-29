---
author: Elisabeth Le Prettre (LePrettre)
title: 01d Programmer avec l'IA
---

# Bloc D — Programmer avec une intelligence artificielle

!!! info "Séances 9 et 10"
    Séance 9 : vérifier trois codes produits par une IA. Séance 10 : d'où vient ce qu'elle produit, ce que coûte une requête, les règles d'usage.

!!! abstract "Au programme"
    Ce qu'une IA générative sait faire et ne sait pas faire · vérifier un code produit par une IA · d'où vient ce qu'elle produit · ce que coûte une requête · ce qu'on doit déclarer

!!! quote "Le principe de ce bloc"
    Tu viens d'apprendre à écrire et à tester du code. Tu as donc maintenant **de quoi juger** le code que produit une intelligence artificielle.

    C'est tout l'objet de cette page : ne pas apprendre à obéir à l'outil, mais à le contrôler.

## <span style="color:#1565c0">Ce que fait une IA générative</span>

Une IA capable d'écrire du code a été **entraînée** sur des quantités gigantesques de programmes déjà écrits par des humains. À partir de cela, elle a appris à prolonger un texte de la façon la plus **vraisemblable**.

!!! info "La phrase à retenir"
    Une IA générative produit ce qui est **plausible**, pas ce qui est **vrai**.

    Un code plausible ressemble à du code correct : il a la bonne forme, les bons mots-clés, la bonne allure. Il peut pourtant donner un résultat faux.

Ce n'est pas un défaut passager qu'on corrigera dans la prochaine version : c'est la conséquence directe de la manière dont ces systèmes fonctionnent. Ils n'exécutent pas le programme, ils ne le testent pas, ils ne savent pas ce que tu voulais obtenir.

### <span style="color:#2e7d32">Ce qu'elle ne fait pas</span>

| Elle sait | Elle ne sait pas |
| --- | --- |
| produire un code qui a l'air correct | vérifier qu'il donne le bon résultat |
| répondre très vite | savoir ce que tu voulais vraiment |
| reprendre des solutions déjà vues | exécuter le programme pour le tester |
| expliquer son code de façon convaincante | garantir que son explication est juste |

!!! warning "Le piège de la confiance"
    Une explication fausse peut être formulée de façon parfaitement assurée. Le ton d'une réponse ne dit **rien** de sa justesse. C'est vrai d'une IA ; c'est vrai aussi d'un site web ou d'une vidéo.

## <span style="color:#1565c0">Activité 1 — Trois codes à vérifier</span>

!!! example "Activité 1"
    On a demandé à une IA d'écrire trois fonctions. Les trois codes ci-dessous sont ceux qu'elle a produits. **Deux au moins sont faux.**

    Pour chacun : lis-le, prédis ce qu'il renvoie, **puis exécute-le** sur les données de test. Compare avec ce que tu attendais.

### <span style="color:#2e7d32">Code A — calculer une moyenne</span>

```python
def moyenne(liste):
    somme = 0
    for i in range(len(liste) - 1):
        somme = somme + liste[i]
    return somme / len(liste)
```

**À tester avec :**

```python
notes = [12, 8, 15, 10, 9, 11, 14, 6, 18, 13]
print(moyenne(notes))
```

??? success "Corrigé — Code A"
    Il affiche **10.3**. La bonne réponse est **11.6**.

    **L'erreur :** `range(len(liste) - 1)` s'arrête **un élément trop tôt**. La dernière note (13) n'est jamais ajoutée à la somme, alors que la division se fait bien par 10.

    Le code est plausible : `len(liste) - 1` apparaît partout en programmation (c'est l'indice du dernier élément), et ici l'IA l'a placé au mauvais endroit.

    **Correction :**

    ```python
    def moyenne(liste):
        somme = 0
        for valeur in liste:
            somme = somme + valeur
        return somme / len(liste)
    ```

    !!! tip "Pourquoi c'est difficile à repérer"
        Le programme **ne plante pas**. Il renvoie un nombre crédible : 10,3 sur 20, ça ne choque personne. Sans vérification, l'erreur passe inaperçue — et c'est le cas le plus dangereux.

### <span style="color:#2e7d32">Code B — compter les élèves qui ont la moyenne</span>

```python
def nb_admis(liste):
    compteur = 0
    for note in liste:
        if note > 10:
            compteur = compteur + 1
    return compteur
```

**À tester avec la même liste `notes`.**

??? success "Corrigé — Code B"
    Il renvoie **6**. La bonne réponse est **7**.

    **L'erreur :** `note > 10` exclut les élèves ayant exactement 10. Or avoir 10, c'est avoir la moyenne. Il fallait `note >= 10`.

    ```python
    if note >= 10:
    ```

    !!! warning "Le cas frontière"
        Ce type d'erreur — `>` au lieu de `>=` — est parmi les plus fréquentes en programmation, humaine comme artificielle. Elle ne se voit **que si l'on teste précisément la valeur du seuil**.

        Retiens la méthode : pour vérifier un programme qui compare à un seuil, teste toujours avec **exactement** la valeur du seuil.

### <span style="color:#2e7d32">Code C — trouver la température la plus élevée</span>

```python
def maximum(liste):
    record = 0
    for valeur in liste:
        if valeur > record:
            record = valeur
    return record
```

**À tester avec :**

```python
temperatures = [-3, -7, -1, -5, -2]
print(maximum(temperatures))
```

??? success "Corrigé — Code C"
    Il renvoie **0**. La bonne réponse est **-1**.

    **L'erreur :** `record = 0` suppose que toutes les valeurs sont positives. Sur des températures hivernales, aucune valeur ne dépasse 0, donc le code renvoie 0 — **une valeur qui n'est même pas dans la liste**.

    **Correction :** partir du premier élément, ce qui garantit un résultat appartenant à la liste.

    ```python
    def maximum(liste):
        record = liste[0]
        for valeur in liste:
            if valeur > record:
                record = valeur
        return record
    ```

    !!! tip "Ce que révèle cette erreur"
        Le code fonctionne parfaitement sur des notes (toujours positives). Il échoue sur des températures. L'IA a produit une solution qui marche **dans le cas le plus courant** — celui qu'elle a le plus souvent rencontré à l'entraînement.

        C'est exactement ce qu'on appelle un **biais** : ce qui est fréquent dans les données d'entraînement devient la réponse par défaut, même quand il ne convient pas.

!!! success "Bilan de l'activité 1"
    Les **trois** codes étaient faux. Aucun ne plantait. Tous renvoyaient un résultat crédible.

    Ce que tu viens d'utiliser pour les débusquer, c'est uniquement ce que tu as appris dans ce module : savoir ce que fait `range`, connaître la différence entre `>` et `>=`, savoir qu'un maximum s'initialise avec le premier élément.

    **Sans ces connaissances, tu n'aurais eu aucun moyen de juger.**

## <span style="color:#1565c0">D'où vient ce qu'elle produit</span>

Une IA n'invente pas ses réponses : elle les construit à partir de ce qu'elle a vu. Ce qui est **fréquent** dans ses données d'entraînement devient sa réponse par défaut.

!!! example "Activité 2 — Compter dans un jeu de données"
    Voici un petit jeu de données : les prénoms cités dans une série d'exemples de code.

    ```python
    exemples = ["Alan", "Ada", "Grace", "Alan", "Alan", "Linus"]
    ```

    Écris un programme qui affiche, pour chaque prénom distinct, **combien de fois** il apparaît et **quel pourcentage** cela représente.

??? success "Corrigé"
    ```python
    exemples = ["Alan", "Ada", "Grace", "Alan", "Alan", "Linus"]

    def compte(liste, valeur):
        c = 0
        for x in liste:
            if x == valeur:
                c = c + 1
        return c

    for prenom in ["Alan", "Ada", "Grace", "Linus"]:
        n = compte(exemples, prenom)
        print(prenom, ":", n, "fois ->", round(n / len(exemples) * 100, 1), "%")
    ```

    ```text
    Alan : 3 fois -> 50.0 %
    Ada : 1 fois -> 16.7 %
    Grace : 1 fois -> 16.7 %
    Linus : 1 fois -> 16.7 %
    ```

    !!! quote "Ce que ça montre"
        Un système entraîné sur ce jeu de données proposerait « Alan » une fois sur deux. Non parce que c'est le meilleur choix, mais parce que c'est **le plus fréquent dans ce qu'il a vu**.

        Transpose : si les exemples de code, les images ou les textes d'entraînement représentent mal certains groupes, le système reproduira ce déséquilibre — et le renforcera.

        Ada Lovelace a écrit le premier programme de l'histoire ; Grace Hopper a conçu le premier compilateur. Elles sont pourtant beaucoup moins citées qu'Alan Turing dans les exemples de cours. Un modèle entraîné là-dessus héritera de ce déséquilibre.

!!! info "Une définition utilisable"
    Un **biais**, ce n'est pas une intention malveillante. C'est un déséquilibre présent dans les données, que le système reproduit et amplifie sans le savoir.

## <span style="color:#1565c0">Ce que coûte une requête</span>

Une IA générative ne tourne pas sur ton ordinateur : elle tourne dans des **centres de données**, des bâtiments remplis de machines qui consomment de l'électricité et qu'il faut refroidir.

!!! example "Activité 3 — Estimer une consommation"
    On estime qu'une requête à un modèle génératif consomme de l'ordre de **3 Wh** (wattheures).

    1. Écris une fonction `energie(nb_requetes)` qui renvoie la consommation en **kWh** (1 kWh = 1000 Wh).
    2. Une classe de 30 élèves fait 20 requêtes chacun pendant une séance. Quelle consommation ?
    3. Combien d'heures d'éclairage d'une ampoule de 10 W cela représente-t-il ?

??? success "Corrigé"
    ```python
    def energie(nb_requetes):
        return round(nb_requetes * 3 / 1000, 2)


    def heures_ampoule(kwh, watts):
        return round(kwh * 1000 / watts, 1)
    ```

    ```text
    >>> energie(30 * 20)
    1.8
    >>> heures_ampoule(1.8, 10)
    180.0
    ```

    Une séance de classe représente environ **1,8 kWh**, soit l'équivalent de **180 heures** d'une ampoule de 10 W — près de huit jours d'éclairage continu.

    !!! warning "Prudence avec ce chiffre"
        L'estimation de 3 Wh est un **ordre de grandeur**, pas une mesure. La consommation réelle dépend du modèle utilisé, de la longueur de la réponse, du centre de données et du mix électrique du pays.

        Les entreprises publient rarement ces données. Savoir **d'où vient un chiffre** — et dire quand on ne le sait pas — fait partie de l'esprit critique attendu.

    !!! note "À mettre en regard"
        Ce n'est ni négligeable ni catastrophique en soi : c'est un **coût réel**, à mettre en balance avec l'usage. La bonne question n'est pas « faut-il l'interdire ? » mais « cette requête valait-elle ce coût ? ».

## <span style="color:#1565c0">Bien utiliser : quatre règles</span>

!!! success "Les règles de l'usage éclairé"
    **1. Comprendre avant d'utiliser.**
    Si tu ne peux pas expliquer ligne à ligne le code que tu rends, tu ne peux pas le rendre. Ce n'est pas une question de règlement, c'est une question de compétence : le jour où il faudra le corriger, tu seras bloqué.

    **2. Tester systématiquement.**
    Un code non testé n'est pas un code qui marche : c'est un code dont on ne sait rien. Teste avec des données dont tu connais déjà le résultat, et teste les **cas limites** (liste vide, valeur du seuil, nombres négatifs).

    **3. Déclarer ce que tu as fait produire.**
    Quand tu rends un travail, indique ce que tu as écrit toi-même et ce que tu as fait générer. Ce n'est pas un aveu, c'est de l'honnêteté intellectuelle — la même que pour citer une source.

    **4. Se demander si la requête valait le coup.**
    Chaque requête a un coût énergétique et matériel. Demander à une IA d'écrire `print("Bonjour")` n'a aucun sens.

!!! quote "Ce que dit la loi et ce que dit l'usage"
    Utiliser une IA n'est pas interdit. Faire passer pour sien un travail qu'on n'a pas fait, en revanche, relève de la **fraude** — dans un examen comme dans la vie professionnelle.

    La différence tient entièrement à la **déclaration**. Un professionnel qui utilise un outil le dit ; c'est ce qui permet à ses collègues de vérifier.

## <span style="color:#1565c0">Où tourne tout cela ?</span>

!!! info "Une question à poser dès maintenant"
    Les modèles les plus utilisés appartiennent à un petit nombre d'entreprises, et tournent sur des serveurs situés le plus souvent hors d'Europe.

    Cela soulève trois questions, qu'on reprendra en détail dans le module *Intelligence artificielle* :

    - **Où vont les données** que tu saisis dans une requête ? Qui peut les lire ? Sont-elles conservées ?
    - **Que se passe-t-il** si l'entreprise ferme le service, change ses tarifs ou modifie son modèle ?
    - **Qui décide** de ce que le modèle accepte ou refuse de produire ?

    C'est ce qu'on appelle la question de la **souveraineté numérique** : la capacité d'un pays, d'une administration ou d'une école à maîtriser les outils dont elle dépend.

!!! danger "Une règle immédiate"
    Ne saisis jamais dans une requête des informations personnelles — les tiennes ou celles d'autrui : nom complet, adresse, numéro de téléphone, coordonnées, situation privée.

    Une fois envoyées, tu n'en as plus le contrôle.

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. Pourquoi dit-on qu'une IA générative produit du « plausible » ?
    2. Le code C fonctionnait sur des notes mais échouait sur des températures. Comment appelle-t-on ce phénomène ?
    3. Quels deux cas faut-il toujours tester dans un programme qui compare à un seuil ?
    4. Que faut-il faire avant de rendre un code qu'on n'a pas écrit soi-même ?
    5. Cite deux raisons pour lesquelles il ne faut pas saisir de données personnelles dans une requête.

??? success "Réponses"
    1. Parce qu'elle a appris à prolonger un texte de la façon la plus **vraisemblable** au vu de ses données d'entraînement — pas à vérifier que le résultat est correct. Elle n'exécute ni ne teste le programme.
    2. Un **biais** : ce qui est fréquent dans les données d'entraînement (des nombres positifs) devient la réponse par défaut, même quand il ne convient pas.
    3. La valeur **exacte du seuil**, et les valeurs juste au-dessus et juste en dessous.
    4. Le **comprendre** ligne à ligne, le **tester** (y compris sur les cas limites), et **déclarer** qu'il a été généré.
    5. On ne maîtrise plus où elles vont ni qui les lit ; elles peuvent être conservées et servir à entraîner de futurs modèles ; les serveurs se trouvent souvent hors d'Europe, sous une autre juridiction.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel de ce bloc"
    - Une IA générative produit du **plausible**, pas du vrai — elle n'exécute ni ne teste ce qu'elle écrit.
    - Un code faux **ne plante pas forcément** : il peut renvoyer un résultat crédible. Seul le **test** permet de trancher.
    - Ce qui est **fréquent** dans les données d'entraînement devient la réponse par défaut : c'est le mécanisme du **biais**.
    - Chaque requête a un **coût énergétique** réel.
    - Utiliser, oui — mais **comprendre**, **tester**, **déclarer**, et ne jamais y mettre de données personnelles.

!!! quote "Le mot de la fin"
    L'objectif de ce bloc n'est pas de te dissuader d'utiliser ces outils : c'est de faire en sorte que ce soit **toi** qui les utilises, et non l'inverse.

    Tu as pu juger les trois codes de l'activité 1 uniquement parce que tu avais appris à programmer. C'est la seule chose qui te rend libre face à l'outil.
