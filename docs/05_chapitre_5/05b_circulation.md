---
author: Elisabeth Le Prettre (LePrettre)
title: 05a Circulation
---

# Bloc A — Comment circule l'information

!!! abstract "Au programme"
    Client et serveur · adresses IP · découpage en paquets · routage et plus court chemin · résilience

!!! info "Séance 1"
    Le voyage complet d'un message, de ton appareil jusqu'à sa destination.

## <span style="color:#1565c0">Client et serveur</span>

Quand tu consultes une page, deux machines dialoguent :

- le **client** — ton appareil — envoie une **requête** : « donne-moi cette page » ;
- le **serveur** — une machine allumée en permanence quelque part — renvoie une **réponse**.

!!! info "Ce qui définit un serveur"
    Ce n'est pas sa puissance, c'est son **rôle** : il attend des requêtes et y répond. Un ordinateur ordinaire peut être un serveur ; un téléphone aussi.

    Et une machine peut être les deux à la fois : un serveur qui va chercher une information ailleurs devient client à son tour.

!!! quote "La première réponse à la question suspendue"
    Tes publications ne sont pas « dans ton téléphone ». Elles sont sur le **disque d'un serveur**, dans un bâtiment, dans un pays. Ton téléphone n'en affiche qu'une copie, redemandée à chaque consultation.

## <span style="color:#1565c0">Les adresses IP</span>

Pour qu'un message arrive, il faut une adresse. Sur Internet, c'est l'**adresse IP**.

Une adresse IPv4 s'écrit avec **quatre nombres de 0 à 255**, séparés par des points :

```text
192.168.1.1
```

!!! question "À toi de jouer A.1 ⭐⭐"
    Écris `ip_valide(adresse)` qui renvoie `True` si l'adresse respecte les règles :

    - exactement **quatre** parties séparées par des points ;
    - chaque partie contient **uniquement des chiffres** ;
    - chaque partie vaut **au plus 255**.

    Teste avec `192.168.1.1`, `8.8.8.8`, `300.1.1.1`, `192.168.1`, `1.2.3.4.5`, `a.b.c.d`.

??? success "Corrigé"
    ```python
    def ip_valide(adresse):
        morceaux = adresse.split(".")
        if len(morceaux) != 4:
            return False
        for morceau in morceaux:
            if morceau == "":
                return False
            for caractere in morceau:
                if caractere not in "0123456789":
                    return False
            if int(morceau) > 255:
                return False
        return True
    ```

    ```text
    192.168.1.1  True
    8.8.8.8      True
    300.1.1.1    False    dépasse 255
    192.168.1    False    trois parties seulement
    1.2.3.4.5    False    cinq parties
    a.b.c.d      False    pas des chiffres
    ```

    !!! warning "Le cas limite qu'on oublie"
        Le test `if morceau == ""` traite l'adresse `192..1.1` — quatre parties, mais l'une est vide. Sans lui, `int("")` provoque une erreur et le programme plante au lieu de renvoyer `False`.

        Vérifier ses cas limites : la même exigence qu'en M0 et dans tous les modules depuis.

!!! question "À toi de jouer A.2 ⭐⭐ — Combien d'adresses ?"
    Chaque partie vaut de 0 à 255, soit **256 valeurs**. Combien d'adresses IPv4 existent au total ? Compare à la population mondiale.

??? success "Corrigé"
    ```python
    print("IPv4 :", 256 ** 4)
    ```

    ```text
    IPv4 : 4294967296
    ```

    Environ **4,3 milliards** — pour plus de 8 milliards d'humains, et bien davantage d'appareils connectés : téléphones, ordinateurs, objets connectés, serveurs.

    !!! danger "Elles sont épuisées"
        Les adresses IPv4 disponibles ont été entièrement attribuées. D'où le déploiement d'**IPv6**, qui utilise 128 bits :

        ```python
        print(2 ** 128)
        print(2 ** 128 // 8000000000, "par habitant")
        ```

        ```text
        340282366920938463463374607431768211456
        42535295865117307932921825928 par habitant
        ```

        Soit environ **42 milliards de milliards de milliards** d'adresses par personne. Le problème ne se reposera pas.

