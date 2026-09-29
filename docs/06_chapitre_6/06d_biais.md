---
author: Elisabeth Le Prettre (LePrettre)
title: 06c Biais
---

# Bloc C — Quand les données mentent

!!! abstract "Au programme"
    Un biais reproduit par le code · recommandation · prédiction et ses limites · les décisions à fort enjeu

!!! info "Séances 4 et 5"
    Séance 4 : voir un biais se transmettre au modèle, par le code. Séance 5 : recommander, prédire, et les limites.

!!! quote "Le fil de l'année arrive à son point de convergence"
    On a rencontré le mot **biais** trois fois : dans *Les données* (un échantillon non représentatif), dans *Images* (les mains ratées), dans le bloc D de M0 (le code C qui échouait sur les négatifs).

    On va maintenant le **produire nous-mêmes**, avec le classifieur du bloc B, et voir précisément comment il naît.

## <span style="color:#1565c0">Fabriquer un biais</span>

Reprenons le classifieur de fruits. Mais cette fois, donnons-lui des données **déséquilibrées** : beaucoup d'oranges, presque pas de pommes.

!!! example "Activité 1 — Le jeu truqué"
    ```python
    desequilibre = [
     [150,7,"orange"], [170,8,"orange"], [140,6,"orange"], [160,9,"orange"],
     [155,8,"orange"], [165,7,"orange"], [145,9,"orange"],
     [130,2,"pomme"]]   # une seule pomme !

    print(classer([140, 4], desequilibre))
    ```

    Le point `[140, 4]` est une pomme un peu plus rugueuse que la moyenne. Que répond le modèle ?

??? success "Résultat"
    ```text
    orange
    ```

    **Le modèle se trompe.** Une pomme légèrement rugueuse est classée orange.

    Pourquoi ? Avec une seule pomme dans les données, le voisinage de presque tout point est peuplé d'oranges. Le modèle n'a pas assez d'exemples de pommes pour savoir à quoi elles ressemblent vraiment.

    !!! danger "Le mécanisme du biais, en une phrase"
        Ce n'est **pas** une erreur de code. Le programme est correct. C'est une conséquence directe des **données** : ce qui est sous-représenté est mal reconnu.

        C'est mot pour mot :

        - le **biais d'échantillonnage** du module *Les données* ;
        - les **mains ratées** du module *Images* — mal représentées, donc mal produites ;
        - le **code C** de M0 — appris sur des cas positifs, faux sur les négatifs.

        Quatre contextes, un seul mécanisme. Tu viens de le fabriquer toi-même.

!!! example "Activité 2 — Corriger"
    Comment corriger ce biais ? Propose deux méthodes, et discute leurs limites.

??? success "Corrigé"
    1. **Ajouter des exemples de pommes**, jusqu'à équilibrer. C'est la bonne méthode — mais elle suppose qu'on **remarque** le déséquilibre, et qu'on ait accès à ces exemples.
    2. **Rééquilibrer artificiellement** en dupliquant les pommes existantes. Cela aide un peu, mais on n'apprend rien de nouveau : si la seule pomme connue n'est pas représentative, la dupliquer ne fait que répéter son cas particulier.

    !!! quote "Le point difficile"
        La vraie difficulté n'est pas de corriger un biais : c'est de le **remarquer**.

        Un modèle biaisé fonctionne parfaitement sur les données majoritaires. Le déséquilibre ne se voit pas dans le taux de réussite global — il faut aller regarder la réussite **groupe par groupe**. C'était déjà la leçon du module *Les données* : la bonne question est *qui manque ?*

## <span style="color:#1565c0">Recommander</span>

!!! info "Séance 5"

Tu as déjà écrit un système de recommandation dans le module *Réseaux sociaux* : suggérer des amis d'après les amis communs. Vu d'ici, c'est de l'apprentissage.

!!! example "Activité 3 — La recommandation est une classification"
    Un service veut recommander des films. Il dispose, pour chaque utilisateur, des films aimés.

    En quoi « recommander un film » ressemble-t-il au classifieur de fruits ?

