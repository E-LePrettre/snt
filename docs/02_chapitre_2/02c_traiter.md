---
author: Elisabeth Le Prettre (LePrettre)
title: 02b Traiter des données
---




# Bloc B — Traiter un jeu de données

!!! abstract "Au programme"
    Découper un CSV · extraire une colonne · réutiliser les fonctions de M0 · filtrer, trier, compter · lire une réponse d'API

!!! info "Séances 2 et 3"
    Séance 2 : charger et explorer un jeu de données. Séance 3 : l'interroger pour répondre à une question.

## <span style="color:#1565c0">Le jeu de données</span>

Recopie ce bloc en tête de tous tes programmes du module :

```python
donnees = """prenom,maths,francais,ecran
Camille,12,14,180
Lou,8,11,240
Mohamed,15,13,90
Sarah,17,16,120
Tom,9,7,300
Ines,11,15,150
Noah,14,12,210
Lea,6,10,270
Gabriel,18,15,60
Jade,13,14,165"""
```

!!! note "Les triples guillemets"
    `"""..."""` permet d'écrire une chaîne sur **plusieurs lignes**. C'est le contenu exact d'un fichier CSV, collé dans le programme.

    On procède ainsi pour éviter les questions de fichiers, qui n'apprennent rien d'intéressant. Le traitement, lui, est identique.

## <span style="color:#1565c0">Découper le CSV</span>

Deux opérations suffisent, et tu connais déjà la logique depuis M0.

!!! example "Activité 1 — De la chaîne à la table"
    Teste et observe :

    ```python
    lignes = donnees.split("\n")
    print(len(lignes))
    print(lignes[0])
    print(lignes[1])
    ```

    Puis :

    ```python
    print(lignes[1].split(","))
    ```

??? success "Réponse"
    ```text
    11
    prenom,maths,francais,ecran
    Camille,12,14,180
    ['Camille', '12', '14', '180']
    ```

    `split(separateur)` **découpe une chaîne** et renvoie une **liste**.

    - `donnees.split("\n")` découpe sur les retours à la ligne → une ligne par élément.
    - `ligne.split(",")` découpe sur les virgules → une valeur par élément.

    11 lignes et non 10 : la première contient les en-têtes.

!!! danger "Tout est du texte"
    Regarde bien : `'12'` est entre guillemets. Après un `split`, **toutes les valeurs sont des chaînes de caractères**, même les nombres.

    C'est exactement le problème rencontré avec `input()` en M0. Et la solution est la même : convertir avec `int()` ou `float()`.

### <span style="color:#2e7d32">Construire la table</span>

```python
lignes = donnees.split("\n")
entetes = lignes[0].split(",")

table = []
for ligne in lignes[1:]:
    table.append(ligne.split(","))
```

```text
>>> entetes
['prenom', 'maths', 'francais', 'ecran']
>>> table[0]
['Camille', '12', '14', '180']
>>> len(table)
10
```

!!! tip "`lignes[1:]` : le slicing resurgit"
    On saute la première ligne (les en-têtes) et on garde tout le reste. C'est la notation vue en M0.

## <span style="color:#1565c0">Extraire une colonne</span>

!!! question "À toi de jouer B.1 ⭐⭐"
    Écris une fonction `colonne(table, indice)` qui renvoie la liste des valeurs d'une colonne donnée.

    ```text
    >>> colonne(table, 0)
    ['Camille', 'Lou', 'Mohamed', ...]
    ```

??? success "Corrigé"
    ```python
    def colonne(table, indice):
        resultat = []
        for ligne in table:
            resultat.append(ligne[indice])
        return resultat
    ```

    C'est le schéma de construction de liste vu en M0 : **liste vide → `append` dans la boucle → renvoyer**.

!!! question "À toi de jouer B.2 ⭐⭐ — Convertir"
    Écris une fonction `en_nombres(liste)` qui transforme une liste de chaînes en liste d'entiers.

??? success "Corrigé"
    ```python
    def en_nombres(liste):
        resultat = []
        for valeur in liste:
            resultat.append(int(valeur))
        return resultat
    ```

    On peut maintenant enchaîner les deux :

    ```python
    maths = en_nombres(colonne(table, 1))
    ecran = en_nombres(colonne(table, 3))
    print(maths)
    print(ecran)
    ```

    ```text
    [12, 8, 15, 17, 9, 11, 14, 6, 18, 13]
    [180, 240, 90, 120, 300, 150, 210, 270, 60, 165]
    ```

## <span style="color:#1565c0">Réutiliser M0 : les statistiques</span>

C'est ici que le module précédent paie. Colle tes fonctions de M0 dans ton programme — **sans les modifier** :

```python
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
```

!!! example "Activité 2 — Les premières statistiques"
    ```python
    print("Moyenne en maths :", round(moyenne(maths), 2))
    print("Meilleure note   :", maximum(maths))
    print("Écran moyen      :", round(moyenne(ecran), 1), "min/jour")
    ```

