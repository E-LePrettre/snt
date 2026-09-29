---
author: Elisabeth Le Prettre (LePrettre)
title: 03d Images générées
---


# Bloc D — Images générées

!!! abstract "Au programme"
    Comment une IA fabrique une image · d'où viennent ses images · deepfakes · vérifier · droit à l'image et droits d'auteur

!!! info "Séance 4"
    Dernière séance du module. Elle prolonge directement le bloc D de M0 : *ce qui est plausible n'est pas ce qui est vrai*.

## <span style="color:#1565c0">Du filtre à la génération</span>

Au bloc C, tu as transformé une image en changeant quatre nombres. Une IA générative fait la même chose — changer des nombres dans une grille — à trois différences près :

| Ton filtre | Une IA générative |
| --- | --- |
| tu écris la règle (`9 - pixel`) | aucune règle n'est écrite |
| 64 pixels | 12 millions de pixels |
| tu pars d'une image existante | elle part de **bruit aléatoire** |

!!! info "Le principe, sans technicité excessive"
    Un modèle générateur d'images a été entraîné sur des **millions d'images accompagnées de leur description**.

    À force d'exemples, il a appris des **régularités** : à quoi ressemblent les pixels autour du mot « chat », comment tombe une ombre, quelle texture a une brique.

    Pour produire une image, il part d'une grille de **pixels aléatoires** — de la neige — et la modifie progressivement, étape après étape, de façon à ce qu'elle ressemble de plus en plus à ce que la description appelle.

!!! quote "La phrase à retenir"
    Une IA générative ne cherche pas dans une base d'images existantes pour recopier. Elle **fabrique** une grille de pixels qui a l'air d'appartenir au monde décrit.

    Elle produit du **plausible**. Exactement comme les trois codes du bloc D de M0 : plausibles, et pourtant faux.

## <span style="color:#1565c0">Pourquoi les mains ont longtemps été ratées</span>

!!! example "Activité 1 — L'énigme des doigts"
    Pendant plusieurs années, les images générées échouaient sur un point précis : les **mains**. Six doigts, articulations impossibles, pouces à l'envers — alors que les visages étaient parfaits.

    Pourquoi les mains plutôt que les visages ?

??? success "Corrigé"
    Trois raisons, toutes liées aux **données d'entraînement** :

    1. **Les mains sont rarement le sujet.** Dans des millions de photos, on trouve d'innombrables visages nets et cadrés. Les mains sont presque toujours petites, floues, en bord de cadre.
    2. **Elles ont une infinité de configurations.** Un visage a toujours deux yeux au-dessus d'un nez. Une main peut être ouverte, fermée, de profil, partiellement cachée, en mouvement.
    3. **Rien n'apprend au modèle qu'une main a cinq doigts.** Il n'a pas de notion d'anatomie : il a des régularités statistiques. Si les mains sont mal représentées dans les données, il produit du « à peu près une main ».

    !!! success "C'est exactement le mécanisme du biais"
        Ce qui est **fréquent et net** dans les données d'entraînement est bien reproduit. Ce qui est rare ou mal représenté est mal reproduit.

        C'est le **code C** du bloc D de M0 : il marchait sur des notes (toujours positives, fréquentes dans les exemples) et échouait sur des températures négatives. Et c'est le **biais** du module *Les données*.

        Même phénomène, trois contextes différents.

!!! warning "Et aujourd'hui ?"
    Les mains sont largement corrigées — les données d'entraînement ont été enrichies exprès. **Le défaut visible disparaît, le mécanisme demeure.**

    Ne retiens donc pas « les IA ratent les mains » : c'est déjà faux. Retiens *ce qui est mal représenté dans les données est mal produit*. Cette phrase-là restera vraie.

## <span style="color:#1565c0">D'où viennent les images d'entraînement ?</span>

!!! danger "Une question non résolue"
    Ces modèles ont été entraînés sur d'immenses collections d'images collectées sur le web : photographies, illustrations, œuvres d'artistes vivants, images de presse.

    Deux questions, toujours ouvertes :

    - **Le droit d'auteur.** Utiliser une œuvre pour entraîner un modèle est-il un usage nécessitant l'autorisation de l'auteur ? Des procès sont en cours dans plusieurs pays, et les législations évoluent.
    - **Le consentement.** Des photos de personnes ordinaires, publiées il y a quinze ans, se retrouvent dans ces collections sans que personne ait jamais été prévenu.

