---
author: Elisabeth Le Prettre (LePrettre)
title: 04d Désinformation, droit
---

# Bloc D — Désinformation, droit et responsabilité

!!! abstract "Au programme"
    Viralité · bulles de filtre · contenus générés · vérifier une information · droit en ligne et cyberharcèlement

!!! info "Séances 5 et 6"
    Séance 5 : pourquoi le faux circule vite. Séance 6 : droit et responsabilité.

## <span style="color:#1565c0">La mécanique de la viralité</span>

Au bloc A, on a vu qu'une information **saute** d'un groupe à l'autre dès qu'elle atteint une personne très connectée. Mettons un chiffre là-dessus.

!!! question "À toi de jouer D.1 ⭐⭐"
    Une personne publie une information. Chaque personne qui la reçoit la partage à **3 personnes** qui ne l'avaient pas encore vue.

    Écris un programme qui affiche, tour par tour, le nombre de nouvelles personnes touchées et le total cumulé. Va jusqu'au tour 8.

??? success "Corrigé"
    ```python
    def propagation(k, tours):
        total = 1
        nouveaux = 1
        for tour in range(tours):
            nouveaux = nouveaux * k
            total = total + nouveaux
            print("Tour", tour + 1, ":", nouveaux, "nouvelles personnes, total", total)
        return total


    propagation(3, 8)
    ```

    ```text
    Tour 1 : 3 nouvelles personnes, total 4
    Tour 2 : 9 nouvelles personnes, total 13
    Tour 3 : 27 nouvelles personnes, total 40
    Tour 4 : 81 nouvelles personnes, total 121
    Tour 5 : 243 nouvelles personnes, total 364
    Tour 6 : 729 nouvelles personnes, total 1093
    Tour 7 : 2187 nouvelles personnes, total 3280
    Tour 8 : 6561 nouvelles personnes, total 9841
    ```

    !!! success "Presque 10 000 personnes en 8 tours"
        Tu reconnais cette courbe : c'est la **croissance exponentielle** du pliage de feuille en M0, et de la consommation du centre de données.

        Même mécanisme, autre contexte. C'est pourquoi la pensée algorithmique sert au-delà de la programmation.

!!! question "À toi de jouer D.2 ⭐⭐ — Le démenti"
    Une information fausse est publiée. Elle se partage à 3. Un démenti est publié **deux tours plus tard**, et il ne se partage qu'à 2 — un démenti intéresse moins.

    Au bout de 8 tours au total, combien de personnes ont vu chacun ?

??? success "Corrigé"
    ```python
    def total_touche(k, tours):
        total = 1
        nouveaux = 1
        for tour in range(tours):
            nouveaux = nouveaux * k
            total = total + nouveaux
        return total


    print("Fausse info (8 tours, k=3) :", total_touche(3, 8))
    print("Démenti    (6 tours, k=2) :", total_touche(2, 6))
    ```

    ```text
    Fausse info (8 tours, k=3) : 9841
    Démenti    (6 tours, k=2) : 127
    ```

    !!! danger "Le rapport est de 1 à 77"
        Le démenti touche **127 personnes**, la fausse information **9841**.

        Deux causes se cumulent : il part plus tard, et il se partage moins. Aucune des deux n'est corrigeable par une bonne volonté individuelle.

    !!! quote "Ce qu'il faut en tirer"
        Corriger une fausse information après coup ne fonctionne pas. La seule intervention efficace se situe **avant le partage**.

        D'où la règle : vérifier avant de partager, pas après.

## <span style="color:#1565c0">Pourquoi le faux circule mieux</span>

Ce n'est pas seulement une question de vitesse. Une information fausse a souvent des **caractéristiques** qui la font partager davantage.

| Une information vraie | Une information fausse |
| --- | --- |
| doit respecter les faits | est libre de dire ce qui plaira |
| est souvent nuancée | est nette, tranchée |
| est parfois ennuyeuse | est conçue pour surprendre |
| prend du temps à vérifier | est disponible immédiatement |

!!! danger "L'effet du bloc B"
    Souviens-toi : un algorithme qui **optimise l'engagement** met en avant ce qui fait réagir.

    Or le faux, précisément parce qu'il est libre d'être surprenant et tranché, fait réagir davantage. **La plateforme n'a pas besoin de vouloir diffuser le faux pour le diffuser** : il suffit qu'elle optimise les réactions.

## <span style="color:#1565c0">Bulles de filtre et chambres d'écho</span>

!!! info "Deux phénomènes proches, à distinguer"
    - Une **bulle de filtre** est produite par l'algorithme : il te montre ce qui te ressemble, donc tu vois de moins en moins autre chose.
    - Une **chambre d'écho** est produite par tes propres choix : tu suis des personnes qui pensent comme toi, tu bloques celles qui te contredisent.

    L'une vient du système, l'autre de nous. Elles se renforcent mutuellement.

