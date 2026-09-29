---
author: Elisabeth Le Prettre (LePrettre)
title: 04a Modéliser un réseau
---

# Bloc A — Modéliser un réseau

!!! abstract "Au programme"
    Graphe, sommet, arête · voisins et degré · matrice d'adjacence · distance et effet petit monde

!!! info "Séances 1 et 2"
    Séance 1 : représenter un réseau. Séance 2 : s'y déplacer.

## <span style="color:#1565c0">Un réseau est un graphe</span>

Pour qu'une machine traite des relations, il faut les représenter. L'outil s'appelle un **graphe**.

| Terme | Ce que c'est | Dans notre réseau |
| --- | --- | --- |
| **Sommet** | un élément du réseau | un élève |
| **Arête** | une relation entre deux sommets | une amitié |
| **Degré** d'un sommet | son nombre d'arêtes | son nombre d'amis |

!!! info "Deux types de relations"
    - Une relation **symétrique** (si A est ami avec B, B est ami avec A) donne un graphe **non orienté**. C'est le cas de notre réseau d'amitié.
    - Une relation **asymétrique** (A suit B sans que B suive A) donne un graphe **orienté**, avec des flèches.

    Les plateformes utilisent les deux : « ami » est généralement symétrique, « abonné » ne l'est pas.

## <span style="color:#1565c0">Représenter le graphe en Python</span>

On n'a besoin de rien de plus que des **listes**, vues en M0.

```python
eleves = ["Camille", "Lou", "Mohamed", "Sarah", "Tom",
          "Ines", "Noah", "Lea", "Gabriel", "Jade"]

liens = [["Camille", "Lou"], ["Camille", "Mohamed"], ["Camille", "Ines"],
         ["Lou", "Sarah"], ["Mohamed", "Sarah"], ["Mohamed", "Tom"],
         ["Sarah", "Ines"], ["Tom", "Noah"], ["Ines", "Lea"],
         ["Noah", "Gabriel"], ["Lea", "Jade"], ["Gabriel", "Jade"]]
```

Chaque lien est une liste de deux prénoms. C'est ce qu'on appelle une **liste d'arêtes**.

!!! question "À toi de jouer A.1 ⭐⭐ — Les voisins"
    Écris une fonction `voisins(personne)` qui renvoie la liste des amis d'une personne.

    **Attention au piège :** un lien peut mentionner la personne en première **ou** en deuxième position.

??? success "Corrigé"
    ```python
    def voisins(personne):
        resultat = []
        for lien in liens:
            if lien[0] == personne:
                resultat.append(lien[1])
            elif lien[1] == personne:
                resultat.append(lien[0])
        return resultat
    ```

    ```text
    >>> voisins("Camille")
    ['Lou', 'Mohamed', 'Ines']
    >>> voisins("Jade")
    ['Lea', 'Gabriel']
    ```

    !!! warning "Pourquoi `elif` et non deux `if` ?"
        Avec deux `if` séparés, un lien `["Camille", "Camille"]` compterait deux fois. Le `elif` garantit qu'un lien n'ajoute **qu'un** voisin.

!!! question "À toi de jouer A.2 ⭐ — Le degré"
    Écris `degre(personne)` et affiche le degré de chacun.

??? success "Corrigé"
    ```python
    def degre(personne):
        return len(voisins(personne))


    for eleve in eleves:
        print(eleve, ":", degre(eleve), "amis")
    ```

    ```text
    Camille : 3 amis
    Lou : 2 amis
    Mohamed : 3 amis
    Sarah : 3 amis
    Tom : 2 amis
    Ines : 3 amis
    Noah : 2 amis
    Lea : 2 amis
    Gabriel : 2 amis
    Jade : 2 amis
    ```

    !!! tip "Une fonction d'une ligne, est-ce utile ?"
        Oui. `degre(x)` dit **ce qu'on cherche** ; `len(voisins(x))` dit comment on l'obtient. Un programme se lit mieux quand il nomme ses intentions.

## <span style="color:#1565c0">La matrice d'adjacence</span>

