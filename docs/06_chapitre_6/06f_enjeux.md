---
author: Elisabeth Le Prettre (LePrettre)
title: 06e Enjeux
---


# Bloc E — Ce que l'IA change

!!! abstract "Au programme"
    Environnement · travail et création · souveraineté · usage éclairé et CRCN · bilan de l'année

!!! info "Séances 8 et 9"
    Séance 8 : les grands enjeux. Séance 9 : l'usage éclairé, et le bilan de l'année entière.

!!! quote "Ce bloc rassemble tout"
    Les données, les images, les réseaux, les infrastructures : tout ce que tu as étudié cette année se retrouve ici, appliqué à l'IA. Ce n'est pas un chapitre de plus — c'est la synthèse.

## <span style="color:#1565c0">L'environnement</span>

!!! info "Séance 8"

On a calculé, dans le module *Internet*, qu'une requête à un modèle génératif consomme environ dix fois une recherche web. Mais l'usage n'est qu'une partie du coût.

!!! example "Activité 1 — Les deux coûts"
    Il y a deux moments où un modèle consomme de l'énergie. Lesquels, et lequel est le plus lourd ?

??? success "Corrigé"
    1. **L'entraînement** : construire le modèle. Cela se fait une fois, mais mobilise d'immenses moyens de calcul pendant des semaines.
    2. **L'utilisation** : chaque requête, une fois le modèle prêt. Peu coûteuse à l'unité, mais répétée des milliards de fois.

    ```python
    def foyers_equivalents(mwh, conso_foyer_annuelle=5):
        return round(mwh / conso_foyer_annuelle)

    print(foyers_equivalents(1000), "foyers pendant un an")
    ```

    ```text
    200 foyers pendant un an
    ```

    L'entraînement d'un grand modèle peut consommer autant d'électricité que **plusieurs centaines de foyers sur une année**. Puis chaque requête ajoute son petit coût, multiplié par le nombre d'utilisateurs.

    !!! warning "Le réflexe du module Les données"
        Ces chiffres sont des **ordres de grandeur**, rarement publiés, très variables selon le mix électrique. Ne pas les citer comme des mesures.

        La compétence n'est pas de retenir « 1000 MWh », c'est de savoir **poser la question du coût** et d'exiger de savoir d'où vient un chiffre.

!!! note "🔄 Capsule d'actualité"
    L'ordre de grandeur du coût d'entraînement (« quelques centaines de foyers ») **date vite** : chaque nouvelle génération de modèles déplace ces chiffres. À réactualiser en début d'année. Ce qui reste stable, c'est la distinction entre coût d'entraînement (une fois, énorme) et coût d'usage (répété).

## <span style="color:#1565c0">Le travail et la création</span>

!!! example "Activité 2 — Remplacer, ou déplacer ?"
    On entend deux discours opposés : « l'IA va supprimer des millions d'emplois » et « l'IA va créer autant d'emplois qu'elle en supprime ».

    Que peut-on dire de solide, sans se ranger derrière l'un ou l'autre ?

??? success "Pistes de réflexion"
    Ce qu'on peut affirmer prudemment :

    - L'IA **transforme** des métiers plus qu'elle ne les fait disparaître d'un coup : elle prend en charge certaines tâches, pas des métiers entiers.
    - Les tâches les plus exposées sont les tâches **répétitives et prévisibles**, y compris intellectuelles — pas seulement manuelles.
    - De nouveaux métiers apparaissent (entraîner, superviser, vérifier ces systèmes), mais **pas nécessairement pour les mêmes personnes** ni aux mêmes endroits.

    Ce qu'on ne peut **pas** affirmer : un bilan chiffré. Les prédictions sur ce sujet sont très incertaines et souvent orientées par les intérêts de ceux qui les énoncent.

    !!! quote "La posture juste"
        Ce n'est pas au cours de trancher un débat de société ouvert. C'est de te donner de quoi le suivre : distinguer une tâche d'un métier, repérer qui parle et dans quel intérêt, se méfier des prédictions chiffrées.

!!! info "La création"
    L'IA générative pose une question neuve à la création artistique :

    - elle a été entraînée sur les œuvres d'artistes **sans leur accord** — le débat juridique du module *Images* ;
    - elle produit à un coût quasi nul ce qui demandait un métier ;
    - elle brouille la notion d'**auteur** : qui a « créé » une image générée à partir d'une description ?

    !!! quote "Une question ouverte, pas un verdict"
        Est-ce un outil de plus, comme la photographie le fut pour la peinture ? Ou une rupture qui menace des métiers entiers ?

        Les deux positions sont défendues par des gens sérieux. Le cours ne tranche pas — il te donne les éléments pour te forger ton avis.

## <span style="color:#1565c0">La souveraineté</span>

