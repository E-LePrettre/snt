---
author: Elisabeth Le Prettre (LePrettre)
title: 04b Qui décide
---


# Bloc B — Qui décide de ce que tu vois ?

!!! abstract "Au programme"
    Suggérer des amis · ordonner un fil d'actualité · ce qu'un algorithme optimise · le lien avec l'IA

!!! info "Séance 3"
    C'est la séance centrale du module. Tu vas écrire toi-même un algorithme de recommandation — et découvrir que « l'algorithme » n'est ni magique ni mystérieux.

!!! quote "La question du module"
    On dit souvent « c'est l'algorithme ». Mais un algorithme, tu sais ce que c'est depuis M0 : une suite d'étapes. Il n'y a rien dedans que tu ne puisses comprendre.

    Reste la vraie question, qui n'est pas technique : **qui décide de ce que l'algorithme optimise ?**

## <span style="color:#1565c0">Suggérer des amis</span>

Comment une plateforme te propose-t-elle « des personnes que tu connais peut-être » ? L'idée de base est simple : **plus vous avez d'amis en commun, plus il est probable que vous vous connaissiez.**

!!! question "À toi de jouer B.1 ⭐⭐"
    Écris `amis_communs(a, b)` qui compte le nombre d'amis partagés par deux personnes.

??? success "Corrigé"
    ```python
    def amis_communs(a, b):
        compteur = 0
        for personne in voisins(a):
            if personne in voisins(b):
                compteur = compteur + 1
        return compteur
    ```

    ```text
    >>> amis_communs("Camille", "Sarah")
    3
    >>> amis_communs("Camille", "Jade")
    0
    ```

    Camille et Sarah partagent trois amis (Lou, Mohamed, Ines) sans être amies elles-mêmes. C'est un signal fort.

!!! question "À toi de jouer B.2 ⭐⭐⭐ — L'algorithme de suggestion"
    Écris `suggestions(personne)` qui renvoie, **triée du plus au moins probable**, la liste des personnes à suggérer.

    Trois règles :

    - on ne se suggère pas soi-même ;
    - on ne suggère pas quelqu'un qui est **déjà** ami ;
    - on ne suggère que s'il y a **au moins un** ami commun.

??? success "Corrigé"
    ```python
    def suggestions(personne):
        candidats = []
        for autre in eleves:
            if autre != personne and autre not in voisins(personne):
                n = amis_communs(personne, autre)
                if n > 0:
                    candidats.append([autre, n])

        # tri par sélection, décroissant — comme en M0
        resultat = []
        while len(candidats) > 0:
            i_max = 0
            for i in range(len(candidats)):
                if candidats[i][1] > candidats[i_max][1]:
                    i_max = i
            resultat.append(candidats[i_max])
            candidats.pop(i_max)
        return resultat
    ```

    ```text
    >>> suggestions("Camille")
    [['Sarah', 3], ['Tom', 1], ['Lea', 1]]
    >>> suggestions("Jade")
    [['Ines', 1], ['Noah', 1]]
    ```

    !!! success "Ce que tu viens d'écrire"
        C'est un **véritable algorithme de recommandation**. Le principe utilisé par les grandes plateformes est le même ; ce qui change, c'est le nombre de signaux pris en compte : amis communs, mais aussi lieux, établissements, contacts du téléphone, appareils utilisés, temps passé sur un profil.

        La logique, elle, tient en dix lignes.

!!! warning "Une suggestion n'est pas neutre"
    Regarde le résultat pour Camille : Sarah arrive largement en tête. Si Camille accepte, une nouvelle arête apparaît — et le réseau se **referme** encore davantage sur ce groupe.

    Un algorithme qui recommande « qui vous ressemble » resserre les groupes existants au lieu d'ouvrir sur de nouveaux. On retrouvera cet effet au bloc D.

## <span style="color:#1565c0">Ordonner un fil d'actualité</span>

Ton fil ne peut pas tout afficher en même temps. **Quelque chose décide de l'ordre.** Voyons quoi.