!!! example "Activité 1 — Le retour du graphe"
    Reprends la fonction `suggestions()` du bloc B. Pour Camille, elle recommande Sarah — avec qui elle partage **trois** amis.

    1. Si Camille accepte, que devient la structure du réseau autour d'elle ?
    2. Quelle personne l'algorithme ne lui recommandera **jamais** ?
    3. Que faudrait-il changer pour ouvrir son réseau ?

??? success "Corrigé"
    1. Le groupe Camille–Lou–Mohamed–Sarah–Ines se **referme** : presque tout le monde y est relié à tout le monde. L'information y circule vite, mais elle y tourne en rond.
    2. **Jade, Gabriel et Noah** — aucun ami commun avec Camille, donc jamais suggérés. L'algorithme ne peut pas proposer ce qui est loin, puisqu'il mesure la proximité.
    3. Il faudrait un critère **opposé** : recommander précisément des personnes éloignées dans le graphe. Aucune plateforme ne le fait, parce que ces suggestions seraient moins souvent acceptées — donc moins bonnes selon le critère qu'elle optimise.

    !!! quote "Le cœur du problème"
        La bulle de filtre n'est pas un dysfonctionnement. C'est le **fonctionnement normal** d'un système qui recommande ce qui a le plus de chances d'être accepté.

## <span style="color:#1565c0">Les contenus générés</span>

Il est désormais possible de produire en quelques secondes un texte, une image, une voix ou une vidéo synthétiques.

!!! danger "Ce que ça change concrètement"
    - **Le volume** : une seule personne peut produire des milliers de messages qui semblent venir de milliers de personnes différentes.
    - **La preuve** : une photo ou un enregistrement ne prouve plus grand-chose à lui seul.
    - **Le doute généralisé** : le risque n'est pas seulement de croire au faux, c'est de ne plus croire au vrai. Un document authentique peut désormais être écarté d'un « c'est une IA ».

!!! quote "Le lien avec M0"
    Dans le bloc D de M0, tu as vérifié trois codes produits par une IA. Les trois étaient faux, aucun ne plantait, tous paraissaient crédibles.

    C'est exactement le même problème, transposé à l'information : **ce qui est plausible n'est pas ce qui est vrai**, et la forme ne dit rien du contenu.

!!! example "Activité 2 — Les signaux d'alerte"
    Quels indices peuvent faire soupçonner un contenu synthétique ou une opération coordonnée ?

??? success "Corrigé"
    Sur le **contenu** : incohérences dans les détails (mains, textes en arrière-plan, reflets), formulations lisses et sans aspérités, absence de sources vérifiables.

    Sur le **compte** : création récente, très forte activité, peu d'abonnés mais beaucoup de publications, absence d'historique personnel.

    Sur la **diffusion** : plusieurs comptes publiant le même texte au même moment, réponses génériques et hors sujet.

    !!! warning "Aucun de ces signaux n'est une preuve"
        Un compte récent peut être sincère ; une image imparfaite peut être authentique. Ces indices invitent à **vérifier**, ils ne concluent pas.

        Et les défauts visuels disparaissent vite : ce qui était détectable il y a un an ne l'est plus. **La vérification par la source restera toujours plus fiable que la vérification par l'apparence.**

## <span style="color:#1565c0">Vérifier une information</span>

!!! success "La méthode, en quatre questions"
    **1. Qui le dit ?** Remonter à la source première, pas au compte qui l'a relayée. Un site d'apparence sérieuse n'est pas une source.

    **2. Quand ?** Une information vraie mais ancienne, republiée hors contexte, est un des procédés les plus courants — et les plus efficaces.

    **3. Est-ce confirmé ailleurs ?** Par des sources **indépendantes** entre elles. Dix sites qui se recopient ne font qu'une seule source.

    **4. Qu'est-ce que ça me fait ressentir ?** Un contenu qui provoque immédiatement de la colère ou de l'indignation est conçu pour être partagé sans réflexion. **Cette réaction est un signal d'alerte, pas une confirmation.**

!!! tip "Le geste le plus efficace"
    Attendre. Le partage immédiat est ce qui donne sa puissance à la désinformation ; quelques minutes suffisent le plus souvent à voir apparaître une confirmation ou un démenti.

## <span style="color:#1565c0">Le droit ne s'arrête pas en ligne</span>

!!! info "Séance 6"

!!! warning "Le principe"
    Ce qui est interdit hors ligne l'est également en ligne. Un réseau social n'est pas un espace sans droit, et l'anonymat apparent n'est qu'apparent : les autorités judiciaires peuvent obtenir l'identité derrière un compte.

Quelques repères, non exhaustifs :

| Comportement | Statut |
| --- | --- |
| Injure, diffamation | Infraction, en ligne comme ailleurs |
| **Cyberharcèlement** | Délit, y compris quand chaque message pris isolément paraît anodin |
| Publier l'image d'une personne sans son accord | Atteinte au droit à l'image |
| Diffuser des contenus intimes sans consentement | Délit spécifiquement réprimé |
| Usurper l'identité de quelqu'un | Délit |
| Republier une œuvre sans autorisation | Contrefaçon |

