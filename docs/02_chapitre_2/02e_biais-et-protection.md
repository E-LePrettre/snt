---
author: Elisabeth Le Prettre (LePrettre)
title: 02d Biais et protection
---


# Bloc D — Biais, protection et souveraineté

!!! abstract "Au programme"
    Échantillon et représentativité · biais et IA · donnée personnelle · anonymisation et ré-identification · RGPD · souveraineté

!!! info "Séances 5 et 6"
    Séance 5 : quand les données trompent. Séance 6 : protéger les données.

!!! quote "Le fil de l'année"
    Dans le bloc D de M0, on avait vu qu'une IA **apprend à partir de données**, et qu'un jeu déséquilibré produit un modèle déséquilibré. On l'avait montré en comptant des prénoms.

    Ce bloc reprend cette idée là où elle devient sérieuse : sur de vraies données, avec de vraies conséquences.

## <span style="color:#1565c0">D'où viennent les données ?</span>

Un jeu de données n'est jamais le réel : c'est un **échantillon** du réel, collecté par quelqu'un, à un moment, selon une méthode.

!!! example "Activité 1 — Deux enquêtes"
    On veut connaître le temps d'écran moyen des élèves de seconde du lycée.

    **Enquête A** — on interroge les quatre élèves du club informatique :

    ```python
    club = [90, 60, 120, 90]
    print("Enquête A :", round(moyenne(club), 1), "min")
    ```

    **Enquête B** — on interroge les dix élèves d'une classe entière :

    ```python
    print("Enquête B :", round(moyenne(ecran), 1), "min")
    ```

    Compare. Laquelle croire ?

??? success "Corrigé"
    ```text
    Enquête A : 90.0 min
    Enquête B : 178.5 min
    ```

    Du simple au double. Pourtant, aucun chiffre n'est faux : chaque moyenne est correctement calculée sur les personnes interrogées.

    **Le problème est ailleurs** : l'enquête A n'interroge pas des élèves de seconde en général, mais des élèves du club informatique. Rien ne dit qu'ils ressemblent aux autres — et il est même probable qu'ils aient un rapport particulier aux écrans.

    On dit que l'échantillon n'est pas **représentatif**.

!!! danger "Le biais d'échantillonnage"
    Un **biais d'échantillonnage** apparaît quand les personnes interrogées ne ressemblent pas à la population qu'on prétend décrire.

    Il ne se voit **jamais dans les chiffres**. Le calcul est juste, la moyenne est exacte, le graphique est propre. Seule la connaissance de **comment les données ont été collectées** permet de le repérer.

    C'est pour cette raison que les métadonnées du bloc A comptent autant que les données elles-mêmes.

!!! question "À toi de jouer D.1 ⭐⭐ — Repérer le biais"
    Pour chacune de ces enquêtes, indique qui est oublié :

    1. Un sondage sur les habitudes de lecture réalisé à la sortie d'une librairie.
    2. Une enquête sur la satisfaction d'un service, envoyée par courriel aux clients.
    3. Un questionnaire sur les transports diffusé uniquement sur un réseau social.
    4. Une étude sur la réussite scolaire menée seulement auprès des élèves présents le jour du test.

??? success "Corrigé"
    1. Ceux qui ne lisent pas — c'est-à-dire précisément ceux qu'on voulait mesurer.
    2. Ceux qui n'ont pas d'adresse électronique, ne la consultent pas, ou sont trop mécontents pour répondre. Les gens très satisfaits et très mécontents répondent davantage que les indifférents.
    3. Ceux qui n'utilisent pas ce réseau — souvent les plus âgés, ou ceux qui ont un accès limité à internet.
    4. Les absents. Or l'absentéisme est justement lié à la difficulté scolaire : on exclut le groupe le plus concerné.

    !!! tip "La question à poser systématiquement"
        Non pas « que disent les données ? » mais **« qui manque dans ces données ? »**

## <span style="color:#1565c0">Du biais des données au biais des systèmes</span>

Ce n'est pas un problème de sondage. C'est le mécanisme central des systèmes qui apprennent.

