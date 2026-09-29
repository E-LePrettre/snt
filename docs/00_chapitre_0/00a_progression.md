---
author: Elisabeth Le Prettre (LePrettre)
title: 00 Progression
---

# Progression annuelle — SNT 



## Les modules

Six blocs, dans un ordre où chacun arme le suivant.

| # | Module |  Ce qu'il installe |
| --- | --- | --- | 
| **0** | Programmer : de la donnée à l'algorithme | La boîte à outils de toute l'année |
| **1** | Les données |  Structurer, traiter, protéger |
| **2** | Images numériques |  La donnée devient visuelle |
| **3** | Réseaux sociaux |  Graphes, recommandation, enjeux démocratiques |
| **4** | Internet et le Web |  L'infrastructure matérielle |
| **5** | Intelligence artificielle |  Les fondements, en héritant de tout le reste |





---


## 0 — Programmer : de la donnée à l'algorithme 

!!! abstract "Objectifs"
    Représenter une information · écrire un algorithme · traiter un jeu de données · porter un regard critique sur du code produit par une IA

| Séances | Bloc | Contenu |
| --- | --- | --- |
| 1 | **A — Représenter une donnée** | Variables, types, calculs, saisie et conversions, chaînes |
| 2 | **B — Écrire un algorithme** | Conditions, boucle `for`, boucle `while` |
| 3 | **C — Traiter un jeu de données** | Listes, fonctions, projet |
| 4 | **D — Programmer avec une IA** | Vérifier un code généré, biais, coût d'une requête, CRCN |

**Point IA :** le bloc D en entier. On reçoit trois codes « produits par une IA », tous faux, aucun ne plantant. Il faut déboguer avec ce qu'on vientd'apprendre.

**Entrée citoyenne :** anonymisation d'un prénom et ses limites (pseudonymisation ≠ anonymisation) · comprendre, tester et déclarer ce qu'on fait générer.

**Sortie attendue :** les fonctions `moyenne()`, `maximum()` et `nb_admis()`, réutilisées dès M1.





---

## 1 — Les données 

!!! abstract "Objectifs"
    Comprendre le rôle central des données : les structurer, les traiter, en mesurer la qualité, les protéger

| # | Séance | Contenu |
| --- | --- | --- |
| 1 | Qu'est-ce qu'une donnée | Types, tables, formats CSV et JSON. Modéliser : que représente une colonne ? |
| 2 | Traiter un fichier réel | Lire un CSV en Python. **Réinvestissement direct de `moyenne()` et `maximum()`** |
| 3 | Interroger | Filtrer, trier, compter. Notion d'API |
| 4 | Visualiser | Construire un graphique, et surtout **le lire de façon critique** |
| 5 | **Qualité et biais** | Données manquantes, non représentatives. *Point IA fort* |
| 6 | **Protéger** | Données personnelles, RGPD, souveraineté |

**Point IA (séance 5) :** une IA apprend *à partir de* données. Si le jeu d'entraînement est déséquilibré, le modèle l'est aussi. On le montre en comptant, pas en l'affirmant — l'activité du bloc D de M0 se prolonge ici sur un vrai jeu de données.

**Entrée citoyenne :** où sont hébergées mes données, qui peut les lire, que dit le RGPD. Reprise de la pseudonymisation vue en M0, cette fois avec l'appui juridique.

**Question suspendue posée ici :** *une donnée peut-elle être neutre ?*

---

## 2 — Images numériques 

!!! abstract "Objectifs"
    Comprendre ce qu'est une image pour une machine, et comment elle peut être fabriquée

| # | Séance | Contenu |
| --- | --- | --- |
| 1 | L'image est une donnée | Pixels, codage RGB, résolution. Manipulation pixel par pixel — **réinvestit les boucles** |
| 2 | De la prise de vue au fichier | Capteur, compression, **métadonnées EXIF** |
| 3 | Transformer une image | Filtres simples en Python : niveaux de gris, seuillage, négatif |
| 4 | **Images et IA générative** | Comment une image est générée ; détecter le synthétique. *Point IA fort* |

**Point IA (séances 3 et 4) :** le passage du filtre programmé — où l'on sait exactement ce qui se passe — à l'image générée, où on ne le sait plus. Ce contraste est l'entrée la plus concrète vers la notion de modèle génératif.

**Entrée citoyenne :** droit à l'image, deepfakes, droits d'auteur sur les images générées · ce que révèlent les métadonnées d'une photo publiée (séance 2 : une géolocalisation dans un fichier EXIF).

---

## 3 — Réseaux sociaux 

!!! abstract "Objectifs"
    Comprendre la mécanique des plateformes et les enjeux démocratiques et informationnels qu'elle soulève

