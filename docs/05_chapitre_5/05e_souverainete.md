---
author: Elisabeth Le Prettre (LePrettre)
title: 05d Souveraineté
---

# Bloc D — Dépendances et souveraineté

!!! abstract "Au programme"
    Qui possède les infrastructures · le droit applicable · neutralité du réseau · formats ouverts · pouvoir partir

!!! info "Séance 4"
    Dernière séance du module. On y répond à une question simple à poser et difficile à trancher : **qui décide ?**

## <span style="color:#1565c0">Un réseau sans centre, mais pas sans pouvoir</span>

Au bloc A, on a établi qu'Internet n'a **aucun centre** : chaque routeur ne connaît que ses voisins, et si un chemin disparaît, un autre est trouvé.

!!! warning "Ne pas confondre deux choses"
    L'absence de centre **technique** ne signifie pas l'absence de **pouvoir**.

    Le réseau est décentralisé dans son fonctionnement. Mais les câbles appartiennent à quelqu'un, les centres de données appartiennent à quelqu'un, les services que tout le monde utilise appartiennent à un petit nombre d'entreprises.

    Une architecture décentralisée n'empêche pas une **concentration économique**.

!!! example "Activité 1 — Remonter la chaîne"
    Tu consultes une page depuis ton téléphone. Liste tous les acteurs dont tu dépends pour que cela fonctionne.

??? success "Corrigé"
    Au minimum :

    - le **fabricant** de ton téléphone, et l'éditeur de son système d'exploitation ;
    - l'éditeur de ton **navigateur** ;
    - ton **opérateur** de téléphonie ou d'accès à Internet ;
    - les **opérateurs de transit** qui acheminent les données entre réseaux ;
    - le propriétaire des **câbles** empruntés ;
    - l'exploitant du **centre de données** qui héberge le site ;
    - le **service de nom de domaine** qui traduit le nom en adresse IP ;
    - éventuellement un **réseau de distribution de contenu**, qui garde des copies des pages près de toi ;
    - le **moteur de recherche** par lequel tu es arrivé.

    !!! success "Ce que révèle l'exercice"
        Neuf acteurs au minimum, pour une seule page. Et pour plusieurs de ces maillons, **deux ou trois entreprises se partagent l'essentiel du marché mondial**.

        C'est là que se situe la vraie dépendance : pas dans l'architecture du réseau, mais dans la concentration de chaque maillon.

## <span style="color:#1565c0">Le droit applicable</span>

!!! info "Le principe"
    Une donnée stockée sur un serveur relève du **droit du pays où se trouve ce serveur**, et du droit applicable à l'entreprise qui l'exploite.

    Une entreprise peut donc être soumise à des obligations légales incompatibles avec le droit européen — par exemple l'obligation de transmettre des données aux autorités de son pays d'origine, y compris pour des données stockées ailleurs.

!!! example "Activité 2 — Trois hébergements"
    Un lycée doit choisir où héberger les données de ses élèves : notes, absences, adresses.

    | Option | Où | Exploitant |
    | --- | --- | --- |
    | A | serveur dans l'établissement | l'établissement |
    | B | centre de données en France | entreprise française |
    | C | service en ligne | entreprise étrangère, serveurs hors Europe |

    Pour chacune : quels avantages, quels risques ?

??? success "Pistes de corrigé"
    **A — serveur local**

    - *Pour* : maîtrise totale, aucune dépendance, droit français sans ambiguïté.
    - *Contre* : il faut des compétences techniques sur place, assurer les sauvegardes, la sécurité, la continuité en cas de panne. Le risque de perte de données est souvent **plus élevé** que chez un hébergeur professionnel.

    **B — hébergeur national**

    - *Pour* : droit français et européen applicable, compétences professionnelles, sauvegardes assurées.
    - *Contre* : dépendance à un prestataire, coût, et il faut vérifier ses propres sous-traitants.

    **C — service en ligne étranger**

    - *Pour* : souvent le plus simple à mettre en œuvre, le plus riche en fonctions, parfois gratuit pour l'éducation.
    - *Contre* : droit étranger applicable, transferts de données hors Europe, dépendance forte, et **difficulté à récupérer les données** pour partir.

    !!! quote "Ce que l'exercice doit faire comprendre"
        Il n'y a pas de bonne réponse évidente. L'option la plus souveraine (A) est aussi la plus fragile techniquement ; l'option la plus commode (C) est la moins maîtrisée.

        **La souveraineté a un coût.** Le débat public porte précisément sur qui doit le payer, et jusqu'où.

## <span style="color:#1565c0">La neutralité du réseau</span>

!!! info "Le principe"
    La **neutralité du réseau** est l'idée qu'un opérateur doit transporter tous les paquets **de la même façon**, sans favoriser ni ralentir un service selon son origine, sa destination ou son contenu.

    Un paquet est un paquet : le réseau le transporte sans regarder ce qu'il contient.

!!! example "Activité 3 — Trois scénarios"
    La neutralité est-elle respectée dans chacun de ces cas ?

    1. Un opérateur ralentit toutes les vidéos en période de saturation du réseau.
    2. Un opérateur ralentit **une seule** plateforme vidéo, avec laquelle il est en concurrence.
    3. Un opérateur propose un forfait où une plateforme précise ne compte pas dans le volume de données.