## <span style="color:#1565c0">Les paquets</span>

Un message ne voyage pas d'un seul bloc. Il est **découpé en paquets**, envoyés séparément.

!!! question "À toi de jouer A.3 ⭐⭐"
    Écris `en_paquets(message, taille)` qui découpe un message en morceaux de longueur donnée, chacun accompagné de son **numéro d'ordre**.

??? success "Corrigé"
    ```python
    def en_paquets(message, taille):
        paquets = []
        numero = 0
        i = 0
        while i < len(message):
            paquets.append([numero, message[i:i + taille]])
            numero = numero + 1
            i = i + taille
        return paquets


    message = "Bonjour, voici un message assez long a transmettre sur le reseau."
    for paquet in en_paquets(message, 12):
        print(paquet)
    ```

    ```text
    [0, 'Bonjour, voi']
    [1, 'ci un messag']
    [2, 'e assez long']
    [3, ' a transmett']
    [4, 're sur le re']
    [5, 'seau.']
    ```

    Le slicing `message[i:i + taille]` vient de M0. Le dernier paquet est plus court : c'est normal, le message ne tombe pas juste.

!!! example "Activité 1 — L'arrivée dans le désordre"
    Chaque paquet voyage **indépendamment** et peut emprunter une route différente. Ils arrivent donc dans n'importe quel ordre.

    ```python
    paquets = en_paquets(message, 12)
    desordre = [paquets[3], paquets[0], paquets[5],
                paquets[1], paquets[4], paquets[2]]

    print("Ordre d'arrivée :", [p[0] for p in desordre])
    ```

    Écris `reassembler(paquets)` qui reconstitue le message d'origine.

??? success "Corrigé"
    ```python
    def reassembler(paquets):
        resultat = ""
        for numero in range(len(paquets)):
            for paquet in paquets:
                if paquet[0] == numero:
                    resultat = resultat + paquet[1]
        return resultat


    print(reassembler(desordre))
    print(reassembler(desordre) == message)
    ```

    ```text
    Bonjour, voici un message assez long a transmettre sur le reseau.
    True
    ```

    !!! success "Le rôle du numéro"
        C'est lui qui rend le désordre sans conséquence. Sans numérotation, un message découpé serait irrécupérable dès qu'un paquet doublerait un autre.

        **C'est une des idées fondatrices d'Internet** : on ne cherche pas à garantir que tout arrive dans l'ordre. On accepte le désordre, et on remet en ordre à l'arrivée.

!!! question "À toi de jouer A.4 ⭐⭐ — Le paquet perdu"
    Un paquet peut se perdre. Écris `manquants(paquets, total)` qui renvoie la liste des numéros absents.

??? success "Corrigé"
    ```python
    def manquants(paquets, total):
        absents = []
        for numero in range(total):
            trouve = False
            for paquet in paquets:
                if paquet[0] == numero:
                    trouve = True
            if not trouve:
                absents.append(numero)
        return absents
    ```

    ```text
    >>> incomplet = [paquets[0], paquets[1], paquets[3], paquets[4], paquets[5]]
    >>> manquants(incomplet, 6)
    [2]
    ```

    !!! tip "Ce qui se passe ensuite"
        Le destinataire constate le manque et **redemande** le paquet 2. Il n'a pas besoin de redemander tout le message.

        C'est pour cette raison qu'un téléchargement interrompu peut reprendre là où il s'était arrêté.

## <span style="color:#1565c0">Le routage</span>

Comment un paquet trouve-t-il son chemin ? Il passe de **routeur** en routeur, chacun le transmettant vers un voisin qui rapproche de la destination.

```python
routeurs = ["A", "B", "C", "D", "E", "F", "G"]

cables = [["A","B"], ["A","C"], ["B","D"], ["C","D"],
          ["C","E"], ["D","F"], ["E","F"], ["F","G"]]
```

!!! success "Tu as déjà écrit cet algorithme"
    Un réseau de routeurs est un **graphe** : les routeurs sont les sommets, les câbles les arêtes.

    Trouver la route la plus courte, c'est chercher le **plus court chemin** — exactement le parcours par vagues du module *Réseaux sociaux*.