!!! quote "Le mécanisme, en une phrase"
    Une IA apprend ce qui est **fréquent** dans ses données d'entraînement. Si un groupe y est absent ou sous-représenté, le système fonctionnera mal pour lui — sans que personne l'ait voulu, et sans que rien dans le code ne le signale.

Trois exemples documentés :

- Des systèmes de **reconnaissance faciale** entraînés majoritairement sur des visages clairs et masculins ont montré des taux d'erreur nettement plus élevés sur les femmes et les personnes à peau foncée.
- Des outils de **tri de candidatures** entraînés sur les recrutements passés d'une entreprise ont reproduit les déséquilibres de ces recrutements, au lieu de les corriger.
- Des systèmes de **reconnaissance vocale** fonctionnent moins bien sur les accents régionaux, moins représentés dans les données d'entraînement.

!!! warning "Un biais n'est pas une intention"
    Personne n'a programmé une règle discriminatoire. Le système a simplement **appris ce qu'on lui a montré**, y compris les déséquilibres.

    C'est ce qui rend le problème difficile : on ne peut pas le corriger en relisant le code. Il faut examiner **les données**.

!!! example "Activité 2 — Le jeu de données de la classe"
    Reprends le jeu de données du module. Suppose qu'on l'utilise pour entraîner un système qui prédit si un élève réussira l'année.

    1. Sur combien d'individus s'appuie-t-il ?
    2. Quelles informations n'y figurent pas et pourraient compter ?
    3. Que se passerait-il si on l'appliquait à un lycée d'une autre région ?

??? success "Corrigé"
    1. **Dix.** C'est dérisoire. Aucune conclusion fiable ne peut en sortir.
    2. Beaucoup de choses : le travail personnel, le sommeil, la situation familiale, la santé, l'accès à un lieu calme, l'aide disponible à la maison. Le jeu contient trois colonnes ; la réussite scolaire dépend de dizaines de facteurs.
    3. Il transporterait les particularités de **cette** classe comme si elles étaient des lois générales.

    !!! danger "Le vrai danger"
        Un système entraîné là-dessus produirait quand même des prédictions, avec des pourcentages d'apparence sérieuse. Rien dans sa sortie n'indiquerait qu'il repose sur dix personnes et trois colonnes.

        **Un résultat faux ne se présente pas comme faux.** C'était déjà la leçon des trois codes du bloc D de M0.

## <span style="color:#1565c0">Qu'est-ce qu'une donnée personnelle ?</span>

!!! info "La définition"
    Une **donnée personnelle** est toute information se rapportant à une personne physique **identifiée ou identifiable**, directement ou indirectement.

    Le mot décisif est **indirectement** : une donnée n'a pas besoin de contenir un nom pour être personnelle.

!!! example "Activité 3 — Personnelle ou non ?"
    1. « Camille Durand, 15 ans »
    2. « L'élève né le 12 mars qui habite au 4 rue des Lilas »
    3. « La température à Mont-de-Marsan est de 18 °C »
    4. « L'unique élève de la classe qui joue du basson »
    5. Une adresse IP

??? success "Corrigé"
    1. **Personnelle** — identification directe.
    2. **Personnelle** — pas de nom, mais la combinaison désigne une seule personne.
    3. **Non personnelle** — elle ne concerne personne en particulier.
    4. **Personnelle** — « l'unique » suffit à identifier.
    5. **Personnelle** — la loi européenne la considère comme telle, car elle permet de remonter à un abonné.

    !!! tip "Le critère"
        Ce n'est pas la présence d'un nom qui compte, c'est la possibilité d'**isoler une personne**. Une combinaison de données banales peut y suffire.

## <span style="color:#1565c0">L'anonymisation est plus dure qu'elle n'en a l'air</span>

En M0, tu as écrit une fonction qui transforme `Camille` en `C......`. Testons-la sérieusement.