??? success "Corrigé"
    1. **Neutralité respectée**, à première vue : la règle s'applique à tous les services de même nature, sans discrimination par origine. La gestion de la congestion est admise si elle est transparente et non discriminatoire.
    2. **Violation claire.** L'opérateur avantage son propre service en dégradant celui d'un concurrent. C'est le cas d'école de ce que la neutralité interdit.
    3. **Le cas discuté.** Techniquement, aucun ralentissement. Mais la gratuité pour une plateforme donnée oriente fortement les usages et **désavantage tout nouvel entrant**. Ces offres ont été contestées en Europe et plusieurs ont été jugées non conformes.

    !!! tip "Pourquoi c'est un enjeu démocratique"
        Sans neutralité, l'accès à un service dépendrait des accords commerciaux de ton opérateur. Un nouveau service, une association, un média indépendant partiraient avec un handicap structurel.

        La neutralité est ce qui a permis à des services nouveaux d'émerger sans autorisation préalable — le Web lui-même en est le meilleur exemple.

## <span style="color:#1565c0">Les formats ouverts, encore</span>

!!! success "Le fil de l'année"
    Ce point est revenu trois fois, et ce n'est pas un hasard.

    - Module *Les données* : le **CSV** survit parce que personne ne le contrôle.
    - Ce module, bloc B : le **Web** s'est imposé parce que ses spécifications étaient publiques et libres de droits.
    - Ici : la capacité à **partir** dépend entièrement du format dans lequel tes données sont enfermées.

!!! info "La question à poser avant de s'engager"
    Trois questions, à poser à tout service — et que peu de gens posent avant de s'inscrire :

    1. **Puis-je récupérer mes données ?** Le RGPD garantit un droit à la portabilité.
    2. **Dans quel format ?** Un export dans un format propriétaire illisible ailleurs ne sert à rien.
    3. **Que se passe-t-il si le service ferme ?** Ou change ses tarifs, ou modifie ses conditions ?

!!! quote "Ce qui fait la dépendance"
    Ce n'est pas d'utiliser un service. C'est de **ne pas pouvoir en sortir**.

    Un service qu'on peut quitter en emportant ses données reste un choix. Un service qu'on ne peut plus quitter est devenu une contrainte.

## <span style="color:#1565c0">Ce qu'on peut faire</span>

!!! success "À l'échelle individuelle"
    - Préférer les **formats ouverts** quand le choix existe.
    - Vérifier qu'un service permet l'**export** de ses données avant de s'y installer.
    - Ne pas mettre toutes ses données chez un seul acteur.
    - **Garder son matériel plus longtemps** — c'est aussi une réduction de dépendance, pas seulement un geste écologique.

!!! success "À l'échelle collective"
    Ces choix se décident aussi par la loi et par les politiques publiques : règles européennes sur les transferts de données, obligations d'interopérabilité, soutien aux hébergeurs européens, exigences de transparence imposées aux grandes plateformes.

    !!! quote "Le point important"
        Ces sujets se décident **en ce moment**, et ils sont débattus. Ce sont des questions politiques, sur lesquelles il existe des positions différentes et légitimes.

        Le rôle de ce cours n'est pas de te dire laquelle choisir. C'est de te donner de quoi comprendre de quoi on parle — parce qu'on ne peut pas se prononcer sur ce qu'on ne comprend pas.

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. Internet est décentralisé. Pourquoi cela n'empêche-t-il pas la concentration du pouvoir ?
    2. De quel droit relève une donnée stockée à l'étranger ?
    3. Qu'est-ce que la neutralité du réseau ?
    4. Pourquoi une offre « données illimitées sur une plateforme » pose-t-elle problème ?
    5. Quelles trois questions poser avant de confier ses données à un service ?
    6. Qu'est-ce qui crée réellement la dépendance à un service ?

??? success "Réponses"
    1. Parce que la décentralisation est **technique** — le routage — alors que la concentration est **économique** : câbles, centres de données et services principaux appartiennent à un petit nombre d'acteurs.
    2. Du droit du pays où se trouve le serveur, **et** du droit applicable à l'entreprise qui l'exploite — qui peuvent être incompatibles avec le droit européen.
    3. L'obligation de transporter tous les paquets de la même façon, sans discriminer selon l'origine, la destination ou le contenu.
    4. Parce qu'elle oriente les usages et **désavantage les nouveaux entrants**, même sans ralentir techniquement quoi que ce soit.
    5. Puis-je récupérer mes données ? Dans quel format ? Que se passe-t-il si le service ferme ou change ?
    6. Non pas l'usage, mais l'**impossibilité de partir** en emportant ses données.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc D"
    - Internet est décentralisé **techniquement**, concentré **économiquement**.
    - Une donnée relève du droit du lieu où elle est stockée et de l'entreprise qui l'exploite.
    - La **neutralité du réseau** garantit qu'un opérateur ne favorise aucun service — condition d'apparition de nouveaux acteurs.
    - Un **format ouvert** est ce qui permet de partir : c'est le fil qui relie CSV, le Web et la portabilité.
    - La dépendance ne vient pas de l'usage, mais de l'**impossibilité de sortir**.
    - La souveraineté a un **coût** : c'est ce qui rend le débat politique, et non technique.

!!! abstract "Et maintenant ?"
    Tu sais où sont les données, par où elles passent, qui possède les infrastructures et ce que tout cela consomme.

    Il reste le module qui récupère tout : **l'intelligence artificielle**. Les données et leurs biais, les images générées, la recommandation, les centres de données — tout ce que tu as vu cette année y converge.

