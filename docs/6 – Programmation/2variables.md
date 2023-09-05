# Les variables et les types

## Définition et affectation

Une **variable** en programmation n'a pas du tout le même sens qu'en mathématiques. Une variable est une **association** entre un **nom** (son identifiant) et une **valeur** (de n'importe quel type). C'est bien la plus petite brique de base pour stocker une information et la manipuler. On peut se représenter une variable comme une boîte étiquetée dans laquelle on met quelque chose. Par exemple :

``` py
toto = 42
```

<div style="text-align:center"><img src="../images/toto.png" /></div>

!!! note "La notion d'affectation"
    L'instruction qui permet d'associer une valeur à une variable (nouvelle ou déjà créée) s'appelle une **affectation**. En python, on utilise le symbole `=`. A ne pas confondre avec l'égalité mathématiques ! Certains langages utilisent le symbole `←` comme symbole d'affection.

!!! note "La notion d'initialisation"
    La première fois qu'on affecte une valeur à une variable, on dit qu'on l'**initialise**. On parle aussi de **déclaration**.


!!! info 
    Par abus de langage, on confond souvent variable et nom de variable. Ici on parlera de la variable `toto`.



## Ce qu'il se passe en mémoire

Regardons ce qu'il se passe physiquement lorsqu'on initialise une variable. Une machine peut être vue comme la réunion de deux composants :

* Un centre de calcul, le **processeur**, chargé de manipuler des données (copie, addition, tests etc.).

* Une **mémoire** permettant de stocker des données.

Toutes les données qu'on manipule dans un programme sont stockées dans la mémoire vive (RAM) de l'ordinateur. C'est un très grand tableau découpé en octet :

<div style="text-align:center"><img src="../images/1ram.png" /></div>

Chaque case (octet) de ce tableau se réfère par un indice, que l'on appelle **adresse**. Lorsque j'initialise `toto` à 42, un entier codé sur 32 bits imaginons, plusieurs étapes se succèdent :

* **Étape 1 :** La machine commence par trouver un emplacement disponible de la taille souhaitée. Ici, elle nous renvoie 312.

<div style="text-align:center"><img src="../images/2ram.png" /></div>

* **Étape 2 :** On associe cet emplacement à l'identifiant `toto`. 

* **Étape 3 :** Finalement, on copie l'entier 42 à cet emplacement.

<div style="text-align:center"><img src="../images/3ram.png" /></div>

L'identifiant `toto` n'est qu'une simple adresse dans la mémoire !

## Expressions et évaluations

Python permet d'effectuer tout type de calcul, comme une calculatrice ordinaire. Les règles de priorité des calculs sont les mêmes qu'en mathématiques. On utilise des parenthèses lorsqu'on a besoin de changer l'ordre de priorité.

| Opération | Symbole | Exemple | Résultat |
|---|---|---|---|
| Addition | `+` | `#!python 10 + 20` | `#!python 30`
| Soustraction | `-` | `#!python 2 - 7` | `#!python -5` |
| Multiplication | `*` | `#!python  5 * 9` | `#!python 45` |
| Puissance | `**` | `#!python  2 ** 3` | `#!python 8` |
| Division | `/` | `#!python 5 / 2` | `#!python 2.5` |
| Division entière | `//` | `#!python  5 // 2` | `#!python 2` |
| Reste (modulo) | `%` | `#!python  5 % 2` | `#!python 1` |

Analysons cette courte séquence d'instructions :

``` py linenums="1"
>>> a = 2
>>> a = 4
>>> a
4
>>> b = a + 3
>>> b
7
>>> b = c + 1
Traceback (most recent call last):
  File "<pyshell>", line 1, in <module>
NameError: name 'c' is not defined
>>> 
```

!!! info "Analyse ligne par ligne"
    === "Ligne 1"
        On initialise une variable `a` à 2.
    === "Ligne 2"
        On réaffecte une nouvelle valeur, 4, à la variable `a`.
    === "Ligne 3 et 4"
        On demande la valeur associée à `a`. L'ancienne valeur 2 a bien été écrasée.
    === "Ligne 5"
        On initialise une nouvelle valeur `b` avec l'**expression** `a + 3`. La machine doit au préalable l'évaluer avant de l'affecter. Dans l'ordre :

        * Python lit le membre de droite  `a + 3`.

        * Il récupère la valeur stockée dans `a`, c'est-à-dire 4.

        * Il **évalue** l'expression `4 + 3`.

        * Il affecte à `b` la somme obtenue, c'est-à-dire 7.

        On retient que l'affection se déroule toujours en dernier (généralement).

    === "Ligne 8"
        On tente de réaffecter à `b` le résultat de l'expression `c + 1`. Or aucune variable nommée `c` n'a été déclarée auparavant, on obtient donc une erreur.

!!! note "Syntaxe abrégée"
    On a souvent besoin d'**incrémenter** une variable (augmenter sa valeur de 1) ou de la décrémenter (diminuer sa valeur de 1). Au lieu d'écrire `#!python a = a + 1`, on peut écrire de façon plus courte : `#!python a += 1`.

    Cette syntaxe raccourcie fonctionne pour n'importe quelle valeur de l'incrément, ainsi que pour les opérateurs `#!python + , - , *, **, / , //, %` :

    ``` py
    >>> a = 20
    >>> a -= 15
    5
    >>> a /= 2
    2.5
    ```

## Types de variables

Pour l'instant, nos variables ne contenaient que des nombres entiers. Pour différencier la nature de ce que peut contenir une variable, on parle alors de **type de variable**. Voici les types que nous allons manipuler tout au long de l'année :

| Syntaxe | Type | Exemple
|:---|:---|:---|
`int`| Entier | `#!python 42` |
`float`| Flottant (à virgule) | `#!python 2.71828` |
`str`| Chaîne de caractères (ou string) | `#!python 'Hello, World'` |
`bool`| Booléen (`#!python True` ou `#!python False`) | `#!python True` |
`tuple`| p-uplet | `#!python (255, 127, 0)` |
`list`| Tableau | `#!python [0, 1, 2, 3, 4, 5]` |
`dict`| Dictionnaire | `#!python {'prenom': 'Thomas', 'age': 44, 'taille': 184}` |
`function`| Fonction | `#!python print` |

!!! tip "Déterminer le type d'une variable"
    Il suffit d'utiliser la fonction `type` :
    ``` py
    >>> a = 'Au secours!'
    >>> type(a)
    <class 'str'>
    ```

!!! info "Typage dynamique/statique"
    En Python, on omet de préciser le type de variable utilisé. Dans le langage C par exemple, il est nécessaire de préciser le type par un mot-clef :

    ``` C
    int a = 42
    ```

    Ce typage est dit **statique** car la variable `a` ne pourra pas changer de type au cours du programme, elle n'aura le droit que de contenir un nombre entier. Python offre une plus grande souplesse :

    ``` py
    >>> a = 1
    >>> type(a)
    <class 'int'>
    >>> a = 'test'
    >>> type(a)
    <class 'str'>
    ```

    Python a changé tout seul le type de notre variable, sans intervention ! On parle alors de **typage dynamique**.

    !!! bug "Mauvaise pratique"
        Changer le type d'une variable au cours d'un programme est une grande source d'erreur. Pour que votre code reste clair et facilement compréhensible, n'utilisez pas le typage dynamique.

!!! note "Conversion entre les différents types"
    On peut parfois souhaiter passer d'un type à un autre, si cela fait sens évidemment.

    ``` py
    >>> float(3)
    3.0
    >>> int(2.47)
    2
    >>> str(47)
    '47'
    ```

## Règles de nommage

Python et la plupart des langages de programmation suivent les mêmes règles de nommage des variables :

* Seuls les **lettres non-accentuées** (:warning: miniscule et majuscule sont des caractères différents, ainsi les variables `a` et `A` sont bien deux variables distincts), les **chiffres** et le **tiret du bas** `_` sont autorisées. Les espaces ne sont donc pas autorisés.

* Le nom de la variable ne doit pas commencer par un chiffre.

* Le nom de la variable ne doit pas être un **mot-clef** (keyword en anglais) du langage comme `#!python while`, `#!python if`, `#!python def` etc.

!!! success "Les bonnes pratiques"
    * Le nom de la variable doit être **explicite** et donner du sens à votre code. Par exemple si on doit manipuler une variable qui stocke un âge, il faut l'écrire non pas `a` mais `age`. Pour les indices de tableau et les incréments dans les boucles on utilise souvent les noms `i`, `j`, `k`.

    * Le nom des variables (et fonctions) commencent par une **minuscule**. Les noms qui commencent par une majuscule seront réservés pour les types construits / classes.

    * Si le nom est composé, il existe deux manières :

        * `snake_case` : les mots sont séparés par des underscores.

        * `camelCase` : les mots sont séparés par des majuscules mais la 1ère lettre est minuscule.

        C'est une question de préférence, la chose à retenir est de ne pas mélanger les deux, il faut rester **consistent**. 

## Afficher une variable

### Méthode directe

La fonction `#!python print` permet d'afficher dans la console ce qu'on lui donne en argument. Cela peut être simplement du texte :

``` py
>>> print("Hello, World.")
Hello, World.
```

Ou même un nombre :

``` py
>>> print(3.1415)
3.1415
```

On peut alors afficher nos variables :

``` py
>>> a = "une chaîne de caractère"
>>> print(a)
une chaîne de caractère
>>> toto = 42
>>> print(toto)
42
```

Ce qui est très utile lorsqu'on conçoit des scripts ! L'interêt est assez limité dans le shell (la console `#!python >>>`) effectivement.


!!! info "Formatage avancé"
    Parfois, on souhaite mélanger du texte prédéfini et des variables. Il existe 3 méthodes :

    === "Utiliser la variadicité de `#!python print`"

        Une fonction est dite variadique si elle accepte un nombre variable de paramètres. C'est le cas pour la fonction `#!python print` :

        ``` py
        >>> age = 18
        >>> print("Vous avez", age, "ans.")
        Vous avez 18 ans.
        ```
        Le problème, c'est que finalement on n'a pas réussi à créer directement la chaîne de caractères `#!python 'Vous avez 18 ans'`.

    === "Concaténer les chaînes de caractères" 
        
        Quand on utilise l'addition `+` entre deux chaînes de caractères, l'expression s'évalue comme la **concaténation** de celles-ci.

        ``` py
        >>> age = 18
        >>> texte = "Vous avez " + str(age) + " ans."
        >>> print(texte)
        Vous avez 18 ans.
        ```

        Attention, il faut bien convertir l'entier `age` en chaîne de caractères !

    === "fstring"

        C'est désormais la méthode standard (à partir de la version 3.5 de Python) pour insérer des variables dans une chaîne de caractères :

        ``` py
        >>> age = 18
        >>> texte = f"Vous avez {age} ans."
        >>> print(texte)
        Vous avez 18 ans.
        ```
        La syntaxe est bien plus claire et courte ! Surtout si on utilise directement `#!python print(f"Vous avez {age} ans.")`.




        
## Demander une entrée à l'utilisateur

Parfois, on voudrait demander à l'utilisateur de nous fournir un nombre ou une saisie clavier. On utilise alors la fonction `input` :

``` py
>>> input()
je tape sur mon clavier
'je tape sur mon clavier'
```

Elle renvoie toujours une chaîne de caractère, c'est pourquoi il ne faut pas oublier de convertir l'entrée dans le format souhaité :

``` py
>>> age = int(input())
18
>>> age
18
```

On peut aussi passer en entrée une chaîne de caractère :

``` py
>>> age = int(input('Donne moi ton âge : '))
Donne moi ton âge : 18
>>> age
18
```