??? success "Résultat"
    ```text
    Moyenne en maths : 12.3
    Meilleure note   : 18
    Écran moyen      : 178.5 min/jour
    ```

    Presque **trois heures** d'écran par jour en moyenne.

    !!! warning "Attention à la moyenne"
        Cette moyenne cache des situations très différentes : de 60 à 300 minutes, soit du simple au quintuple. Une moyenne seule ne décrit pas une population — on y revient au bloc C.

!!! question "À toi de jouer B.3 ⭐⭐ — Le minimum"
    Tu as `maximum`. Écris `minimum(liste)` sur le même modèle, puis affiche l'écart entre le plus gros et le plus petit temps d'écran.

??? success "Corrigé"
    ```python
    def minimum(liste):
        record = liste[0]
        for valeur in liste:
            if valeur < record:
                record = valeur
        return record


    print("Écart :", maximum(ecran) - minimum(ecran), "minutes")
    ```

    ```text
    Écart : 240 minutes
    ```

    !!! tip "Le piège évité"
        On initialise avec `liste[0]`, pas avec un nombre arbitraire — c'est exactement l'erreur du **code C** débusqué dans le bloc D de M0. La même vigilance sert ici.

## <span style="color:#1565c0">Filtrer</span>

Filtrer, c'est **ne garder que les lignes** qui vérifient une condition.

!!! question "À toi de jouer B.4 ⭐⭐"
    Écris une fonction `filtrer(table, indice, seuil)` qui renvoie les lignes dont la valeur de la colonne `indice` est **supérieure ou égale** à `seuil`.

??? success "Corrigé"
    ```python
    def filtrer(table, indice, seuil):
        resultat = []
        for ligne in table:
            if int(ligne[indice]) >= seuil:
                resultat.append(ligne)
        return resultat
    ```

    ```python
    bons_en_maths = filtrer(table, 1, 12)
    print(len(bons_en_maths), "élèves ont 12 ou plus")
    print(colonne(bons_en_maths, 0))
    ```

    ```text
    6 élèves ont 12 ou plus
    ['Camille', 'Mohamed', 'Sarah', 'Noah', 'Gabriel', 'Jade']
    ```

    !!! warning "`>=` et non `>`"
        Encore le cas frontière du bloc D de M0 : avec `>`, les élèves ayant exactement 12 disparaîtraient.

        Remarque aussi que `filtrer` renvoie une **table**, pas une liste de valeurs. On peut donc lui appliquer `colonne` juste après.

## <span style="color:#1565c0">Trier</span>

!!! question "À toi de jouer B.5 ⭐⭐⭐"
    Écris `trier_par(table, indice)` qui renvoie la table triée par ordre **décroissant** sur une colonne. Interdiction d'utiliser `sorted` ou `.sort()`.

    **Indice :** tu sais trouver un maximum. Que se passe-t-il si tu le retires, puis recommences ?

??? success "Corrigé"
    C'est le **tri par sélection** : on retire le maximum, on l'ajoute au résultat, on recommence.

    ```python
    def trier_par(table, indice):
        reste = []
        for ligne in table:
            reste.append(ligne)

        resultat = []
        while len(reste) > 0:
            i_max = 0
            for i in range(len(reste)):
                if int(reste[i][indice]) > int(reste[i_max][indice]):
                    i_max = i
            resultat.append(reste[i_max])
            reste.pop(i_max)
        return resultat
    ```

    ```python
    classement = trier_par(table, 3)
    for ligne in classement:
        print(ligne[0], ":", ligne[3], "min")
    ```

    ```text
    Tom : 300 min
    Lea : 270 min
    Lou : 240 min
    Noah : 210 min
    Camille : 180 min
    ...
    ```

    !!! tip "Pourquoi on copie la table d'abord"
        `reste.pop()` **détruit** la liste au fur et à mesure. Sans la copie, on abîmerait la table d'origine et les traitements suivants seraient faux.

        C'est une règle générale : une fonction ne doit pas modifier ce qu'on lui donne, sauf si c'est explicitement son rôle.

    !!! note "Ce que ça coûte"
        Pour trier 10 lignes, ce tri fait une centaine de comparaisons. Pour un million de lignes, il en faudrait mille milliards. Les algorithmes de tri efficaces sont un grand sujet d'informatique — c'est au programme de NSI en première.

## <span style="color:#1565c0">Répondre à une question</span>

!!! question "À toi de jouer B.6 ⭐⭐⭐ — L'enquête"
    Réponds à ces trois questions **en écrivant un programme**, pas en lisant le tableau à l'œil :

    1. Combien d'élèves ont la moyenne dans les **deux** matières ?
    2. Quelle est la moyenne de temps d'écran des élèves qui ont moins de 10 en maths ? Et celle des autres ?
    3. Qui a le plus grand écart entre sa note de maths et celle de français ?

