---
author: Elisabeth Le Prettre (LePrettre)
title: 03b Capteur et fichier
---

# Bloc B — De la lumière au fichier

!!! abstract "Au programme"
    Le capteur · le poids d'une image · compression avec et sans perte · les métadonnées EXIF

!!! info "Séance 2"
    Comment la lumière devient un fichier — et ce que ce fichier contient en plus de l'image.

## <span style="color:#1565c0">Le capteur</span>

Un appareil photo numérique ne « voit » rien. Derrière son objectif se trouve un **capteur** : une plaque couverte de millions de cellules sensibles à la lumière, appelées **photosites**.

!!! info "La chaîne complète"
    1. La lumière traverse l'objectif et frappe le capteur.
    2. Chaque **photosite** accumule une charge électrique proportionnelle à la quantité de lumière reçue.
    3. Un circuit convertit cette charge en **nombre**.
    4. On obtient une grille de nombres — c'est-à-dire exactement le tableau du bloc A.

!!! warning "Un photosite ne voit qu'une seule couleur"
    Chaque photosite est recouvert d'un filtre coloré : rouge, vert ou bleu. Il ne mesure donc **qu'une** des trois composantes.

    Les deux autres sont **calculées** à partir des photosites voisins. Une photo de 12 millions de pixels ne comporte pas 36 millions de mesures : elle comporte 12 millions de mesures et 24 millions de valeurs **estimées**.

    !!! quote "Un point qui vaut d'être souligné"
        Dès la prise de vue, une photographie numérique contient déjà des valeurs qui n'ont pas été mesurées, mais **reconstituées par calcul**.

        Ce n'est pas une falsification — c'est le fonctionnement normal de tout appareil. Mais cela affaiblit l'idée qu'une photo serait un enregistrement brut du réel. Retiens-le : le bloc D y reviendra.

!!! example "Activité 1 — Les filtres verts sont deux fois plus nombreux"
    Sur la plupart des capteurs, la disposition des filtres est : **1 rouge, 2 verts, 1 bleu** pour quatre photosites.

    Pourquoi le vert est-il privilégié ?

??? success "Réponse"
    Parce que l'œil humain y est le plus sensible — c'est exactement ce que montraient les coefficients de la conversion en gris du bloc A : `0,587` pour le vert, contre `0,299` pour le rouge et `0,114` pour le bleu.

    En mesurant deux fois plus de vert, on obtient une image dont **la netteté perçue** est meilleure, sans augmenter le nombre de photosites.

    Là encore : un choix technique dicté par une caractéristique biologique.

## <span style="color:#1565c0">Combien pèse une image ?</span>

!!! question "À toi de jouer B.1 ⭐⭐"
    Une photo fait 4032 × 3024 pixels, chaque pixel codé sur 3 octets (un par composante).

    Écris `poids(largeur, hauteur)` qui renvoie le poids **en mégaoctets** (1 Mo = 1024 × 1024 octets).

??? success "Corrigé"
    ```python
    def poids(largeur, hauteur):
        octets = largeur * hauteur * 3
        return round(octets / 1024 / 1024, 1)


    print(poids(4032, 3024), "Mo")
    ```

    ```text
    34.9 Mo
    ```

    !!! note "Tu as déjà fait ce calcul"
        C'était l'exercice du poids d'une photo, en M0. Tu peux vérifier : la fonction écrite alors donne le même résultat.

!!! example "Activité 2 — Le problème de la vidéo"
    Une vidéo affiche **25 images par seconde**. Calcule le poids d'**une minute** de vidéo non compressée, en gigaoctets.

??? success "Corrigé"
    ```python
    def poids_octets(largeur, hauteur):
        return largeur * hauteur * 3


    une_minute = poids_octets(4032, 3024) * 25 * 60
    print(round(une_minute / 1024 / 1024 / 1024, 1), "Go")
    ```

    ```text
    51.1 Go
    ```

    !!! danger "Cinquante gigaoctets pour une minute"
        Une vidéo de deux heures pèserait plus de **6 téraoctets**. Aucun réseau ne pourrait la transporter, aucun téléphone ne pourrait la stocker.

        Sans compression, la photographie numérique serait un usage marginal et la vidéo en ligne n'existerait tout simplement pas.

## <span style="color:#1565c0">La compression</span>

Compresser, c'est **réduire le nombre d'octets** nécessaires pour représenter la même image — ou une image suffisamment ressemblante.

!!! info "Deux familles"
    | | Sans perte | Avec perte |
    | --- | --- | --- |
    | Principe | supprimer les **redondances** | supprimer ce que l'œil ne voit pas |
    | L'image d'origine est-elle récupérable ? | **oui, à l'identique** | non, jamais |
    | Gain typique | 2 à 3 fois | 10 à 20 fois |
    | Formats | PNG | JPEG |

!!! example "Activité 3 — Compresser sans perte, à la main"
    Regarde la première ligne de notre image :

    ```text
    9,9,2,2,2,2,9,9
    ```

    Comment l'écrire plus court **sans rien perdre** ?

??? success "Corrigé"
    En comptant les répétitions au lieu de les écrire :

    ```text
    2×9, 4×2, 2×9
    ```

    Huit valeurs deviennent trois couples. C'est le principe du **codage par plages** (*run-length encoding*), l'une des techniques de compression sans perte les plus anciennes.

    !!! tip "Quand ça ne marche pas"
        Sur une image de bruit aléatoire, sans aucune répétition, ce codage produirait un fichier **plus gros** que l'original.

        Aucune méthode ne compresse tout : la compression exploite la **régularité**. Une image sans régularité est incompressible.

