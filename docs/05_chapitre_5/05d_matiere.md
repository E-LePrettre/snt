---
author: Elisabeth Le Prettre (LePrettre)
title: 05c Matière
---


# Bloc C — La matière du numérique

!!! abstract "Au programme"
    Câbles sous-marins · centres de données · consommation électrique · le coût d'une requête · fabrication et déchets

!!! info "Séance 3"
    Le « nuage » n'existe pas. Il y a des câbles, des bâtiments et de l'électricité — et c'est la réponse complète à la question suspendue du module précédent.

## <span style="color:#1565c0">Où passent réellement les données</span>

!!! quote "Le mot qui trompe"
    On parle de **nuage** pour désigner le stockage à distance. Le mot suggère quelque chose de léger, de flottant, d'immatériel.

    La réalité : des bâtiments de plusieurs milliers de mètres carrés, remplis de machines, refroidis en permanence, raccordés au réseau électrique, situés à des endroits précis et appartenant à des entreprises identifiables.

### <span style="color:#2e7d32">Les câbles sous-marins</span>

L'essentiel du trafic intercontinental ne passe **pas** par les satellites. Il passe par des **câbles de fibre optique posés au fond des océans** — quelques centimètres de diamètre, des milliers de kilomètres de long.

!!! info "Quelques ordres de grandeur"
    - Plusieurs centaines de câbles sous-marins sont en service dans le monde.
    - Ils acheminent la très grande majorité des communications intercontinentales.
    - Ils sont posés par un petit nombre de navires spécialisés, et de plus en plus financés par de grandes entreprises du numérique — et non plus seulement par des opérateurs télécoms.

!!! danger "Le lien avec le bloc A"
    Souviens-toi de G, notre routeur à un seul câble : sa coupure l'isolait totalement.

    C'est exactement la situation de certains territoires — îles, pays enclavés — desservis par un ou deux câbles seulement. Une avarie, une ancre de navire, un séisme sous-marin, et l'accès à Internet d'un pays entier peut être dégradé pendant des jours.

    La résilience d'Internet n'est pas uniforme : elle dépend de la **redondance disponible localement**.

### <span style="color:#2e7d32">Les centres de données</span>

Un **centre de données** est un bâtiment conçu pour héberger des serveurs. Trois contraintes le définissent :

| Contrainte | Pourquoi |
| --- | --- |
| **Électricité** | les serveurs fonctionnent en continu, sans interruption |
| **Refroidissement** | toute l'électricité consommée finit en chaleur, qu'il faut évacuer |
| **Connexion** | il doit être relié au réseau par plusieurs liaisons à très haut débit |

!!! tip "Pourquoi ils sont là où ils sont"
    Ces contraintes expliquent leur implantation : régions à électricité abondante et peu chère, climats froids qui réduisent le coût de refroidissement, proximité des grands nœuds du réseau.

    Ce n'est pas un hasard géographique : c'est une conséquence directe de la physique.

!!! quote "La réponse complète à la question suspendue"
    *Où sont stockées tes publications ?*

    Sur des disques, dans des baies, dans un bâtiment climatisé, dans un pays donné, exploité par une entreprise soumise au droit de ce pays.

    Cette dernière précision n'est pas un détail — c'est tout l'objet du bloc D.

## <span style="color:#1565c0">Combien ça consomme</span>

!!! question "À toi de jouer C.1 ⭐⭐"
    Écris `kwh(nombre, wh_unitaire)` qui convertit une consommation en **kilowattheures** (1 kWh = 1000 Wh), puis calcule :

    | Usage | Estimation |
    | --- | --- |
    | Une heure de streaming vidéo HD | ~110 Wh |
    | Une requête à un modèle génératif | ~3 Wh |
    | Une recherche web classique | ~0,3 Wh |

    1. Une heure de streaming.
    2. Une classe de 30 élèves faisant 20 requêtes à une IA chacun.
    3. Mille recherches web.

??? success "Corrigé"
    ```python
    def kwh(nombre, wh_unitaire):
        return round(nombre * wh_unitaire / 1000, 2)


    print("1 h de streaming HD    :", kwh(1, 110), "kWh")
    print("30 élèves × 20 requêtes:", kwh(600, 3), "kWh")
    print("1000 recherches web    :", kwh(1000, 0.3), "kWh")
    ```

    ```text
    1 h de streaming HD    : 0.11 kWh
    30 élèves × 20 requêtes: 1.8 kWh
    1000 recherches web    : 0.3 kWh
    ```

    !!! success "Le rapport qui compte"
        Une requête à un modèle génératif consomme environ **dix fois plus** qu'une recherche web classique.

        Ce n'est ni négligeable ni catastrophique. C'est un **ordre de grandeur à connaître** pour pouvoir se poser la bonne question : *cette requête valait-elle ce coût ?*

        C'était déjà la quatrième règle du bloc D de M0. Elle prend ici tout son sens, avec les bâtiments derrière.

!!! note "🔄 Capsule d'actualité — à réactualiser chaque année"
    Les valeurs de consommation (streaming, requête IA, recherche web) sont des **ordres de grandeur qui évoluent vite** : les modèles changent, les centres de données gagnent en efficacité. À vérifier en début d'année. **Le raisonnement ne change pas** : c'est le rapport entre les usages qui compte, pas le chiffre exact.