Il existe une autre représentation, plus proche de ce que manipule une machine : un tableau de 0 et de 1.

!!! example "Activité 1 — Construire la matrice"
    ```python
    def relies(a, b):
        for lien in liens:
            if (lien[0] == a and lien[1] == b) or (lien[0] == b and lien[1] == a):
                return 1
        return 0


    matrice = []
    for a in eleves:
        ligne = []
        for b in eleves:
            ligne.append(relies(a, b))
        matrice.append(ligne)

    for i in range(len(eleves)):
        print(eleves[i], matrice[i])
    ```

??? success "Résultat"
    ```text
    Camille [0, 1, 1, 0, 0, 1, 0, 0, 0, 0]
    Lou     [1, 0, 0, 1, 0, 0, 0, 0, 0, 0]
    Mohamed [1, 0, 0, 1, 1, 0, 0, 0, 0, 0]
    Sarah   [0, 1, 1, 0, 0, 1, 0, 0, 0, 0]
    Tom     [0, 0, 1, 0, 0, 0, 1, 0, 0, 0]
    Ines    [1, 0, 0, 1, 0, 0, 0, 1, 0, 0]
    Noah    [0, 0, 0, 0, 1, 0, 0, 0, 1, 0]
    Lea     [0, 0, 0, 0, 0, 1, 0, 0, 0, 1]
    Gabriel [0, 0, 0, 0, 0, 0, 1, 0, 0, 1]
    Jade    [0, 0, 0, 0, 0, 0, 0, 1, 1, 0]
    ```

    Un `1` en ligne *i*, colonne *j* signifie : *i* et *j* sont amis.

    !!! example "Trois observations à faire faire aux élèves"
        1. La **diagonale est nulle** — personne n'est son propre ami.
        2. La matrice est **symétrique** — c'est la traduction du « non orienté ».
        3. La **somme d'une ligne** donne le degré. Vérifie sur Camille : 1+1+1 = 3.

!!! info "Deux représentations, deux usages"
    | | Liste d'arêtes | Matrice d'adjacence |
    | --- | --- | --- |
    | Place occupée | proportionnelle au nombre de liens | proportionnelle au **carré** du nombre de sommets |
    | « A et B sont-ils amis ? » | il faut parcourir toute la liste | réponse immédiate |
    | Réseau creux (peu de liens) | efficace | très gaspilleur |

    Pour un réseau social réel — des milliards de personnes, mais quelques centaines d'amis chacun — la matrice serait absurde : elle contiendrait presque uniquement des zéros.

    **Le choix d'une représentation est un choix d'ingénierie**, pas un détail.

## <span style="color:#1565c0">Se déplacer : la distance</span>

!!! info "Séance 2"

La **distance** entre deux personnes est le nombre minimal d'arêtes à parcourir pour aller de l'une à l'autre. C'est le « degré de séparation ».

!!! example "Activité 2 — Les vagues"
    Pour calculer les distances depuis Camille, on procède par **vagues** :

    - vague 0 : Camille elle-même ;
    - vague 1 : ses amis directs ;
    - vague 2 : les amis de ses amis, non déjà atteints ;
    - et ainsi de suite.

    Fais-le d'abord **à la main**, sur papier, avant de regarder le code.

??? success "Corrigé — le code"
    ```python
    def distances(depart):
        atteints = [depart]
        distance = [0]
        vague = [depart]
        d = 0

        while len(vague) > 0:
            d = d + 1
            suivante = []
            for personne in vague:
                for ami in voisins(personne):
                    if ami not in atteints:
                        atteints.append(ami)
                        distance.append(d)
                        suivante.append(ami)
            vague = suivante

        return atteints, distance


    noms, dist = distances("Camille")
    for i in range(len(noms)):
        print(noms[i], ":", dist[i])
    ```

    ```text
    Camille : 0
    Lou : 1
    Mohamed : 1
    Ines : 1
    Sarah : 2
    Tom : 2
    Lea : 2
    Noah : 3
    Jade : 3
    Gabriel : 4
    ```

    !!! warning "Le rôle de `if ami not in atteints`"
        Sans ce test, le programme tournerait **indéfiniment** : il repasserait sans arrêt d'un ami à l'autre.

        C'est la boucle infinie du bloc B de M0, sous une autre forme. Ici, la condition d'arrêt n'est pas un compteur mais une **mémoire de ce qu'on a déjà visité**.

    !!! tip "Pourquoi les vagues donnent le chemin le plus court"
        Une personne est atteinte à la vague *d* : cela signifie qu'aucun chemin plus court n'existait, sinon elle aurait été atteinte plus tôt. La méthode garantit le minimum sans jamais comparer de chemins.

