---
author: Elisabeth Le Prettre (LePrettre)
title: 02a Qu'est ce qu'une donnée ?
---

# Bloc A — Qu'est-ce qu'une donnée ?

!!! abstract "Au programme"
    Donnée et information · types · tableaux et tables · les formats CSV et JSON · modéliser

!!! info "Séance 1"
    Ce qu'est une donnée, comment on la structure, dans quels formats on l'échange.

## <span style="color:#1565c0">Donnée, information, connaissance</span>

Trois mots qu'on confond souvent, et qu'il faut distinguer.

| Mot | Ce que c'est | Exemple |
| --- | --- | --- |
| **Donnée** | Une valeur brute, sans contexte | `18` |
| **Information** | La donnée mise en contexte | *il fait 18 °C à Mont-de-Marsan* |
| **Connaissance** | Ce qu'on en déduit | *c'est doux pour un mois de février* |

!!! quote "Le point à retenir"
    Une donnée toute seule ne veut **rien dire**. `18`, c'est peut-être une température, un âge, une note, un numéro de département. C'est le **contexte** — le nom de la colonne, l'unité, la source — qui la rend interprétable.

    Retiens-le : chaque fois qu'on te montre un chiffre sans son contexte, on te demande de croire sans pouvoir vérifier.

## <span style="color:#1565c0">Les types de données</span>

Tu les connais déjà, tu les as manipulés en M0.

| Type | Nom en Python | Exemple | Sert à |
| --- | --- | --- | --- |
| Entier | `int` | `18` | compter, mesurer |
| Décimal | `float` | `18.5` | mesurer finement |
| Texte | `str` | `"Mont-de-Marsan"` | nommer, décrire |
| Booléen | `bool` | `True` | répondre par oui ou non |

!!! example "Activité 1 — Choisir le bon type"
    Pour chacune de ces informations, quel type choisirais-tu ? Justifie.

    1. Le nombre d'élèves d'une classe
    2. La température relevée à midi
    3. Un code postal
    4. Un numéro de téléphone
    5. « L'élève est-il inscrit à la cantine ? »
    6. Le prix d'un article

??? success "Corrigé"
    1. `int` — on compte des élèves entiers.
    2. `float` — 18,5 °C a du sens.
    3. **`str`** — et c'est un piège. Un code postal ressemble à un nombre, mais on n'en fait jamais la moyenne. Surtout, `01000` (Bourg-en-Bresse) perdrait son zéro initial en `int`.
    4. **`str`**, pour la même raison — c'est déjà ce qu'on avait vu en M0.
    5. `bool` — la réponse est oui ou non.
    6. `float` — 12,90 €.

    !!! tip "La règle"
        Le type ne dépend pas de l'**apparence** de la donnée, mais de son **usage**. Si tu ne fais jamais de calcul avec, ce n'est pas un nombre.

        C'est un premier acte de **modélisation** : décider comment représenter le réel dans une machine.

## <span style="color:#1565c0">Organiser : la table</span>

Une donnée isolée sert rarement. On les regroupe en **table** (ou tableau de données) :

| prenom | maths | francais | ecran |
| --- | --- | --- | --- |
| Camille | 12 | 14 | 180 |
| Lou | 8 | 11 | 240 |
| Mohamed | 15 | 13 | 90 |

Le vocabulaire compte :

- une **ligne** (ou *enregistrement*) décrit **un individu** — ici, un élève ;
- une **colonne** (ou *descripteur*, *attribut*) décrit **une même caractéristique** pour tous ;
- la première ligne, les **en-têtes**, donne le nom de chaque colonne.

!!! example "Activité 2 — Lire une table"
    En regardant la table ci-dessus :

    1. Combien d'individus ? Combien de descripteurs ?
    2. Que vaut le descripteur `ecran` pour Mohamed ?
    3. La colonne `ecran` contient `180`. Cette donnée est-elle interprétable telle quelle ?

??? success "Corrigé"
    1. 3 individus, 4 descripteurs.
    2. 90.
    3. **Non.** 180 quoi ? Des minutes ? Par jour, par semaine ? Sur quel appareil ? Mesuré comment — déclaré par l'élève, ou relevé par le téléphone ?

    Sans ces précisions, la colonne est inutilisable. On appelle ces informations sur les données des **métadonnées** : elles disent ce que les données signifient.

    !!! warning "L'erreur la plus fréquente"
        Utiliser un jeu de données sans savoir **comment il a été construit**. C'est la source d'erreur numéro un du traitement de données — bien avant les erreurs de programmation.

## <span style="color:#1565c0">Le format CSV</span>

Pour échanger des tables entre logiciels, on utilise un format simple : le **CSV** (*Comma-Separated Values*, valeurs séparées par des virgules).

```text
prenom,maths,francais,ecran
Camille,12,14,180
Lou,8,11,240
Mohamed,15,13,90
```

