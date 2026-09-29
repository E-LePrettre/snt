---
author: Elisabeth Le Prettre (LePrettre)
title: 04c L'économie
---

# Bloc C — L'économie de l'attention

!!! abstract "Au programme"
    Pourquoi c'est gratuit · calculer le revenu publicitaire · la valeur d'un profil · les mécaniques de rétention

!!! info "Séance 4"
    Une plateforme ne coûte rien à l'utilisateur, mais coûte très cher à faire tourner. Ce bloc explique d'où vient l'argent — et ce que ça change pour toi.

## <span style="color:#1565c0">La question de départ</span>

Un réseau social, c'est des milliers de serveurs, des ingénieurs, des centres de données. C'est gratuit pour toi.

!!! question "Activité 1 — Trois hypothèses"
    Avant de lire la suite, propose trois façons dont une plateforme gratuite peut gagner de l'argent.

??? success "Corrigé"
    Les trois principales :

    1. **La publicité** — de loin la première source. Des annonceurs paient pour être affichés.
    2. **Les abonnements payants** — une minorité d'utilisateurs paie pour des fonctions supplémentaires.
    3. **La vente de services** aux entreprises : outils de statistiques, mise en avant de contenus, accès aux données agrégées.

    La publicité domine largement. Or une publicité ne rapporte que si quelqu'un la voit.

    !!! quote "La formule"
        Si le service est gratuit, ce n'est pas toi le client : c'est ton **attention** qui est le produit vendu.

        Formule un peu brutale, mais utile. Elle rappelle qu'entre toi et la plateforme, l'intérêt commun n'est pas garanti.

## <span style="color:#1565c0">Combien vaut une minute d'attention ?</span>

Faisons le calcul avec les données du module *Les données* : **178 minutes d'écran par jour** en moyenne.

!!! question "À toi de jouer C.1 ⭐⭐"
    On suppose qu'une plateforme affiche **une publicité toutes les deux minutes** (soit 0,5 par minute), et que mille affichages rapportent **8 €** aux annonceurs.

    Écris une fonction `revenu(minutes)` qui calcule ce que rapporte un utilisateur par jour, puis calcule :

    1. le revenu par utilisateur et par jour ;
    2. le revenu par utilisateur et par an ;
    3. le revenu annuel pour **un million** d'utilisateurs.

??? success "Corrigé"
    ```python
    def revenu(minutes):
        pubs = minutes * 0.5
        return pubs * 8 / 1000


    par_jour = revenu(178)
    par_an = par_jour * 365

    print("Par jour et par utilisateur :", round(par_jour, 2), "€")
    print("Par an et par utilisateur   :", round(par_an, 2), "€")
    print("Pour 1 million d'utilisateurs :", round(par_an * 1000000 / 1000000, 1), "M€")
    ```

    ```text
    Par jour et par utilisateur : 0.71 €
    Par an et par utilisateur   : 259.15 €
    Pour 1 million d'utilisateurs : 259.1 M€
    ```

    !!! success "Le renversement de perspective"
        Soixante-et-onze **centimes** par jour : c'est dérisoire. Deux cent cinquante-neuf **millions d'euros** par an pour un million d'utilisateurs : ça ne l'est plus du tout.

        Chaque utilisateur individuel ne vaut presque rien. C'est le **nombre** qui fait la valeur — et c'est pourquoi la croissance est l'obsession de ces entreprises.

!!! question "À toi de jouer C.2 ⭐⭐ — L'effet d'une minute"
    Combien rapporterait, pour un million d'utilisateurs et sur une année, le fait de gagner **une seule minute** d'attention quotidienne par personne ?

??? success "Corrigé"
    ```python
    gain = revenu(1) * 365 * 1000000
    print(round(gain / 1000000, 2), "M€ par an")
    ```

    ```text
    1.46 M€ par an
    ```

    !!! danger "Ce que ça explique"
        Une minute de plus par jour et par utilisateur vaut environ **un million et demi d'euros par an**.

        C'est pourquoi tant d'efforts d'ingénierie portent sur la **rétention** : garder l'utilisateur quelques secondes de plus. Ce ne sont pas des détails d'interface, ce sont des décisions économiques.

## <span style="color:#1565c0">Les mécaniques de rétention</span>

Voici les procédés les plus courants. Aucun n'est illégal ; tous sont conçus pour prolonger le temps passé.

| Mécanique | Comment ça marche |
| --- | --- |
| **Défilement infini** | Aucune fin de page — donc aucun moment naturel pour s'arrêter |
| **Lecture automatique** | La vidéo suivante démarre seule ; il faut agir pour partir, pas pour rester |
| **Notifications** | Un rappel régulier qui ramène vers l'application |
| **Récompense imprévisible** | On ne sait jamais si le prochain contenu sera intéressant — c'est l'imprévisibilité qui retient |
| **Séries et compteurs** | Un décompte de jours consécutifs qu'on ne veut pas « perdre » |
| **Signaux sociaux** | « Vu à 14 h 03 », « en train d'écrire… » : une pression à répondre vite |