!!! question "À toi de jouer B.2 ⭐⭐⭐"
    Écris `compresser(ligne)` qui prend une liste de pixels et renvoie une liste de couples `[nombre, valeur]`.

??? success "Corrigé"
    ```python
    def compresser(ligne):
        resultat = []
        valeur = ligne[0]
        compteur = 1
        for i in range(1, len(ligne)):
            if ligne[i] == valeur:
                compteur = compteur + 1
            else:
                resultat.append([compteur, valeur])
                valeur = ligne[i]
                compteur = 1
        resultat.append([compteur, valeur])
        return resultat
    ```

    ```text
    >>> compresser([9,9,2,2,2,2,9,9])
    [[2, 9], [4, 2], [2, 9]]
    >>> compresser([2,7,0,0,0,0,7,2])
    [[1, 2], [1, 7], [4, 0], [1, 7], [1, 2]]
    ```

    !!! warning "Le dernier `append` en dehors de la boucle"
        Sans lui, la **dernière** plage n'est jamais enregistrée : la boucle se termine avant d'avoir rencontré un changement.

        C'est un cas limite classique — du même genre que ceux du bloc D de M0.

!!! danger "La compression avec perte est irréversible"
    Une image enregistrée en JPEG a **définitivement perdu** de l'information. Rouvrir et réenregistrer plusieurs fois dégrade l'image un peu plus à chaque fois.

    C'est pourquoi une image qui a beaucoup circulé — partagée, capturée, repartagée — finit floue et pleine d'artefacts. Chaque passage a coûté quelque chose.

## <span style="color:#1565c0">Les métadonnées</span>

Un fichier photo ne contient pas que des pixels. Il transporte aussi des **métadonnées** — des informations *sur* l'image — dans un format appelé **EXIF**.

!!! example "Activité 4 — Ce qu'on trouve dans un fichier photo"
    ```python
    import json

    exif = """{
      "appareil": "Modèle X-200",
      "date": "2026-07-23 14:32:07",
      "ouverture": "f/1.8",
      "iso": 200,
      "latitude": 43.8914,
      "longitude": -0.4998,
      "logiciel": "Retouche Pro 4.1"
    }"""

    infos = json.loads(exif)
    for cle in infos:
        print(cle, ":", infos[cle])
    ```

    Parmi ces champs, lesquels poseraient un problème si la photo était publiée en ligne ?

??? success "Corrigé"
    Trois champs sont sensibles :

    - **latitude et longitude** — l'endroit exact où la photo a été prise. Sur une photo prise chez soi, c'est l'adresse du domicile.
    - **la date et l'heure précises** — combinées avec le lieu, elles permettent de reconstituer des habitudes : où quelqu'un se trouve, à quelle heure, quels jours.
    - **le modèle d'appareil** — il permet de relier entre elles des photos publiées sous des identités différentes.

    Le champ `logiciel` est également instructif : il indique que l'image a été **retouchée**.

    !!! quote "Le lien avec le module précédent"
        Reprends la définition d'une **donnée personnelle** : toute information se rapportant à une personne identifiée ou **identifiable**.

        Des coordonnées GPS associées à une date ne contiennent aucun nom. Elles n'en sont pas moins des données personnelles — elles permettent d'isoler une personne, ce qui suffit.

!!! success "Ce qu'on peut faire"
    - La plupart des systèmes permettent de **désactiver la géolocalisation** des photos dans les réglages de l'appareil photo.
    - Certains outils suppriment les métadonnées avant partage.
    - Beaucoup de réseaux sociaux les retirent automatiquement à la publication — mais **pas tous**, et pas pour un fichier envoyé par messagerie ou par courriel.

!!! warning "Le cas le plus fréquent"
    Envoyer une photo « originale » par messagerie ou par courriel transmet en général les métadonnées **intactes**. C'est le canal par lequel une localisation fuit le plus souvent.

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. Qu'est-ce qu'un photosite, et combien de couleurs mesure-t-il ?
    2. Pourquoi y a-t-il deux fois plus de filtres verts ?
    3. Pourquoi la vidéo en ligne serait-elle impossible sans compression ?
    4. Quelle différence entre compression avec et sans perte ?
    5. Pourquoi une image beaucoup repartagée devient-elle floue ?
    6. Que sont les métadonnées EXIF, et laquelle est la plus sensible ?

??? success "Réponses"
    1. Une cellule du capteur sensible à la lumière. Elle ne mesure qu'**une seule** composante colorée ; les deux autres sont calculées à partir des voisins.
    2. Parce que l'œil humain est le plus sensible au vert — c'est ce que traduisaient déjà les coefficients de conversion en gris.
    3. Une minute de vidéo non compressée pèserait environ **51 Go** ; deux heures dépasseraient 6 To.
    4. **Sans perte** : l'original est récupérable à l'identique. **Avec perte** : de l'information est définitivement supprimée.
    5. Chaque réenregistrement en JPEG **perd** un peu plus d'information ; les pertes s'accumulent à chaque partage.
    6. Des informations *sur* l'image stockées dans le fichier. Les plus sensibles sont les **coordonnées GPS**, surtout combinées à la date et à l'heure.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc B"
    - Un **photosite** mesure une seule couleur ; les deux autres sont **calculées**. Une photo contient dès l'origine des valeurs reconstituées.
    - Sans compression, la vidéo en ligne n'existerait pas : **51 Go** pour une minute.
    - **Sans perte** : réversible, gain modeste. **Avec perte** : irréversible, gain considérable.
    - La compression exploite la **régularité** — une image sans régularité est incompressible.
    - Les **métadonnées EXIF** transportent lieu, date, appareil et logiciel de retouche : ce sont des données personnelles.