!!! example "Activité 4 — Ré-identifier"
    ```python
    def anonymise(prenom):
        return prenom[0] + "." * (len(prenom) - 1)


    for i in range(len(table)):
        print(anonymise(table[i][0]), table[i][1], table[i][2], table[i][3])
    ```

    Maintenant, la vraie question : **combien d'élèves restent identifiables** par le seul couple (initiale, longueur du prénom) ?

    Écris le programme qui le compte.

??? success "Corrigé"
    ```python
    prenoms = colonne(table, 0)

    cles = []
    for p in prenoms:
        cles.append(p[0] + str(len(p)))

    uniques = 0
    for cle in cles:
        occurrences = 0
        for autre in cles:
            if cle == autre:
                occurrences = occurrences + 1
        if occurrences == 1:
            uniques = uniques + 1

    print(uniques, "profils sur", len(prenoms), "sont uniques")
    ```

    ```text
    8 profils sur 10 sont uniques
    ```

    !!! danger "Le résultat"
        **Huit élèves sur dix restent identifiables.** Un camarade de classe qui sait qu'il n'y a qu'un seul prénom de 7 lettres commençant par G retrouve Gabriel immédiatement — et lit ses notes.

        L'anonymisation a masqué le prénom sans protéger personne.

!!! info "Pseudonymisation ≠ anonymisation"
    | | Pseudonymisation | Anonymisation |
    | --- | --- | --- |
    | Principe | remplacer l'identifiant | rendre la ré-identification impossible |
    | Ré-identification | possible | impossible |
    | Statut juridique | **reste une donnée personnelle** | sort du champ du RGPD |

    Ce qu'on a fait est une **pseudonymisation**. Le RGPD la considère toujours comme une donnée personnelle, avec toutes les obligations qui vont avec.

    Une vraie anonymisation est un problème difficile : il faut supprimer non seulement les identifiants, mais toutes les **combinaisons** susceptibles d'isoler quelqu'un.

## <span style="color:#1565c0">Le RGPD</span>

Le **Règlement général sur la protection des données** est le texte européen qui encadre le traitement des données personnelles depuis 2018.

!!! info "Au-delà des données personnelles : les secrets protégés"
    La protection de la vie privée n'est pas la seule en jeu. Certaines informations relèvent de **secrets protégés** par la loi : secret médical, secret professionnel, secret des affaires, secret de la défense. Manipuler des données, c'est aussi savoir reconnaître celles qu'on n'a **pas le droit** de collecter, de diffuser ou de faire traiter par un outil — y compris par une IA.

!!! abstract "Les principes qui te concernent"
    - **Finalité** — on collecte pour un usage précis, annoncé à l'avance. On ne peut pas réutiliser les données pour autre chose.
    - **Minimisation** — on ne collecte que ce qui est nécessaire à cet usage.
    - **Consentement** — il doit être libre, éclairé et révocable. Une case pré-cochée n'est pas un consentement.
    - **Durée limitée** — on ne conserve pas indéfiniment.
    - **Sécurité** — on protège ce qu'on détient.

!!! abstract "Tes droits"
    - **Accès** — savoir quelles données une organisation détient sur toi.
    - **Rectification** — faire corriger une erreur.
    - **Effacement** — demander la suppression.
    - **Opposition** — refuser certains traitements.
    - **Portabilité** — récupérer tes données pour les emporter ailleurs.

!!! note "Pour les mineurs"
    En France, un mineur de moins de 15 ans ne peut pas consentir seul au traitement de ses données par un service en ligne : l'accord d'un titulaire de l'autorité parentale est requis.

!!! question "À toi de jouer D.2 ⭐⭐ — Le cas du module"
    Reviens au jeu de données du module : prénoms, notes, temps d'écran d'élèves.

    1. Aurait-on le droit de le publier tel quel sur le site du lycée ?
    2. Et après avoir anonymisé les prénoms ?
    3. Quel principe du RGPD la colonne `ecran` pose-t-elle problème ?