| # | Séance | Contenu |
| --- | --- | --- |
| 1 | Modéliser un réseau | Graphes : sommets, arêtes, degré. Le graphe d'amitiés de la classe |
| 2 | Parcourir un graphe | Chemins, distance, effet petit monde |
| 3 | **La recommandation** | Comment un fil est ordonné, ce qui est optimisé. *Point IA fort* |
| 4 | Le modèle économique | Économie de l'attention, publicité ciblée, valeur des données |
| 5 | **Désinformation** | Viralité, bulles de filtre, contenus générés. *Point IA* |
| 6 | Droit et responsabilité | Cyberharcèlement, modération, responsabilité des plateformes |

**Point IA (séances 3 et 5) :** les systèmes de recommandation, et la circulation de contenus synthétiques — qui relie directement aux deepfakes vus en M2.

**Entrée citoyenne :** c'est le module le plus dense en EMI et EMC — vérifier une information, recouper les sources, connaître le droit applicable.

!!! quote "Question suspendue à poser ici, sans y répondre"
    *Où sont stockées tes publications, et qui décide de l'ordre de ton fil ?*

    M4 répondra pour la première moitié, M5 pour la seconde.

---

## 4 — Internet et le Web 

!!! abstract "Objectifs"
    Appréhender la réalité matérielle et les infrastructures du numérique

| # | Séance | Contenu |
| --- | --- | --- |
| 1 | Comment circule l'information | Client-serveur, adresses IP, paquets, routage |
| 2 | Du Net au Web | URL, HTTP, HTML ; fonctionnement d'une page |
| 3 | **La matière du numérique** | Câbles sous-marins, centres de données, coût énergétique. *Point IA* |
| 4 | Dépendances et souveraineté | Qui possède les infrastructures, neutralité du réseau |

**Point IA (séance 3) :** où « vit » un modèle. On reprend le calcul du coût d'une requête déjà fait dans le bloc D de M0, cette fois avec l'infrastructure sous les yeux.

**Entrée citoyenne :** la souveraineté numérique, posée ici concrètement (des câbles, des bâtiments, des entreprises) avant d'être reprise en M5 sous son angle politique.

---

## 5 — Intelligence artificielle 

!!! abstract "Objectifs"
    Poser les bases d'une compréhension scientifique et technique de l'IA, **sans technicité excessive**, et donner les clés d'un usage éclairé

| # | Séance | Contenu |
| --- | --- | --- |
| 1 | Qu'est-ce qu'apprendre ? | Apprendre à partir d'exemples plutôt que suivre des règles écrites. Repères historiques |
| 2 | **Classer** | Classification à partir d'exemples ; jeu d'entraînement et jeu de test |
| 3 | Atelier classification | Entraîner et tester un classifieur simple sur un jeu de données de classe |
| 4 | **Quand les données mentent** | Biais du jeu d'entraînement, sur-représentation. Reprise de M1 |
| 5 | Recommander et prédire | Comment un modèle apprend des préférences. **Réponse à la question suspendue de M3** |
| 6 | Générer du texte | Prédire le mot suivant ; limites, erreurs factuelles |
| 7 | Générer des images | Reprise de M2 ; détecter le synthétique |
| 8 | **Ce que ça coûte, ce que ça change** | Environnement, souveraineté, effets sur le travail et la création |
| 9 | **Usage éclairé — CRCN** | Formuler, vérifier, citer, déclarer. Droits d'auteur. Synthèse et projet |

!!! success "Le lien avec M0"
    Le bloc D de M0 avait posé ce qu'une IA **ne fait pas** : elle ne teste pas, ne vérifie pas, produit du plausible. M5 pose ce qu'elle **fait** : apprendre à partir de données, classer, recommander, générer.

    L'année boucle : les élèves reviennent avec des outils sur une question posée dès les premières séances.

**Entrée citoyenne :** dimensions éthiques, juridiques et environnementales, en articulation explicite avec l'EMC.

---


---

## Deux exigences transversales

!!! abstract "Mixité filles / garçons — un principe de conception, pas un chapitre"
    La saisine en fait un objectif explicite : *susciter chez les filles comme chez les garçons l'intérêt et la confiance nécessaires*.

    - **Figures citées** : Ada Lovelace et Grace Hopper (M0 et son bloc IA), et des parcours féminins dans l'ouverture métiers de M5.
    - **Contextes d'exercices** équilibrés : ni finance ni sport en majorité — création, données sociales, environnement.
    - **Temps dédié** : la clôture de M5 comporte une section « Les métiers du numérique sont pour tout le monde », donnant à voir une représentation équilibrée des femmes et des hommes, adressée aux filles comme aux garçons.
    - **Vigilance en classe** : qui tient le clavier en binôme, qui prend la parole en mise en commun.

!!! abstract "Actualisabilité"
    - Le programme fixe des **notions**, pas des outils. Python, Basthon et les plateformes citées sont des exemples remplaçables d'une année sur l'autre.
    - Chaque module peut accueillir une **capsule d'actualité** — un exemple récent, changé chaque année — sans que la structure bouge.
    - Les chiffres (coût énergétique, part des centres de données) sont donnés comme ordres de grandeur **à réactualiser**.