!!! danger "Prudence avec tous ces chiffres"
    Ces estimations varient énormément selon les sources : le modèle utilisé, la longueur de la réponse, le rendement du centre de données, le **mix électrique** du pays.

    Une même requête émet beaucoup moins de CO₂ dans un pays à électricité largement décarbonée que dans un pays dont l'électricité vient majoritairement du charbon.

    Les entreprises publient rarement ces données. Savoir **d'où vient un chiffre**, et dire quand on ne le sait pas, fait partie de l'esprit critique — c'était déjà le message du module *Les données*.

!!! example "Activité 1 — Situer l'ordre de grandeur"
    Les estimations disponibles situent la consommation électrique mondiale des centres de données autour de **1 à 2 %** de la consommation électrique totale, avec une croissance rapide tirée notamment par l'IA.

    1. Est-ce beaucoup ou peu ?
    2. À quoi faudrait-il comparer pour répondre sérieusement ?

??? success "Pistes de réflexion"
    1. **La question n'a pas de réponse dans l'absolu.** 1 % de la consommation mondiale, c'est énorme rapporté à un seul secteur — et modeste comparé aux transports ou au chauffage.
    2. Pour répondre sérieusement, il faudrait comparer :
       - à ce que le numérique **remplace** (déplacements évités, courrier papier, supports physiques) ;
       - à la **tendance** plutôt qu'au niveau : une part qui double tous les quelques ans ne pose pas le même problème qu'une part stable ;
       - au **service rendu** : toutes les requêtes ne se valent pas.

    !!! tip "Le réflexe méthodologique"
        Un pourcentage seul ne permet aucune conclusion. Il faut un **point de comparaison** et une **tendance**.

        C'est exactement la leçon du bloc C du module *Les données* : un chiffre sans contexte n'est pas une information.

!!! note "🔄 Capsule d'actualité"
    La part mondiale des centres de données (donnée un peu plus haut) et l'impact de fabrication des appareils sont des chiffres **en évolution rapide**. À vérifier chaque année ; ce sont exactement les valeurs qu'un chiffre de presta ou d'ONG réactualise régulièrement.

## <span style="color:#1565c0">Ce qu'on oublie : fabriquer</span>

La consommation électrique n'est qu'une partie du coût. Il y a aussi la **fabrication** des appareils.

!!! info "Trois faits à connaître"
    - Pour beaucoup d'appareils personnels — téléphones, ordinateurs portables — **la fabrication représente une part majoritaire** de l'impact environnemental total, davantage que toute leur durée d'utilisation.
    - Cette fabrication mobilise de nombreux **métaux**, dont certains sont extraits dans des conditions sociales et environnementales très difficiles.
    - Le **recyclage** de ces composants reste partiel : ils sont mélangés en très petites quantités, ce qui rend leur séparation coûteuse.

!!! success "La conséquence pratique"
    Si l'essentiel de l'impact se joue à la fabrication, alors le geste le plus efficace n'est pas d'éteindre son appareil : c'est de le **garder plus longtemps**.

    Passer de trois à six ans d'usage divise l'impact de fabrication par deux — bien plus que toutes les économies d'usage réunies.

!!! example "Activité 2 — Classer les gestes"
    Range ces actions de la plus efficace à la moins efficace pour réduire l'impact environnemental du numérique :

    - supprimer ses anciens courriels ;
    - garder son téléphone deux ans de plus ;
    - regarder les vidéos en qualité réduite plutôt qu'en très haute définition ;
    - éteindre sa box la nuit.

??? success "Corrigé"
    1. **Garder son téléphone deux ans de plus** — de très loin le plus efficace, puisque la fabrication domine l'impact.
    2. **Regarder en qualité réduite** — effet réel, la vidéo représentant l'essentiel du trafic.
    3. **Éteindre sa box la nuit** — effet modeste mais mesurable, une box consommant en continu.
    4. **Supprimer ses anciens courriels** — effet quasi nul. Un courriel stocké consomme très peu ; ce qui consomme, c'est de l'**envoyer**, surtout avec des pièces jointes.

    !!! warning "Pourquoi cet ordre surprend"
        Les gestes les plus médiatisés — nettoyer sa boîte mail — sont souvent les moins efficaces, parce qu'ils sont visibles et faciles.

        Les plus efficaces sont invisibles et engageants : garder son matériel, réparer plutôt que remplacer.

        **Se sentir vertueux et être efficace sont deux choses différentes.** C'est vrai bien au-delà du numérique.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc C"
    - Le « nuage » n'existe pas : ce sont des **câbles**, des **bâtiments** et de l'**électricité**.
    - L'essentiel du trafic intercontinental passe par des **câbles sous-marins**, pas par les satellites.
    - Là où la redondance manque, une seule coupure suffit — comme le routeur G du bloc A.
    - Une requête à un modèle génératif consomme environ **dix fois** une recherche web.
    - Tout chiffre de consommation dépend du **mix électrique** : toujours demander d'où il vient.
    - Pour un appareil personnel, **la fabrication domine l'impact** : le garder plus longtemps est le geste le plus efficace.