!!! info "Qui contrôle les modèles ?"
    Les modèles les plus puissants sont conçus et exploités par un très petit nombre d'entreprises, disposant des données, des calculateurs et des moyens financiers nécessaires — le tout concentré dans quelques pays.

    On retrouve, appliquées à l'IA, les trois questions du module *Internet* :

    - **où** tournent les modèles, et sous quel droit ?
    - **qui** décide de ce qu'ils acceptent ou refusent de produire ?
    - **peut-on s'en passer** si l'accès est coupé ou les conditions changées ?

!!! example "Activité 3 — Un modèle pour l'école"
    Un ministère veut mettre un assistant IA à disposition des élèves. Doit-il utiliser un service existant d'une grande entreprise étrangère, ou développer le sien ?

    Reprends le raisonnement des trois hébergements du module *Internet*.

??? success "Pistes de corrigé"
    - **Service existant** : puissant, immédiat, souvent gratuit au début. Mais dépendance totale, données des élèves envoyées hors Europe, contenu du modèle non maîtrisé, tarif et conditions susceptibles de changer.
    - **Modèle souverain** : maîtrise du contenu, des données, du droit applicable. Mais coût considérable, compétences rares, résultat probablement moins performant.

    C'est **exactement** l'arbitrage des trois hébergements : la solution la plus souveraine est la plus coûteuse et la moins performante, la plus commode est la moins maîtrisée.

    !!! tip "La cohérence de l'année"
        Ce n'est pas une coïncidence si le raisonnement est identique. La souveraineté numérique est **une seule question**, qu'on retrouve pour les données, les infrastructures et l'IA. Tu la reconnais maintenant sous toutes ses formes.

## <span style="color:#1565c0">L'usage éclairé</span>

!!! info "Séance 9"

On revient au point de départ de l'année — le bloc D de M0 — mais avec, désormais, tout ce qu'il faut pour le comprendre.

!!! success "Les règles, reprises et complétées"
    **1. Comprendre avant d'utiliser.** Tu sais maintenant pourquoi : le modèle produit du plausible, il ne comprend pas. Si tu ne peux pas juger sa réponse, tu ne peux pas l'utiliser.

    **2. Vérifier — surtout les faits.** Tu sais où est le risque : faible quand l'IA transforme ce que tu fournis, élevé quand elle produit un fait. Méfie-toi des chiffres, dates, citations, références.

    **3. Déclarer ce que tu as fait produire.** Honnêteté intellectuelle : indiquer ce qui a été généré, comme on cite une source.

    **4. Se demander si la requête valait le coût.** Tu connais maintenant ce coût : énergétique, matériel, et pour certains usages, humain.

    **5. Ne jamais confier de données personnelles.** Tu sais où elles vont : sur des serveurs, sous un droit étranger, potentiellement conservées pour entraîner de futurs modèles.

!!! info "Le cadre officiel : le CRCN"
    Ces compétences s'inscrivent dans le **cadre de référence des compétences numériques** (CRCN), le référentiel national qui structure ce qu'un élève doit maîtriser du numérique — et qui est évalué en fin de collège et de lycée.

    Un usage éclairé de l'IA en fait désormais partie : savoir formuler une demande, évaluer une réponse, respecter le droit d'auteur, protéger ses données.

!!! example "Activité 4 — Bon ou mauvais usage ?"
    Pour chaque situation, dis si l'usage est pertinent, et pourquoi.

    1. Demander à une IA de t'expliquer une notion que tu n'as pas comprise en cours.
    2. Lui faire rédiger ta dissertation et la rendre telle quelle.
    3. Lui demander de reformuler tes propres idées plus clairement.
    4. Lui demander la solution d'un exercice sans chercher toi-même.
    5. Lui faire vérifier l'orthographe d'un texte que tu as écrit.

??? success "Corrigé"
    1. **Utile** — à condition de vérifier : une explication fausse est formulée avec la même assurance qu'une vraie. Croiser avec le cours.
    2. **Fraude**, et perte pour toi : tu n'apprends rien, et tu rends un travail qui n'est pas le tien.
    3. **Utile et honnête** — les idées sont de toi, l'IA aide à les exprimer. À déclarer si le contexte l'exige.
    4. **Contre-productif.** Tu obtiens la réponse sans acquérir la méthode. Le jour de l'évaluation, tu es démuni — c'est l'élève qui apprend les corrigés par cœur du bloc B.
    5. **Utile** — c'est une transformation d'un texte fourni, donc à faible risque.

    !!! quote "Le critère qui résume tout"
        Un bon usage de l'IA te rend **plus capable**. Un mauvais usage te rend **dépendant**.

        La question à te poser n'est pas « est-ce autorisé ? » mais « après cet usage, est-ce que je sais faire quelque chose de plus, ou de moins ? ».

