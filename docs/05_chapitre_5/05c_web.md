---
author: Elisabeth Le Prettre (LePrettre)
title: 05b Web
---

# Bloc B — Du Net au Web

!!! abstract "Au programme"
    Internet ≠ Web · les trois piliers · décomposer une URL · le protocole HTTP · lire du HTML · les moteurs de recherche

!!! info "Séance 2"
    Internet est le réseau. Le Web est **une** des choses qu'on fait circuler dessus.

## <span style="color:#1565c0">Internet n'est pas le Web</span>

C'est la confusion la plus répandue, et elle empêche de comprendre le reste.

| | Internet | Le Web |
| --- | --- | --- |
| Ce que c'est | un **réseau** de machines | un **service** qui circule sur ce réseau |
| Apparu | années 1970 | 1989-1991 |
| Analogie | le réseau routier | le courrier livré par la route |

!!! info "Ce qui circule sur Internet en dehors du Web"
    Le courrier électronique, les messageries instantanées, les appels vidéo, les jeux en ligne, les mises à jour de logiciels, les objets connectés.

    Le Web n'est qu'un usage parmi d'autres — le plus visible, pas le seul. Internet lui est **antérieur d'une vingtaine d'années**.

!!! quote "L'invention du Web"
    Le Web a été conçu à la fin des années 1980 dans un laboratoire de recherche européen, pour permettre à des scientifiques de partager des documents reliés entre eux.

    Point décisif : ses spécifications ont été rendues **publiques et libres de droits**. N'importe qui pouvait créer un navigateur ou un serveur sans demander d'autorisation ni payer.

    C'est cette ouverture, plus que la technique, qui explique son adoption mondiale. À rapprocher de ce qu'on disait du format CSV au module *Les données* : un format ouvert que personne ne contrôle survit à ses créateurs.

## <span style="color:#1565c0">Les trois piliers</span>

| Pilier | Rôle | Exemple |
| --- | --- | --- |
| **URL** | adresser un document | `https://exemple.fr/page.html` |
| **HTTP** | transporter la demande et la réponse | `GET /page.html` |
| **HTML** | décrire le contenu du document | `<h1>Titre</h1>` |

Une adresse pour dire *quoi*, un protocole pour dire *comment on le demande*, un langage pour dire *ce que c'est*.

## <span style="color:#1565c0">Décomposer une URL</span>

```text
https://www.exemple.fr/cours/snt/internet.html?page=2
```

| Partie | Rôle |
| --- | --- |
| `https` | le **protocole** — le `s` signifie *sécurisé*, la communication est chiffrée |
| `www.exemple.fr` | le **nom de domaine** — l'adresse lisible du serveur |
| `/cours/snt/internet.html` | le **chemin** — où se trouve le document sur ce serveur |
| `page=2` | les **paramètres** — des informations transmises au serveur |

!!! question "À toi de jouer B.1 ⭐⭐⭐"
    Écris `decouper_url(u)` qui renvoie les quatre parties.

    **Indice :** `split("://")` puis `split("/")` puis `split("?")`.

??? success "Corrigé"
    ```python
    def decouper_url(u):
        protocole = u.split("://")[0]
        reste = u.split("://")[1]

        domaine = reste.split("/")[0]
        chemin = "/" + "/".join(reste.split("/")[1:])

        parametres = ""
        if "?" in chemin:
            parametres = chemin.split("?")[1]
            chemin = chemin.split("?")[0]

        return protocole, domaine, chemin, parametres


    for partie in decouper_url("https://www.exemple.fr/cours/snt/internet.html?page=2"):
        print("[", partie, "]")
    ```

    ```text
    [ https ]
    [ www.exemple.fr ]
    [ /cours/snt/internet.html ]
    [ page=2 ]
    ```

    !!! danger "Le piège des paramètres — un rappel du module Les données"
        Tout ce qui suit le `?` est **visible** : dans l'historique du navigateur, dans les journaux du serveur, et parfois transmis aux sites suivants.

        C'est pourquoi une donnée sensible ne doit **jamais** figurer dans une URL. Un site qui affiche un mot de passe ou un numéro dans la barre d'adresse est mal conçu — et c'est un signal d'alerte immédiat.