!!! example "Activité 2 — L'inventaire"
    Choisis une application que tu utilises. Combien de ces six mécaniques y trouves-tu ? Note pour chacune un exemple précis.

!!! tip "Une distinction utile"
    Toutes ces mécaniques ne se valent pas.

    - Certaines rendent réellement service : la lecture automatique est confortable quand on veut enchaîner.
    - D'autres n'ont **aucun bénéfice** pour l'utilisateur et ne servent qu'à retenir : les compteurs de séries en sont l'exemple le plus net.

    La question à se poser : *cette fonction m'aide-t-elle à faire ce que je voulais faire, ou m'empêche-t-elle de partir quand je l'avais décidé ?*

## <span style="color:#1565c0">La publicité ciblée</span>

Une publicité vaut plus cher si elle atteint la bonne personne. D'où la valeur des **données personnelles**, étudiées au module précédent.

!!! example "Activité 3 — Reconstituer un profil"
    Voici ce qu'une plateforme peut déduire sans jamais te poser de question.

    | Ce qu'elle observe | Ce qu'elle en déduit |
    | --- | --- |
    | Heures de connexion | Rythme de vie, horaires scolaires ou de travail |
    | Temps passé sur chaque publication | Centres d'intérêt réels — pas ceux que tu déclares |
    | Comptes suivis | Goûts, opinions, milieu social |
    | Vitesse de défilement | Niveau d'attention, moments de fatigue |
    | Modèle d'appareil | Niveau de revenu estimé |
    | Contacts et amis communs | Entourage, établissement, ville |

    **Question :** aucune de ces informations n'a été demandée. Sont-elles pour autant des **données personnelles** au sens du module précédent ?

??? success "Corrigé"
    **Oui, sans ambiguïté.** La définition vue au module *Les données* ne porte pas sur la manière dont l'information a été obtenue, mais sur le fait qu'elle se rapporte à une personne **identifiée ou identifiable**.

    Le rapprochement de ces observations permet même de déduire des informations que l'utilisateur n'a jamais fournies : des opinions, une situation familiale, un état de santé.

    !!! danger "Le cas des données sensibles"
        Certaines catégories — opinions politiques, convictions religieuses, santé, orientation sexuelle — sont dites **sensibles** et bénéficient d'une protection renforcée par le RGPD.

        Or ce sont précisément celles qu'un profil de navigation permet souvent d'**inférer**, sans jamais qu'elles aient été déclarées. C'est un des points les plus discutés du droit du numérique.

!!! quote "L'argument à connaître, et sa limite"
    Les plateformes répondent qu'elles ne **vendent** pas les données : elles vendent aux annonceurs la possibilité d'atteindre certains profils, en gardant les données chez elles.

    C'est exact techniquement. Mais cela ne change rien à l'essentiel : les données sont bien collectées, conservées et exploitées. Ce qui est vendu, c'est le **résultat** de leur exploitation.

## <span style="color:#1565c0">Ce qu'on peut faire</span>

!!! success "Reprendre la main — quelques leviers réels"
    - **Couper les notifications** non essentielles. C'est le levier le plus efficace, et le plus simple.
    - **Consulter les paramètres de confidentialité** : la plupart des collectes optionnelles peuvent être désactivées, et presque personne ne le fait.
    - **Utiliser le droit d'accès** vu au module précédent : demander à une plateforme les données qu'elle détient sur soi est instructif.
    - **Repérer les mécaniques** plutôt que culpabiliser. Ces dispositifs sont conçus par des équipes entières ; ne pas y résister n'a rien à voir avec un manque de volonté.

!!! quote "Ce que ce bloc ne dit pas"
    Ce module ne te dit pas d'arrêter les réseaux sociaux. Ils permettent de rester en contact, de s'informer, de créer, de s'organiser.

    Il te donne de quoi comprendre **comment ils sont construits, et pourquoi**. C'est ce qui permet de décider par toi-même — au lieu que ce soit décidé pour toi.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc C"
    - Une plateforme gratuite se finance par la **publicité** : ton attention est ce qui est vendu.
    - Un utilisateur vaut quelques centimes par jour ; c'est le **nombre** qui fait la valeur.
    - Une minute d'attention quotidienne supplémentaire vaut des **millions** par an — d'où l'ingénierie de la rétention.
    - Une publicité **ciblée** vaut plus cher : c'est ce qui donne leur valeur aux données personnelles.
    - Un profil publicitaire se construit par **observation**, sans qu'aucune question ne soit posée.