!!! danger "Ce qui est propre au cyberharcèlement"
    La loi prévoit explicitement le cas où **plusieurs personnes** envoient chacune un seul message. Chacune peut se dire qu'elle n'a rien fait de grave ; l'effet cumulé constitue pourtant le harcèlement, et la responsabilité est individuelle.

    Trois autres particularités par rapport au harcèlement hors ligne :

    - il ne s'arrête pas à la sortie de l'établissement ;
    - les contenus restent et peuvent ressurgir des années plus tard ;
    - le public est potentiellement illimité.

!!! success "Que faire — pour soi ou pour quelqu'un d'autre"
    - **Ne pas répondre** : la réponse alimente le mécanisme.
    - **Conserver les preuves** : captures d'écran datées, avant toute suppression.
    - **Signaler** sur la plateforme, et **en parler à un adulte** : un parent, un professeur, l'infirmerie, la vie scolaire.
    - Des **numéros d'aide nationaux** existent, gratuits et confidentiels ; ton établissement peut te les indiquer.
    - **Ne pas rester témoin passif.** Un témoin qui soutient la personne visée change souvent le cours des choses.

!!! quote "Sur la responsabilité de témoin"
    Partager, liker ou même simplement regarder un contenu qui humilie quelqu'un contribue à sa diffusion — les blocs B et D l'ont montré chiffres à l'appui.

    Ne rien faire n'est pas neutre : c'est participer à la mécanique.

## <span style="color:#1565c0">La modération</span>

!!! example "Activité 3 — Le dilemme"
    Une plateforme reçoit des millions de signalements par jour. Elle doit décider quoi retirer.

    1. Pourquoi ne peut-elle pas faire examiner chaque cas par un humain ?
    2. Quels risques si elle confie tout à un système automatique ?
    3. Qui devrait décider de ce qui est acceptable ?

??? success "Pistes de corrigé"
    1. **Le volume.** Des millions de contenus par jour rendent l'examen humain systématique impossible. La modération automatique est donc une nécessité pratique, pas un choix idéologique.
    2. Un système automatique reproduit les **biais** de ses données d'entraînement — on l'a vu en M1. Il ne comprend ni l'ironie, ni le contexte, ni les usages locaux. Il retire des contenus légitimes et laisse passer des contenus problématiques. Et il n'explique pas ses décisions.
    3. **C'est une question politique, pas technique.** Faut-il laisser une entreprise privée fixer les limites de ce qui peut se dire ? Les États ? Un organisme indépendant ? Les réponses varient selon les pays et font l'objet de débats en cours.

    !!! note "Un repère"
        L'Union européenne a adopté un règlement imposant aux grandes plateformes des obligations de transparence sur leurs systèmes de modération et de recommandation, ainsi que des voies de recours pour les utilisateurs.

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. Pourquoi un démenti touche-t-il beaucoup moins de monde que l'information fausse ?
    2. Quelle différence entre une bulle de filtre et une chambre d'écho ?
    3. Pourquoi une plateforme qui optimise l'engagement diffuse-t-elle le faux sans le vouloir ?
    4. Quelles sont les quatre questions à se poser avant de partager ?
    5. Pourquoi le cyberharcèlement engage-t-il la responsabilité de chacun, même pour un seul message ?

??? success "Réponses"
    1. Deux causes cumulées : il part **plus tard** et se partage **moins**. Sur nos calculs, 127 personnes contre 9841.
    2. La bulle de filtre est produite par **l'algorithme** ; la chambre d'écho par **nos propres choix**. Elles se renforcent.
    3. Parce que le faux, libre d'être tranché et surprenant, fait davantage réagir. Optimiser les réactions revient à favoriser ce qui en produit.
    4. Qui le dit ? Quand ? Est-ce confirmé par des sources indépendantes ? Qu'est-ce que ça me fait ressentir ?
    5. Parce que la loi prévoit le cas de messages émanant de plusieurs personnes : l'effet cumulé constitue le harcèlement, et chacun répond de sa contribution.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc D"
    - La propagation est **exponentielle** : 8 tours de partage à 3 touchent près de 10 000 personnes.
    - Un démenti arrive trop tard et circule moins : corriger après ne fonctionne pas.
    - Le faux circule mieux parce qu'il est **libre d'être surprenant** — et qu'un algorithme d'engagement le favorise mécaniquement.
    - Les contenus générés changent l'échelle du problème et fragilisent la valeur de preuve d'une image.
    - Vérifier : **qui, quand, confirmé ailleurs, et que me fait ressentir ce contenu ?**
    - Le droit s'applique en ligne. Le cyberharcèlement engage la responsabilité de **chaque** contributeur.

!!! abstract "Et maintenant ?"
    Tu sais comment les plateformes ordonnent ce que tu vois. Reste la question laissée ouverte au début du module : **où sont physiquement stockées tes publications ?**

    C'est l'objet du module *Internet et le Web*.