!!! warning "Lire un nom de domaine correctement"
    Le domaine se lit **de droite à gauche**. Dans `www.exemple.fr`, c'est `exemple.fr` qui identifie le propriétaire.

    Conséquence pratique, à connaître :

    - `banque.fr.exemple.com` appartient à **exemple.com**, pas à une banque.
    - `exemple.com/banque.fr` appartient aussi à **exemple.com**.

    C'est le fondement de nombreuses tentatives d'escroquerie : une adresse qui **contient** un nom connu n'appartient pas pour autant à son propriétaire. Le nom qui compte est celui juste avant l'extension.

## <span style="color:#1565c0">HTTP : demander et répondre</span>

Le client envoie une **requête**, le serveur renvoie une **réponse** accompagnée d'un **code**.

| Code | Signification |
| --- | --- |
| **200** | tout va bien, voici le document |
| **301 / 302** | le document a déménagé, voici sa nouvelle adresse |
| **403** | tu n'as pas le droit d'accéder à ce document |
| **404** | ce document n'existe pas |
| **500** | le serveur a rencontré une erreur de son côté |

!!! tip "Retenir la logique des familles"
    Le **premier chiffre** donne le sens général : `2xx` réussite, `3xx` redirection, `4xx` erreur **du client** (ta demande est fautive), `5xx` erreur **du serveur**.

    D'où une distinction utile : un `404` signifie que tu t'es trompé d'adresse ; un `500` signifie que le site est en panne. Dans le premier cas, inutile de réessayer.

!!! danger "HTTP et HTTPS"
    En **HTTP** simple, tout circule en clair : n'importe quel intermédiaire sur le trajet peut lire ce qui passe — y compris un mot de passe.

    En **HTTPS**, la communication est **chiffrée**. Un intermédiaire voit qu'une communication a lieu et avec quel serveur, mais pas son contenu.

    !!! warning "Ce que le cadenas ne dit pas"
        Le cadenas garantit que la communication est chiffrée. Il ne garantit **absolument pas** que le site est honnête.

        Un site frauduleux peut parfaitement obtenir un certificat et afficher un cadenas. La vraie vérification porte sur le **nom de domaine**, pas sur le cadenas.

## <span style="color:#1565c0">HTML : décrire un document</span>

Le HTML n'est pas un langage de programmation : il ne calcule rien. C'est un langage de **description** — il dit ce que sont les éléments d'un document.

```html
<html>
  <body>
    <h1>Cours de SNT</h1>
    <p>Voir <a href="donnees.html">les données</a> et
       <a href="images.html">les images</a>.</p>
  </body>
</html>
```

| Balise | Signifie |
| --- | --- |
| `<html>` | le document entier |
| `<body>` | la partie visible |
| `<h1>` | un titre de premier niveau |
| `<p>` | un paragraphe |
| `<a href="...">` | un **lien** vers un autre document |

!!! info "La structure en balises"
    Chaque élément est encadré par une balise ouvrante `<p>` et une balise fermante `</p>`. Les éléments s'**imbriquent** les uns dans les autres.

    Cette structure imbriquée rappelle le **JSON** du module *Les données* : deux formats différents, une même idée d'emboîtement.

!!! question "À toi de jouer B.2 ⭐⭐⭐ — Extraire les liens"
    Écris `liens(html)` qui renvoie la liste des adresses pointées par les balises `<a href="...">`.

    **Indice :** découper sur `href="`, puis sur le guillemet suivant.

??? success "Corrigé"
    ```python
    page = '''<html><body>
    <h1>Cours de SNT</h1>
    <p>Voir <a href="donnees.html">les donnees</a> et
       <a href="images.html">les images</a>.</p>
    </body></html>'''


    def liens(html):
        resultat = []
        morceaux = html.split('href="')
        for morceau in morceaux[1:]:
            resultat.append(morceau.split('"')[0])
        return resultat


    print(liens(page))
    ```

    ```text
    ['donnees.html', 'images.html']
    ```

    !!! tip "Pourquoi `morceaux[1:]`"
        Le premier morceau est ce qui précède le **premier** `href="` — il ne contient aucun lien. On le saute avec le slicing de M0.

    !!! success "Ce que tu viens d'écrire"
        Un **extracteur de liens**. C'est la brique de base d'un robot d'indexation : partir d'une page, en extraire les liens, visiter chaque lien, recommencer.

        C'est ainsi qu'un moteur de recherche découvre le Web.