## <span style="color:#1565c0">L'effet petit monde</span>

!!! question "À toi de jouer A.3 ⭐⭐⭐"
    1. Calcule les distances depuis Gabriel. Quelle est la plus grande ?
    2. Quelle est la plus grande distance dans tout le réseau ?

??? success "Corrigé"
    ```python
    noms, dist = distances("Gabriel")
    for i in range(len(noms)):
        print(noms[i], ":", dist[i])
    ```

    ```text
    Gabriel : 0
    Noah : 1
    Jade : 1
    Tom : 2
    Lea : 2
    Mohamed : 3
    Ines : 3
    Camille : 4
    Sarah : 4
    Lou : 5
    ```

    La plus grande distance du réseau est **5**, entre Gabriel et Lou. On l'appelle le **diamètre** du graphe.

!!! quote "L'expérience du petit monde"
    Dans les années 1960, une expérience célèbre a demandé à des personnes de faire parvenir une lettre à un inconnu, uniquement en la transmettant à quelqu'un qu'elles connaissaient personnellement. Les lettres arrivées avaient franchi en moyenne un nombre très faible d'intermédiaires — d'où l'expression **« six degrés de séparation »**.

    Des études conduites plus tard sur de grands réseaux sociaux numériques ont trouvé des valeurs encore plus basses, autour de quatre.

!!! example "Activité 3 — Le paradoxe"
    Notre réseau compte **10 personnes** et son diamètre est de **5**. Un réseau social mondial compte des **milliards** de personnes, et sa distance moyenne tourne autour de **4**.

    Comment est-ce possible ?

??? success "Corrigé"
    Ce n'est pas la **taille** du réseau qui compte, mais sa **structure**.

    Notre graphe est presque une chaîne : Gabriel n'a que deux amis, Noah deux, Tom deux… Pour aller d'un bout à l'autre, il faut passer par tout le monde.

    Dans un réseau réel, quelques personnes ont **énormément** de connexions et servent de raccourcis entre des groupes éloignés. Il suffit de quelques-uns de ces ponts pour effondrer les distances.

    !!! tip "Ce que ça implique"
        Une information ne se propage pas de proche en proche à vitesse régulière : elle **saute** d'un groupe à l'autre dès qu'elle atteint une personne très connectée.

        C'est la clé de la viralité — le sujet du bloc D.

!!! question "À toi de jouer A.4 ⭐⭐ — Créer un pont"
    Ajoute un seul lien entre Lou et Gabriel, puis recalcule le diamètre. Que se passe-t-il ?

??? success "Corrigé"
    ```python
    liens.append(["Lou", "Gabriel"])
    noms, dist = distances("Gabriel")
    ```

    Lou passe de la distance 5 à la distance 1, et toutes les distances qui passaient par le « long chemin » s'effondrent. Le diamètre tombe à 3.

    **Une seule arête** a transformé la structure du réseau. C'est exactement ce que font les comptes très suivis.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc A"
    - Un réseau se modélise par un **graphe** : sommets, arêtes, degré.
    - Deux représentations, deux usages : **liste d'arêtes** (économe) et **matrice d'adjacence** (réponse immédiate).
    - La **distance** se calcule par vagues successives — en mémorisant ce qu'on a déjà visité.
    - Ce n'est pas la taille d'un réseau qui fait ses distances, mais sa **structure** : quelques personnes très connectées suffisent à tout rapprocher.