!!! question "À toi de jouer A.5 ⭐⭐⭐"
    Reprends `voisins()` du module précédent, en l'adaptant aux câbles. Puis écris `chemin(depart, arrivee)` qui renvoie la **liste des routeurs traversés**.

??? success "Corrigé"
    ```python
    def voisins(routeur):
        resultat = []
        for cable in cables:
            if cable[0] == routeur:
                resultat.append(cable[1])
            elif cable[1] == routeur:
                resultat.append(cable[0])
        return resultat


    def chemin(depart, arrivee):
        if depart == arrivee:
            return [depart]
        chemins = [[depart]]
        visites = [depart]
        while len(chemins) > 0:
            suivants = []
            for ch in chemins:
                dernier = ch[len(ch) - 1]
                for v in voisins(dernier):
                    if v not in visites:
                        visites.append(v)
                        nouveau = ch + [v]
                        if v == arrivee:
                            return nouveau
                        suivants.append(nouveau)
            chemins = suivants
        return None
    ```

    ```text
    >>> chemin("A", "G")
    ['A', 'B', 'D', 'F', 'G']
    >>> chemin("B", "E")
    ['B', 'A', 'C', 'E']
    ```

    !!! tip "La différence avec le module précédent"
        Là-bas, on gardait la **distance**. Ici, on garde le **chemin entier** : chaque élément de `chemins` est une liste de routeurs, allongée à chaque vague.

        Même algorithme, information plus riche.

## <span style="color:#1565c0">La résilience</span>

!!! example "Activité 2 — Couper un câble"
    Un câble est sectionné entre B et D. Supprime-le et recalcule la route de A vers G.

    ```python
    cables.remove(["B", "D"])
    print(chemin("A", "G"))
    ```

??? success "Résultat"
    ```text
    ['A', 'C', 'D', 'F', 'G']
    ```

    Le message passe **automatiquement** par C. Personne n'est intervenu ; aucune configuration n'a été modifiée.

    !!! success "L'idée fondatrice d'Internet"
        Il n'existe **aucun centre**. Chaque routeur ne connaît que ses voisins et transmet au mieux. Si un chemin disparaît, un autre est trouvé.

        C'est précisément ce qui a été recherché dans la conception d'origine : un réseau qui continue de fonctionner même si une partie est détruite.

!!! example "Activité 3 — La limite"
    Coupe cette fois le câble entre F et G.

    ```python
    cables.remove(["F", "G"])
    print(chemin("A", "G"))
    ```

??? success "Résultat"
    ```text
    None
    ```

    **G est totalement isolé.** Aucune route n'existe plus.

    Pourquoi ? Regarde le **degré** de chaque routeur :

    ```python
    for r in routeurs:
        print(r, ":", len(voisins(r)))
    ```

    ```text
    A : 2    B : 2    C : 3    D : 3
    E : 2    F : 3    G : 1
    ```

    G n'a **qu'un seul câble**. Un unique point de défaillance suffit à le couper du monde.

    !!! danger "Ce que ça explique dans la réalité"
        La résilience d'Internet n'est pas magique : elle vient de la **redondance des chemins**. Là où la redondance manque, la coupure est totale.

        C'est pourquoi une panne de câble sous-marin peut priver toute une île, ou tout un pays, d'accès à Internet : il n'y a parfois qu'un ou deux câbles pour desservir un territoire entier.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc A"
    - Un **client** demande, un **serveur** répond. Tes publications sont sur le disque d'un serveur, pas dans ton téléphone.
    - Une **adresse IP** identifie une machine. Les adresses IPv4 sont épuisées, d'où IPv6.
    - Un message est **découpé en paquets numérotés**, qui voyagent indépendamment et sont remis en ordre à l'arrivée.
    - Un paquet perdu est **redemandé seul**, pas le message entier.
    - Le **routage** est un plus court chemin dans un graphe : le même algorithme que celui du module précédent.
    - Internet n'a **aucun centre** : c'est ce qui le rend résilient. Mais là où il n'y a qu'un seul chemin, la coupure est totale.