```python
# [auteur, minutes depuis la publication, likes, commentaires]
posts = [["Lou", 5, 3, 0],
         ["Mohamed", 120, 240, 55],
         ["Sarah", 30, 45, 2],
         ["Tom", 600, 900, 310],
         ["Ines", 15, 12, 1]]
```

!!! example "Activité 1 — Le fil chronologique"
    Trie les publications de la plus récente à la plus ancienne.

    ```python
    def trier(liste, indice, croissant):
        reste = []
        for x in liste:
            reste.append(x)
        resultat = []
        while len(reste) > 0:
            choisi = 0
            for i in range(len(reste)):
                if croissant:
                    if reste[i][indice] < reste[choisi][indice]:
                        choisi = i
                else:
                    if reste[i][indice] > reste[choisi][indice]:
                        choisi = i
            resultat.append(reste[choisi])
            reste.pop(choisi)
        return resultat


    for post in trier(posts, 1, True):
        print(post[0], "-", post[1], "min")
    ```

??? success "Résultat"
    ```text
    Lou - 5 min
    Ines - 15 min
    Sarah - 30 min
    Mohamed - 120 min
    Tom - 600 min
    ```

    C'est le fil le plus simple : **le plus récent d'abord**. C'est ainsi que fonctionnaient les premiers réseaux sociaux.

!!! question "À toi de jouer B.3 ⭐⭐ — Le fil par engagement"
    Aucune plateforme n'utilise plus l'ordre chronologique. Elles classent par **engagement** : ce qui fait réagir.

    Définis un score : `score = likes + 3 × commentaires` (un commentaire demande plus d'effort qu'un like, il vaut donc plus). Trie les publications par score décroissant.

??? success "Corrigé"
    ```python
    def score(post):
        return post[2] + 3 * post[3]


    avec_score = []
    for post in posts:
        avec_score.append([post[0], post[1], post[2], post[3], score(post)])

    for post in trier(avec_score, 4, False):
        print(post[0], "- score", post[4], "-", post[1], "min")
    ```

    ```text
    Tom - score 1830 - 600 min
    Mohamed - score 405 - 120 min
    Sarah - score 51 - 30 min
    Ines - score 15 - 15 min
    Lou - score 3 - 5 min
    ```

!!! danger "Compare les deux fils"
    | Chronologique | Par engagement |
    | --- | --- |
    | Lou (5 min) | **Tom** (600 min) |
    | Ines | Mohamed |
    | Sarah | Sarah |
    | Mohamed | Ines |
    | **Tom** (600 min) | **Lou** (5 min) |

    **L'ordre est exactement inversé.** Les mêmes publications, les mêmes données, deux affichages opposés.

    La publication de Lou, vieille de 5 minutes, se retrouve en dernier. Celle de Tom, vieille de 10 heures, arrive en tête.

    Personne n'a triché. On a simplement changé **ce qu'on décide d'optimiser**.

## <span style="color:#1565c0">Ce qu'un algorithme optimise</span>

!!! quote "Le point à comprendre"
    Un algorithme de classement ne cherche pas à te montrer ce qui est **vrai**, ni ce qui est **important**, ni ce qui te rendrait **heureux**.

    Il cherche à maximiser une **grandeur mesurable**, choisie par ceux qui l'ont conçu. Le plus souvent : le temps que tu passes sur la plateforme.

!!! example "Activité 2 — Changer l'objectif"
    Reprends les mêmes publications et propose un score qui privilégierait :

    1. la nouveauté ;
    2. les publications de tes amis proches plutôt que des inconnus ;
    3. les publications qui font **débat** (beaucoup de commentaires, peu de likes).