??? success "Corrigé"
    ```python
    # 1. Moyenne dans les deux matières
    compteur = 0
    for ligne in table:
        if int(ligne[1]) >= 10 and int(ligne[2]) >= 10:
            compteur = compteur + 1
    print("1 -", compteur, "élèves ont la moyenne partout")

    # 2. Comparer deux groupes
    faibles = []
    autres = []
    for ligne in table:
        if int(ligne[1]) < 10:
            faibles.append(int(ligne[3]))
        else:
            autres.append(int(ligne[3]))
    print("2 - moins de 10 en maths :", round(moyenne(faibles), 1), "min")
    print("    les autres           :", round(moyenne(autres), 1), "min")

    # 3. Le plus grand écart
    record = 0
    nom = ""
    for ligne in table:
        ecart = int(ligne[1]) - int(ligne[2])
        if ecart < 0:
            ecart = -ecart
        if ecart > record:
            record = ecart
            nom = ligne[0]
    print("3 -", nom, "avec un écart de", record, "points")
    ```

    ```text
    1 - 7 élèves ont la moyenne partout
    2 - moins de 10 en maths : 270.0 min
        les autres           : 139.3 min
    3 - Ines avec un écart de 4 points
    ```

    !!! warning "Question 3 : il y a une égalité"
        Ines (11 et 15) et Lea (6 et 10) ont **toutes deux** un écart de 4 points. Le programme n'en affiche qu'une : celle qu'il rencontre en premier, parce que la condition est `ecart > record` et non `>=`.

        Ce n'est pas un bug, mais ce n'est pas anodin : **ton programme a tranché une égalité sans te le dire**. Sur un classement, une attribution de place ou une sélection, ce silence peut avoir des conséquences réelles.

    !!! danger "Le piège de la question 2"
        Les élèves en difficulté en maths passent en moyenne **bien plus de temps** devant un écran. Beaucoup concluraient : *les écrans font baisser les notes*.

        C'est une conclusion **injustifiée**. On observe que les deux vont ensemble ; on n'a montré aucun lien de cause à effet. Peut-être qu'une troisième cause explique les deux. Peut-être que ce sont les difficultés scolaires qui poussent vers les écrans, et non l'inverse.

        **Corrélation n'est pas causalité.** On y revient au bloc C — c'est une des erreurs de raisonnement les plus répandues.

## <span style="color:#1565c0">Lire une réponse d'API</span>

Une **API** est un service auquel un programme peut poser une question. La réponse arrive presque toujours en JSON.

!!! example "Activité 3 — Décoder du JSON"
    ```python
    import json

    reponse = '{"ville": "Mont-de-Marsan", "temperature": 18.5, "humidite": 72}'

    releve = json.loads(reponse)

    print(releve["ville"])
    print(releve["temperature"], "°C")
    ```

??? success "Résultat"
    ```text
    Mont-de-Marsan
    18.5 °C
    ```

    `json.loads` transforme une **chaîne** JSON en structure Python exploitable. On accède ensuite à chaque champ par son nom, entre crochets.

    Remarque : `18.5` est arrivé directement comme un nombre, sans conversion. Le JSON, contrairement au CSV, **transporte les types**. C'est son principal avantage.

!!! question "À toi de jouer B.7 ⭐⭐"
    ```python
    reponse = '{"station": "MDM-04", "releves": [17.2, 18.5, 19.1, 18.8, 17.9]}'
    ```

    Écris un programme qui affiche le nom de la station, le nombre de relevés, et la température moyenne.

??? success "Corrigé"
    ```python
    import json

    reponse = '{"station": "MDM-04", "releves": [17.2, 18.5, 19.1, 18.8, 17.9]}'
    data = json.loads(reponse)

    print("Station :", data["station"])
    print("Relevés :", len(data["releves"]))
    print("Moyenne :", round(moyenne(data["releves"]), 2), "°C")
    ```

    ```text
    Station : MDM-04
    Relevés : 5
    Moyenne : 18.3 °C
    ```

    `moyenne()`, écrite en M0 pour des notes d'élèves, fonctionne sans une modification sur des températures venues d'une API. **C'est tout l'intérêt d'écrire des fonctions.**

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc B"
    - `split(separateur)` découpe une chaîne en liste : c'est tout ce qu'il faut pour lire un CSV.
    - Après un `split`, **tout est du texte** — il faut convertir avant de calculer.
    - **Filtrer** garde des lignes, **trier** les réordonne, **compter** répond à une question.
    - Une fonction ne doit pas abîmer ce qu'on lui donne : on copie avant de détruire.
    - `json.loads` décode une réponse d'API — et le JSON, lui, transporte les types.
    - **Corrélation n'est pas causalité** : deux colonnes qui varient ensemble ne prouvent aucun lien de cause à effet.