## <span style="color:#1565c0">Bilan de l'année</span>

!!! success "Ce que tu as appris à faire"
    En une année, tu es passé de « je ne sais pas programmer » à :

    - **écrire un programme** : variables, conditions, boucles, listes, fonctions ;
    - **traiter des données** réelles, les visualiser, en repérer les biais et les pièges ;
    - **manipuler des images** comme des tableaux de nombres ;
    - **modéliser un réseau** et écrire un algorithme de recommandation ;
    - **comprendre les infrastructures** physiques du numérique ;
    - **écrire une IA** : un classifieur, un générateur de texte.

!!! quote "Le fil qui a tout relié"
    Une seule idée a traversé toute l'année, sous des formes différentes :

    > *Une machine produit du plausible à partir de données. Ce qui est bien représenté est bien traité ; ce qui manque est mal traité ; et rien, dans le résultat, ne signale la différence.*

    Tu l'as rencontrée avec le code de M0, les mains des images, les échantillons biaisés, les hallucinations. C'est ce qui te permet, aujourd'hui, d'utiliser ces outils sans en être le jouet.

## <span style="color:#1565c0">Les métiers du numérique sont pour tout le monde</span>

Une remarque pour finir, et elle compte autant que le reste.

!!! quote "Un déséquilibre qui n'a rien de naturel"
    Les filières et les métiers du numérique et de l'IA comptent aujourd'hui **beaucoup moins de femmes que d'hommes**. Ce n'est ni une question de goût, ni une question de capacité : rien, dans ce que tu as fait cette année, ne dépend du fait d'être une fille ou un garçon.

    C'est un déséquilibre **construit** — par des représentations, des habitudes, des stéréotypes qui s'installent tôt. Et ce qui est construit peut être défait.

!!! info "Ce que l'histoire montre"
    Les débuts de l'informatique ont largement reposé sur des femmes.

    - **Ada Lovelace** a écrit le premier programme de l'histoire, un siècle avant le premier ordinateur.
    - **Grace Hopper** a conçu le premier compilateur — l'idée qu'on puisse programmer avec des mots plutôt qu'avec des nombres.
    - Les premières programmeuses des grands calculateurs, dans les années 1940, étaient en majorité des femmes.

    Ce n'est que plus tard que le métier s'est refermé sur une image masculine. Cette image est récente, et elle n'a rien d'inévitable.

!!! success "Ce qui est vrai pour toi, quel que soit ton genre"
    - Tu as **écrit des programmes** cette année : un classifieur, un générateur de texte, un système de recommandation. Tu sais le faire.
    - Ces compétences ouvrent sur une **immense variété de métiers** — pas seulement « informaticien » : santé, création, environnement, journalisme, droit, recherche. Le numérique traverse tout.
    - Les études qui y mènent te sont **aussi accessibles qu'à n'importe qui**. La seule question qui vaille est : est-ce que ça t'intéresse ?

!!! quote "À l'intention de chacune et chacun"
    Si tu es une fille et que ces sujets t'ont plu : ne laisse personne — pas même une petite voix intérieure — te faire croire que « ce n'est pas pour toi ». L'histoire dit exactement le contraire.

    Si tu es un garçon : une équipe qui conçoit les outils numériques de demain a besoin de tous les regards. Un numérique construit par une seule moitié de l'humanité se trompe sur l'autre — c'est même, techniquement, une des formes du **biais** que tu as étudiées toute l'année.

!!! abstract "Et après la seconde ?"
    Si ces sujets t'ont intéressé, l'enseignement de **NSI** (Numérique et Sciences Informatiques) approfondit la programmation et l'algorithmique en première et terminale.

    Mais ces compétences ne servent pas qu'à devenir informaticien : comprendre le numérique est devenu nécessaire dans presque tous les métiers, et pour être un citoyen libre dans un monde où l'IA décide d'une part croissante de ce qui nous entoure.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc E"
    - L'IA a un coût **d'entraînement** (une fois, énorme) et **d'usage** (répété). Les chiffres sont incertains : demander leur source.
    - Elle **transforme** le travail plus qu'elle ne le supprime — mais pas pour les mêmes personnes. Se méfier des prédictions chiffrées.
    - La **souveraineté** de l'IA pose les mêmes questions que celle des données et des infrastructures.
    - Usage éclairé : **comprendre, vérifier, déclarer, mesurer le coût, protéger ses données** — c'est le CRCN.
    - Le critère ultime : un bon usage te rend **plus capable**, un mauvais te rend **dépendant**.
    - Les métiers du numérique sont **ouverts à tout le monde** : le déséquilibre filles/garçons est construit, pas naturel — et l'histoire de l'informatique commence avec des femmes.