!!! example "Activité 2 — Le raisonnement juridique"
    Un modèle est entraîné sur les œuvres d'un illustrateur vivant. On lui demande ensuite une image « dans le style de » cet illustrateur.

    1. L'image produite est-elle une copie d'une de ses œuvres ?
    2. L'illustrateur devrait-il être rémunéré ?
    3. Un **style** peut-il appartenir à quelqu'un ?

??? success "Pistes de réflexion"
    1. **Non**, techniquement : l'image est nouvelle, aucun pixel n'est copié. C'est l'argument principal des concepteurs de ces outils.
    2. C'est le cœur du litige. Ses œuvres ont bien servi à produire l'outil, sans autorisation ni rémunération. Mais le droit d'auteur protège des **œuvres**, pas la capacité à en produire de semblables.
    3. En droit français, **un style n'est pas protégeable** — seules les œuvres concrètes le sont. Un peintre peut légalement imiter le style d'un autre.

       Mais ce principe a été conçu à une époque où imiter un style demandait des années d'apprentissage. Il produit des effets très différents quand l'imitation devient instantanée et illimitée.

    !!! quote "Ce qu'il faut en retenir"
        Ce n'est **pas** une question technique. La technique ne dit pas ce qui est juste. Ce débat est juridique et politique, et il est en train de se trancher — y compris par vos usages.

## <span style="color:#1565c0">Les deepfakes</span>

Un **deepfake** est un contenu synthétique représentant une personne réelle dans une situation qui n'a jamais eu lieu.

!!! danger "Trois conséquences distinctes"
    **1. La diffamation et le harcèlement.** Faire dire ou faire n'importe quoi à quelqu'un. Les victimes les plus nombreuses sont des femmes, et les contenus intimes non consentis constituent le premier usage recensé de ces outils.

    **2. La perte de valeur de preuve.** Pendant plus d'un siècle, une photographie a constitué un élément de preuve. Ce n'est plus le cas à elle seule.

    **3. Le doute généralisé — le plus insidieux.** Le risque n'est pas seulement de croire au faux. C'est de **ne plus croire au vrai** : un document authentique peut désormais être balayé d'un « c'est une IA ».

!!! quote "L'effet le plus grave n'est pas celui qu'on croit"
    Une image fausse peut être démentie. Mais si plus rien ne peut être prouvé par l'image, alors n'importe qui peut nier n'importe quoi.

    Ce n'est pas la crédulité qui est menacée : c'est la **possibilité même d'établir un fait**.

## <span style="color:#1565c0">Vérifier une image</span>

!!! success "Ce qui marche durablement"
    **1. Remonter à la source.** Qui a publié cette image en premier, et quand ? Un compte créé la semaine dernière n'est pas une source.

    **2. Chercher l'image ailleurs.** Une recherche par image révèle souvent qu'elle est ancienne, ou prise dans un autre contexte. **Le procédé le plus fréquent n'est pas la fabrication : c'est la republication d'une vraie image hors de son contexte.**

    **3. Croiser avec d'autres sources indépendantes.** Un événement réel laisse plusieurs traces, sous plusieurs angles.

    **4. Regarder les métadonnées** quand elles sont disponibles — le bloc B a montré ce qu'elles contiennent, y compris le logiciel de retouche.

!!! warning "Ce qui ne marche pas durablement"
    Chercher les défauts visuels. Les six doigts, les textes illisibles en arrière-plan, les reflets incohérents : tout cela **disparaît d'une génération de modèles à l'autre**.

    Une méthode de vérification fondée sur l'apparence est périmée dans l'année. La vérification par la **source** ne se périme pas.

!!! info "Une piste technique : la provenance"
    Des normes sont en cours de déploiement pour attacher à un fichier un historique **signé cryptographiquement** : quel appareil l'a produit, quelles modifications ont été appliquées, par quel logiciel.

    L'approche est prometteuse mais partielle : elle certifie ce qui est signé, elle ne dit rien de ce qui ne l'est pas. Une capture d'écran fait disparaître toute signature.

## <span style="color:#1565c0">Le droit</span>

!!! abstract "Le droit à l'image"
    Toute personne dispose d'un droit sur son image. Publier la photographie d'une personne identifiable **sans son accord** constitue une atteinte à sa vie privée.

    Quelques précisions utiles :

    - L'accord doit être donné **pour un usage précis**. Accepter une photo de classe n'autorise pas sa publication en ligne.
    - Pour un **mineur**, l'accord des représentants légaux est requis.
    - Une personne **non identifiable** — de dos, noyée dans une foule — n'est pas concernée.
    - Créer ou diffuser un **montage** représentant une personne sans son consentement est spécifiquement réprimé.