??? success "Corrigé"
    1. **Non.** Ce sont des données personnelles de mineurs, dont des résultats scolaires. Aucune finalité ne justifierait une publication ouverte.
    2. **Non plus** — l'activité 4 vient de le montrer : 8 profils sur 10 restent identifiables. La pseudonymisation ne suffit pas.
    3. La **minimisation**. Pourquoi un établissement collecterait-il le temps d'écran quotidien de ses élèves ? Cette donnée n'est nécessaire à aucune mission de l'école. Elle n'aurait pas dû être collectée du tout.

    !!! quote "Le réflexe à garder"
        La meilleure protection d'une donnée personnelle, c'est de **ne pas la collecter**.

## <span style="color:#1565c0">Où sont les données ?</span>

Une donnée est stockée quelque part : un disque, dans un bâtiment, dans un pays, exploité par une entreprise soumise à un droit.

!!! info "La souveraineté numérique"
    C'est la capacité d'un pays, d'une administration ou d'une école à **maîtriser les outils et les données dont elle dépend**.

    Trois questions concrètes :

    - **Où** sont hébergées les données ? Un serveur situé hors d'Europe relève d'une autre juridiction, qui peut autoriser des accès que le droit européen interdit.
    - **Qui** exploite le service ? Que se passe-t-il s'il ferme, change ses tarifs ou ses conditions ?
    - **Peut-on partir ?** Les données sont-elles récupérables dans un format ouvert, ou enfermées dans un format propriétaire ?

!!! tip "Le lien avec le bloc A"
    Cette dernière question rejoint ce qu'on disait du **CSV** : un format ouvert, lisible sans logiciel particulier, qu'aucune entreprise ne contrôle.

    Choisir un format ouvert, c'est déjà un choix de souveraineté.

!!! note "On y revient"
    La souveraineté sera reprise dans le module *Internet et le Web* (où sont physiquement les infrastructures) puis dans le module *Intelligence artificielle* (qui contrôle les modèles).

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. Qu'est-ce qu'un biais d'échantillonnage, et pourquoi ne se voit-il pas dans les chiffres ?
    2. Une donnée sans nom peut-elle être une donnée personnelle ?
    3. Quelle différence entre pseudonymisation et anonymisation ?
    4. Que dit le principe de minimisation ?
    5. Pourquoi le format d'un fichier est-il une question de souveraineté ?
    6. Deux colonnes varient ensemble. Que peut-on en conclure ?

??? success "Réponses"
    1. Les personnes interrogées ne représentent pas la population décrite. Il ne se voit pas dans les chiffres parce que **le calcul est juste** : seule la connaissance de la méthode de collecte permet de le repérer.
    2. **Oui**, si une combinaison d'informations permet d'isoler une personne — comme « l'unique élève qui joue du basson ».
    3. La pseudonymisation remplace un identifiant mais laisse la ré-identification possible ; elle reste soumise au RGPD. L'anonymisation rend la ré-identification impossible.
    4. On ne collecte que les données **nécessaires** à la finalité annoncée.
    5. Un format propriétaire enferme les données : on ne peut plus les lire sans le logiciel de l'entreprise qui l'a créé, ni les emporter ailleurs.
    6. **Rien sur les causes.** On observe une corrélation ; le sens du lien, ou l'existence d'une troisième cause, reste indéterminé.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc D"
    - Un jeu de données est un **échantillon**, pas le réel. La bonne question est *qui manque ?*
    - Un **biais** ne se voit pas dans les chiffres : il faut examiner la collecte.
    - Une IA apprend ce qui est fréquent dans ses données — les déséquilibres sont appris avec le reste.
    - Une donnée est **personnelle** dès qu'elle permet d'isoler quelqu'un, même sans nom.
    - Masquer un prénom **ne suffit pas** : 8 profils sur 10 restaient identifiables.
    - Le **RGPD** impose finalité, minimisation, consentement, durée limitée, sécurité — et garantit des droits.
    - La meilleure protection d'une donnée, c'est de **ne pas la collecter**.

!!! abstract "Et maintenant ?"
    Tu sais traiter un jeu de données et t'en méfier. Le module suivant, *Réseaux sociaux*, montre ce que les plateformes font des données que nous produisons tous les jours — et qui décide de ce que nous voyons.