??? success "Pistes de corrigé"
    1. **Nouveauté** — un score qui décroît avec le temps :

       ```python
       def score_nouveaute(post):
           return 1000 - post[1]
       ```

    2. **Proximité** — pondérer par la distance dans le graphe (bloc A) : un ami direct compte plus qu'une personne à distance 3.

    3. **Débat** — un fort rapport commentaires / likes signale la controverse :

       ```python
       def score_debat(post):
           return post[3] * 10 - post[2]
       ```

       Sur nos données, ce score met Tom en tête (310 commentaires) mais fait remonter les publications clivantes.

    !!! warning "Ce que révèle l'exercice 3"
        Un contenu qui **fait débat** génère beaucoup de réactions. Un algorithme qui maximise les réactions mettra donc spontanément en avant ce qui divise, ce qui indigne, ce qui choque.

        Ce n'est pas une décision malveillante : c'est la **conséquence mécanique** de l'objectif choisi. Personne n'a écrit « montre ce qui énerve ». On a écrit « maximise l'engagement », et l'indignation engage.

## <span style="color:#1565c0">Le lien avec l'intelligence artificielle</span>

Notre score est écrit **à la main** : `likes + 3 × commentaires`. C'est nous qui avons choisi le 3.

!!! info "Ce que font les vraies plateformes"
    Elles ne fixent pas ces coefficients à la main. Elles laissent un système les **apprendre à partir des données** : on lui montre des millions d'exemples de publications avec, pour chacune, si l'utilisateur est resté ou est parti. Le système ajuste tout seul ce qui prédit le mieux le fait de rester.

    C'est exactement le mécanisme rencontré dans le bloc D de M0 : **apprendre à partir de données**, sans qu'aucune règle explicite ait été écrite.

!!! danger "Trois conséquences directes"
    **1. Personne ne peut expliquer simplement pourquoi tu vois cette publication.** Il n'existe pas de règle écrite quelque part. Il y a des milliers de coefficients appris, ajustés en permanence.

    **2. Le système reproduit ce qu'il a vu.** Si les contenus les plus regardés dans les données d'entraînement sont d'un certain type, il en montrera davantage. C'est le **biais** du module *Les données*, appliqué au fil d'actualité.

    **3. Il optimise ce qu'on lui a demandé, pas ce qui est bon.** Un système entraîné à maximiser le temps passé maximisera le temps passé — y compris si le meilleur moyen d'y parvenir est de te montrer des contenus qui t'agacent.

!!! quote "La formule à retenir"
    Un algorithme ne veut rien. Il **optimise ce qu'on lui a demandé d'optimiser**.

    Tout le problème est donc dans la question : *qui choisit l'objectif, et dans l'intérêt de qui ?*

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. Sur quel principe repose une suggestion d'amis ?
    2. Les mêmes publications peuvent-elles produire deux fils différents ? Pourquoi ?
    3. Que signifie « optimiser l'engagement » ?
    4. Pourquoi un algorithme qui maximise les réactions met-il en avant ce qui divise ?
    5. Pourquoi est-il difficile d'expliquer pourquoi une publication précise t'est montrée ?

??? success "Réponses"
    1. Sur le nombre d'**amis en commun** : plus il est élevé, plus il est probable que deux personnes se connaissent. Les plateformes y ajoutent d'autres signaux.
    2. **Oui** — l'ordre dépend entièrement du critère choisi. Chronologique et engagement donnent ici des ordres inversés.
    3. Classer les contenus de façon à maximiser les réactions (likes, commentaires, partages, temps passé).
    4. Parce que ce qui indigne fait beaucoup réagir. L'algorithme ne vise pas la division : il vise les réactions, et la division en produit.
    5. Parce que les coefficients ne sont pas écrits à la main : ils sont **appris** à partir de millions d'exemples, et il y en a des milliers.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc B"
    - Un algorithme de recommandation tient en quelques lignes : tu viens d'en écrire un.
    - Les mêmes données, triées selon deux critères, produisent des fils **opposés**.
    - Un algorithme **optimise une grandeur mesurable** choisie par ses concepteurs — pas la vérité, pas ton intérêt.
    - Maximiser les réactions favorise mécaniquement ce qui divise.
    - Dans les vraies plateformes, les coefficients sont **appris à partir de données** : personne ne peut expliquer simplement une recommandation précise.