!!! abstract "Les droits d'auteur"
    Une image trouvée en ligne n'est pas libre d'usage par défaut. Le fait qu'elle soit accessible ne dit rien de ce qu'on a le droit d'en faire.

    - Certaines images portent une **licence libre** qui autorise la réutilisation, souvent à condition de citer l'auteur.
    - Les banques d'images libres de droits existent : c'est le bon réflexe pour un exposé ou un site.
    - **Citer sa source est un minimum**, mais ne rend pas légal un usage non autorisé.

!!! question "À toi de jouer D.1 ⭐⭐ — Quatre situations"
    Pour chacune, dis ce qui est en jeu et si c'est autorisé.

    1. Tu publies une photo de groupe prise en sortie scolaire, où l'on reconnaît tes camarades.
    2. Tu illustres un exposé avec une image trouvée par un moteur de recherche.
    3. Tu génères une image représentant un professeur du lycée dans une situation ridicule.
    4. Tu génères une illustration pour ton exposé et tu ne le mentionnes pas.

??? success "Corrigé"
    1. **Droit à l'image.** Chaque personne identifiable doit avoir donné son accord — et pour des mineurs, leurs représentants légaux. Publier sans cet accord est une atteinte à la vie privée.
    2. **Droits d'auteur.** Une image accessible en ligne n'est pas pour autant réutilisable. Chercher une image sous licence libre, et citer l'auteur.
    3. **Les deux, et davantage.** Atteinte au droit à l'image, montage sans consentement, et selon le contenu : injure, diffamation ou cyberharcèlement. Le fait que l'image soit visiblement fausse **ne supprime pas** l'infraction.
    4. Ce n'est pas illégal, mais **c'est une faute d'honnêteté intellectuelle**. C'est la quatrième règle du bloc D de M0 : *déclarer ce qu'on a fait produire*. Dans un travail scolaire comme professionnel, on indique ce qui a été généré.

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. De quoi part une IA générative pour produire une image ?
    2. Pourquoi les mains ont-elles longtemps été ratées ?
    3. Pourquoi ne faut-il pas retenir « les IA ratent les mains » ?
    4. Quel est l'effet le plus grave des deepfakes ?
    5. Quelle méthode de vérification ne se périme pas ?
    6. Une image trouvée en ligne est-elle libre d'usage ?

??? success "Réponses"
    1. De **bruit aléatoire**, qu'elle modifie progressivement pour le rapprocher de ce que décrit la demande. Elle ne recopie pas d'images existantes.
    2. Parce qu'elles étaient **mal représentées** dans les données d'entraînement : rarement nettes, rarement le sujet, et de configurations très variables.
    3. Parce que c'est déjà faux — le défaut a été corrigé. Ce qui reste vrai, c'est le mécanisme : **ce qui est mal représenté dans les données est mal produit**.
    4. Le **doute généralisé** : si plus rien ne peut être prouvé par l'image, n'importe qui peut nier n'importe quoi.
    5. La vérification par la **source** — qui a publié, quand, est-ce confirmé ailleurs. Les indices visuels se périment.
    6. **Non.** L'accessibilité ne dit rien des droits. Chercher une licence libre et citer l'auteur.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc D"
    - Une IA générative part de **bruit aléatoire** et le transforme jusqu'à obtenir du **plausible**.
    - Ce qui est mal représenté dans les données est mal produit — c'est le même mécanisme que le **biais**.
    - Les défauts visibles disparaissent ; le mécanisme reste. Ne pas fonder sa vérification sur l'apparence.
    - L'effet le plus grave des deepfakes est le **doute généralisé**.
    - Vérifier, c'est **remonter à la source** — le procédé le plus courant reste la republication hors contexte.
    - **Droit à l'image** : accord requis, pour un usage précis. **Droits d'auteur** : accessible ≠ réutilisable.
    - Une image générée pour un travail se **déclare**.

!!! abstract "Et maintenant ?"
    Tu sais qu'une image est un tableau de nombres, qu'on peut le transformer, et qu'on peut même le fabriquer.

    Reste une question : où circulent toutes ces images, et où sont-elles stockées ? Ce sera l'objet des modules suivants.