??? success "Corrigé"
    C'est le **même principe du plus proche voisin** :

    - on cherche les utilisateurs qui **ressemblent** le plus à toi (qui ont aimé les mêmes films) ;
    - on te recommande ce qu'ils ont aimé et que tu n'as pas encore vu.

    « Se ressembler » ne se mesure plus en masse et rugosité, mais en goûts communs. L'algorithme, lui, est le même.

    !!! warning "Le biais revient, sous une autre forme"
        Un système de recommandation te propose ce qu'ont aimé les gens qui te ressemblent. Il te **enferme donc dans ce que tu aimes déjà** — c'est exactement la bulle de filtre du module *Réseaux sociaux*.

        Ce n'est pas un défaut du système : c'est ce qu'on lui a demandé. Il optimise la ressemblance, donc il resserre.

## <span style="color:#1565c0">Prédire</span>

Prédire, c'est estimer une valeur inconnue à partir de valeurs connues. Météo, trafic, consommation, risques.

!!! example "Activité 4 — Ce qu'une prédiction peut et ne peut pas faire"
    Un système prédit la note d'un élève au bac à partir de ses notes de l'année, de son assiduité et de son établissement.

    1. Sur quoi s'appuie-t-il pour prédire ?
    2. Que se passe-t-il pour un élève au parcours atypique ?
    3. Faut-il utiliser cette prédiction pour l'orienter ?

??? success "Corrigé"
    1. Sur les **régularités du passé** : ce qu'ont obtenu les élèves ayant eu des profils semblables les années précédentes.
    2. Le système le classe comme les cas qu'il connaît. Un parcours atypique, par définition **sous-représenté**, sera mal prédit — le biais, encore.
    3. **C'est une question grave.** Une prédiction décrit une tendance statistique sur un groupe ; elle ne dit rien de certain sur un **individu**. S'en servir pour orienter, c'est risquer d'enfermer un élève dans le destin moyen de ceux qui lui ressemblent — et de **reproduire les inégalités passées** au lieu de les corriger.

    !!! danger "La règle à retenir sur les prédictions"
        Une prédiction est une **probabilité sur un groupe**, jamais une certitude sur une personne.

        Plus l'enjeu est grave — orientation, embauche, justice, crédit — plus il est dangereux de laisser une prédiction décider seule. Le rôle d'un humain n'est pas d'appliquer la prédiction, mais de **décider si elle s'applique à ce cas précis**.

## <span style="color:#1565c0">Les décisions à fort enjeu</span>

!!! info "Là où l'IA décide de la vie des gens"
    Des systèmes d'apprentissage sont déjà utilisés pour aider à décider : accorder un crédit, trier des candidatures, évaluer un risque de récidive, prioriser des dossiers médicaux.

    Trois problèmes s'y cumulent, tous rencontrés cette année :

    - le **biais** : le système reproduit les déséquilibres de ses données ;
    - l'**opacité** : sa décision n'est pas explicable, puisqu'elle est apprise et non écrite ;
    - l'**effet d'autorité** : une décision « calculée » paraît objective, donc on la conteste moins.

!!! quote "Le piège de l'objectivité apparente"
    Un chiffre produit par une machine semble neutre. Mais il porte tous les biais des données qui l'ont produit — il les rend seulement **invisibles**, sous une couche d'apparente objectivité.

    « L'ordinateur l'a calculé » n'est pas une garantie de justice. C'est parfois l'inverse : une injustice à laquelle on a retiré la possibilité de protester.

!!! success "Le principe qui doit rester"
    Pour toute décision qui engage la vie d'une personne, un système peut **aider**, il ne doit pas **décider seul**. Un humain doit pouvoir comprendre, contester, et passer outre.

    C'est un principe qu'on retrouve dans le droit européen : le droit de ne pas faire l'objet d'une décision entièrement automatisée ayant des effets importants.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc C"
    - Un **biais** des données se transmet au modèle : ce qui est sous-représenté est mal reconnu. Tu l'as fabriqué toi-même.
    - Le plus dur n'est pas de corriger un biais, c'est de le **remarquer** — il faut regarder groupe par groupe.
    - **Recommander**, c'est classer par ressemblance : d'où la bulle de filtre.
    - Une **prédiction** est une probabilité sur un groupe, jamais une certitude sur une personne.
    - Une décision « calculée » n'est pas neutre : elle rend les biais **invisibles**.
    - Pour une décision à fort enjeu, l'IA aide, un **humain décide** — et doit pouvoir contester.

