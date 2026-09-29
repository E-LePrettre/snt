---
author: Elisabeth Le Prettre (LePrettre)
title: 06a Apprendre
---

# Bloc A — Qu'est-ce qu'apprendre ?

!!! abstract "Au programme"
    Programmer une règle · apprendre d'exemples · les grandes familles d'IA · ce que « intelligence » veut dire, et ne veut pas dire

!!! info "Séance 1"
    La question fondatrice du module : comment une machine peut-elle « apprendre » quelque chose qu'on ne lui a pas explicitement programmé ?

## <span style="color:#1565c0">Deux façons de résoudre un problème</span>

Prenons une tâche concrète : distinguer une **pomme** d'une **orange** à partir de deux mesures — sa masse et la rugosité de sa peau.

### <span style="color:#2e7d32">Première façon : écrire la règle</span>

C'est ce que tu fais depuis M0. Tu réfléchis, tu trouves une règle, tu la programmes :

```python
def classer(masse, rugosite):
    if rugosite >= 5:
        return "orange"
    else:
        return "pomme"
```

!!! info "Ce qui caractérise cette approche"
    **C'est toi qui apportes la connaissance.** Tu as observé que les oranges ont la peau plus rugueuse, et tu as écrit cette observation sous forme de règle.

    Le programme n'a rien appris : il applique ce que tu sais déjà. C'est de la programmation classique — celle de toute l'année.

### <span style="color:#2e7d32">Deuxième façon : montrer des exemples</span>

L'autre approche est radicalement différente. **Tu n'écris aucune règle.** Tu donnes seulement des exemples déjà étiquetés :

```python
# [masse, rugosité, étiquette]
exemples = [
 [150, 7, "orange"], [170, 8, "orange"], [140, 6, "orange"],
 [130, 2, "pomme"],  [145, 3, "pomme"],  [120, 1, "pomme"]]
```

Et tu laisses le programme **trouver tout seul** comment séparer les deux.

!!! quote "La différence fondamentale"
    - Programmation classique : **humain → règle → machine applique.**
    - Apprentissage automatique : **humain → exemples → machine trouve la règle.**

    C'est cela, l'« apprentissage » d'une machine : découvrir une régularité dans des exemples, sans qu'on la lui ait dictée.

    Le terme technique est **apprentissage automatique** (*machine learning*).

## <span style="color:#1565c0">Pourquoi ne pas toujours écrire la règle ?</span>

Si on peut écrire la règle, pourquoi s'en priver ? Parce que pour beaucoup de tâches, **personne ne sait l'écrire.**

!!! example "Activité 1 — Écris la règle"
    Essaie d'écrire, en français, la règle qui permet de reconnaître :

    1. un chiffre `7` manuscrit ;
    2. la voix de ton meilleur ami parmi d'autres ;
    3. un chat sur une photo.

??? success "Corrigé"
    Tu n'y arrives pas — et c'est normal. Personne n'y arrive.

    Tu **reconnais** un 7, une voix, un chat instantanément. Mais tu es incapable d'écrire la règle qui le décide : où commence un 7, qu'est-ce qui fait qu'une voix est celle-ci et pas une autre, quels pixels font un chat.

    !!! tip "La leçon"
        Il existe des tâches que l'on sait **faire** sans savoir **expliquer**. Pour celles-là, écrire une règle est impossible — mais on peut fournir des milliers d'exemples.

        C'est précisément le domaine où l'apprentissage automatique est utile, et c'est pourquoi il a pris tant d'importance : la reconnaissance d'images, de sons, de langage.

!!! warning "Le revers de la médaille"
    Quand une machine apprend d'exemples au lieu d'appliquer une règle écrite, **personne ne peut expliquer précisément sa décision**.

    On l'a déjà rencontré deux fois cette année :

    - le fil d'actualité des réseaux sociaux, dont les coefficients sont appris et non écrits ;
    - le code produit par une IA en M0, qu'on ne pouvait juger qu'en le testant.

    Un système qui apprend gagne en capacité ce qu'il perd en **transparence**. C'est un compromis, pas un progrès pur.

## <span style="color:#1565c0">Les grandes familles</span>

« Intelligence artificielle » est un terme large. Voici les repères utiles, sans entrer dans la technique.

| Approche | Principe | Exemple |
| --- | --- | --- |
| **Systèmes à règles** | des règles écrites par des humains | un logiciel de calcul d'impôts |
| **Apprentissage supervisé** | apprendre d'exemples **étiquetés** | reconnaître une pomme d'une orange |
| **Apprentissage non supervisé** | trouver des groupes **sans étiquettes** | regrouper des clients par comportement |
| **IA générative** | produire du contenu plausible | générer un texte, une image |

!!! info "Ce module se concentre sur deux d'entre elles"
    - l'**apprentissage supervisé** (blocs B et C) : le plus simple à comprendre, et celui que tu vas coder ;
    - l'**IA générative** (bloc D) : celle que tu utilises déjà, et qu'il faut démystifier.

## <span style="color:#1565c0">Le mot « intelligence » est trompeur</span>

!!! quote "Une mise au point nécessaire"
    Le mot « intelligence artificielle » date des années 1950. Il a été choisi en partie pour attirer l'attention et des financements. Beaucoup de chercheurs le regrettent, car il suggère des capacités que ces systèmes n'ont pas.

    Un système d'apprentissage **ne comprend pas**, **ne raisonne pas** au sens où tu le fais, **ne veut rien**. Il détecte des régularités statistiques dans des données et les applique.

!!! example "Activité 2 — Intelligent ?"
    Pour chacun de ces systèmes, discute : mérite-t-il le mot « intelligent » ?

    1. Une calculatrice qui donne la racine carrée en une milliseconde.
    2. Un programme qui bat le champion du monde d'échecs.
    3. Un système qui décrit le contenu d'une photo en une phrase.

??? success "Pistes de discussion"
    1. Personne ne dirait qu'une calculatrice est intelligente — pourtant elle fait en un instant ce qu'aucun humain ne fait de tête. **La rapidité de calcul n'est pas l'intelligence.**
    2. Longtemps considéré comme le sommet de l'intelligence, jouer aux échecs se fait aujourd'hui par exploration de coups et évaluation. On a cessé de trouver ça « intelligent » dès qu'on a su comment le faire.
    3. Impressionnant — mais le système a appris à associer des images à des mots à partir de millions d'exemples. Il **décrit** sans **comprendre** ce qu'est la scène.

    !!! tip "Le paradoxe de l'IA"
        Dès qu'on comprend comment une machine accomplit une tâche, on cesse de trouver ça « intelligent ». Ce qui reste appelé « intelligence » est toujours **ce qu'on ne sait pas encore expliquer**.

        C'est un bon réflexe critique : quand on te dit qu'un système « comprend » ou « pense », demande *comment il fait*. La réponse est toujours plus modeste que le mot employé.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc A"
    - Deux approches : **écrire la règle** (programmation classique) ou **montrer des exemples** (apprentissage automatique).
    - On recourt à l'apprentissage pour les tâches qu'on sait **faire sans savoir expliquer** — images, sons, langage.
    - Un système qui apprend gagne en capacité ce qu'il perd en **transparence** : sa décision n'est plus explicable.
    - Une machine qui « apprend » ne comprend pas et ne veut rien : elle détecte des **régularités**.
    - Dès qu'on sait comment une tâche est faite, on cesse de l'appeler « intelligente ».