## <span style="color:#1565c0">Comment un moteur de recherche fonctionne</span>

En trois étapes :

!!! abstract "1. L'exploration"
    Des programmes automatiques — des **robots** — parcourent le Web de lien en lien, exactement comme ta fonction `liens()`. Ils découvrent ainsi de nouvelles pages en continu.

!!! abstract "2. L'indexation"
    Le contenu de chaque page est analysé et rangé dans un **index** : pour chaque mot, la liste des pages où il apparaît. C'est ce qui rend la recherche instantanée — on ne fouille pas le Web au moment de la requête, on consulte un index préparé à l'avance.

!!! abstract "3. Le classement"
    Des milliers de pages contiennent le mot cherché. Il faut les **ordonner**. Les critères historiques incluent le nombre de liens pointant vers une page, la qualité perçue du site, la localisation de l'utilisateur, son historique.

!!! danger "L'étape 3 est la même question qu'au module précédent"
    Ordonner des résultats, c'est **optimiser un critère choisi**. Exactement comme le fil d'actualité que tu as trié de deux façons opposées.

    Trois conséquences directes :

    - **Le premier résultat n'est pas « le meilleur »** — c'est celui qui maximise le critère du moteur.
    - Des entreprises entières travaillent à **remonter** dans ce classement : c'est le référencement.
    - Deux personnes cherchant la même chose au même moment n'obtiennent **pas les mêmes résultats**.

!!! quote "Ce qu'il faut en tirer pour vérifier une information"
    « Je l'ai vu en premier sur un moteur de recherche » n'est pas un argument. La position d'un résultat dit quelque chose sur son adéquation au critère de classement, **rien** sur sa véracité.

    C'est le même réflexe que pour le fil d'actualité : remonter à la source plutôt que se fier à l'ordre d'affichage.

## <span style="color:#1565c0">Auto-évaluation</span>

!!! question "Teste tes connaissances"
    1. Quelle différence entre Internet et le Web ?
    2. Dans `https://banque.fr.exemple.com`, à qui appartient le site ?
    3. Que signifie un code 404 ? Et un code 500 ?
    4. Le cadenas HTTPS garantit-il qu'un site est honnête ?
    5. Pourquoi ne jamais mettre de donnée sensible dans une URL ?
    6. Pourquoi le premier résultat d'un moteur n'est-il pas forcément le meilleur ?

??? success "Réponses"
    1. Internet est le **réseau** de machines ; le Web est **un service** qui circule dessus, apparu une vingtaine d'années plus tard. Courriel, messageries et jeux en ligne circulent aussi sur Internet sans être le Web.
    2. À **exemple.com**. Le nom qui compte est celui juste avant l'extension ; on lit de droite à gauche.
    3. **404** : le document n'existe pas — erreur du client, inutile de réessayer. **500** : le serveur est en panne — erreur du serveur, réessayer plus tard a du sens.
    4. **Non.** Il garantit seulement que la communication est chiffrée. Un site frauduleux peut afficher un cadenas. Ce qu'il faut vérifier, c'est le nom de domaine.
    5. Parce que les paramètres après le `?` sont visibles : historique du navigateur, journaux du serveur, parfois transmis aux sites suivants.
    6. Parce que le classement **optimise un critère** choisi par le moteur — comme le fil d'actualité du module précédent. La position ne dit rien de la véracité.

## <span style="color:#1565c0">Ce qu'il faut retenir</span>

!!! success "L'essentiel du bloc B"
    - **Internet** est le réseau, **le Web** un service qui circule dessus.
    - Le Web repose sur trois piliers : **URL**, **HTTP**, **HTML**.
    - Un nom de domaine se lit **de droite à gauche** : c'est le nom juste avant l'extension qui identifie le propriétaire.
    - Le cadenas **HTTPS** garantit le chiffrement, **pas** l'honnêteté du site.
    - Le **HTML décrit**, il ne calcule pas.
    - Un moteur de recherche **explore, indexe, classe** — et le classement optimise un critère, comme le fil d'actualité.