Ses règles tiennent en trois lignes :

- une **ligne de texte** par individu ;
- les valeurs séparées par un **séparateur**, souvent la virgule ou le point-virgule ;
- la **première ligne** contient les en-têtes.

!!! tip "Pourquoi ce format a survécu à tout"
    Il est lisible par un humain avec un simple éditeur de texte, il ne dépend d'aucun logiciel, et il n'appartient à personne. Un fichier CSV de 1985 s'ouvre encore aujourd'hui.

    C'est l'inverse d'un format propriétaire, qui devient illisible le jour où l'entreprise qui l'a créé disparaît ou change ses règles.

!!! warning "Le piège du séparateur"
    En France, le tableur utilise souvent le **point-virgule**, parce que la virgule sert déjà de séparateur décimal (`18,5`). Un fichier CSV mal lu affiche tout dans une seule colonne : c'est presque toujours une histoire de séparateur.

## <span style="color:#1565c0">Le format JSON</span>

Le CSV convient aux tables régulières. Quand les données ont une structure plus riche — des éléments imbriqués, des champs absents chez certains — on utilise le **JSON**.

```json
{
  "ville": "Mont-de-Marsan",
  "temperature": 18.5,
  "humidite": 72,
  "capteur": {
    "identifiant": "MDM-04",
    "altitude": 62
  }
}
```

Les règles :

- des couples **`"nom": valeur`**, séparés par des virgules ;
- des **accolades** `{ }` pour regrouper ;
- des **crochets** `[ ]` pour une liste ;
- les noms sont toujours entre guillemets.

!!! example "Activité 3 — Lire du JSON"
    ```json
    {
      "classe": "2nde 4",
      "effectif": 28,
      "options": ["SNT", "Arts plastiques"],
      "professeur_principal": {
        "matiere": "physique-chimie"
      }
    }
    ```

    1. Combien d'élèves ?
    2. Combien d'options, et lesquelles ?
    3. Quelle est la matière du professeur principal ?

??? success "Corrigé"
    1. 28.
    2. Deux : SNT et Arts plastiques. Les crochets signalent une **liste**.
    3. Physique-chimie. La valeur de `professeur_principal` est elle-même un objet, avec ses propres champs : c'est ce qu'on appelle une structure **imbriquée**.

!!! info "Quand utilise-t-on l'un ou l'autre ?"
    | | CSV | JSON |
    | --- | --- | --- |
    | Structure | table régulière | structure libre, imbriquée |
    | Lisibilité humaine | très bonne | bonne |
    | Usage typique | export d'un tableur, données ouvertes | échanges entre programmes, **API** |

    Une **API** est un service qui répond à une requête d'un programme. La plupart répondent en JSON — on en manipulera au bloc B.

## <span style="color:#1565c0">Les données ouvertes</span>

De nombreuses données publiques sont mises à disposition de tous, gratuitement et réutilisables : population, qualité de l'air, résultats électoraux, horaires de transports, relevés météo.

C'est ce qu'on appelle l'**open data**. En France, l'État publie ces jeux sur un portail public, et la loi impose à de nombreuses administrations de le faire.

!!! quote "Pourquoi c'est un enjeu démocratique"
    Si les données publiques sont accessibles, n'importe qui — un journaliste, une association, un élève — peut vérifier une affirmation par lui-même.

    Si elles ne le sont pas, il faut croire sur parole celui qui les détient.

!!! question "À toi de jouer A.1 ⭐ — Décrire un jeu de données"
    Choisis un sujet qui t'intéresse (le sport, la musique, le climat, les jeux vidéo). Décris en quelques lignes la table que tu construirais :

    - quel est l'individu représenté par une ligne ?
    - quels descripteurs, et de quel type chacun ?
    - où trouverais-tu ces données ?

??? success "Un exemple de réponse"
    **Sujet : les stations de vélos en libre-service d'une ville.**

    - Un individu = une station.
    - Descripteurs : `nom` (`str`), `latitude` (`float`), `longitude` (`float`), `capacite` (`int`), `velos_disponibles` (`int`), `en_service` (`bool`).
    - Source : le portail open data de la ville, souvent via une API en JSON.

    Remarque : `velos_disponibles` change en permanence. Certaines données sont **statiques** (la capacité), d'autres **dynamiques**. Ce n'est pas la même chose à stocker ni à interpréter.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc A"
    - Une donnée seule ne signifie rien : c'est le **contexte** qui la rend interprétable.
    - Le **type** dépend de l'usage, pas de l'apparence : un code postal est du texte.
    - Une **table** : une ligne par individu, une colonne par descripteur.
    - **CSV** pour les tables régulières, **JSON** pour les structures imbriquées et les API.
    - Les **métadonnées** — comment les données ont été construites — comptent autant que les données.

