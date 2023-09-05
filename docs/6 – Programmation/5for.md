# La boucle for

:warning: [Activité Capytale](https://capytale2.ac-paris.fr/web/c/f8b0-673856/mlc) :warning:

Si écrire correctement la condition d'une boucle `#!python while` est parfois difficile, la pluplart des boucles utilisées en programmation sont **finies**. On utilisera dans ce cas la boucle `#!python for` (*pour* en anglais).

## La notion d'itérables (ou ensembles de valeurs énumérables)

La notion d'itérables est une notion clef en programmation. Un **itérable** désigne un objet que l'on peut **énumérer**, ou plutôt **itérer**, c'est-à-dire le décomposer en une suite d'éléments. Quelques exemples concrets :

* La chaine de caractère `#!python 'pantoufle'` est itérable : `#!python 'p'`, `#!python 'a'`, `#!python 'n'`, `#!python 't'`, `#!python 'o'`, `#!python 'u'`, `#!python 'f'`, `#!python 'l'`, `#!python 'e'`

* Le tableau (type `list`qu'on étudiera plus tard) `#!python [4, 3, 17]` est itérable : `#!python 4`, `#!python 3`, `#!python 17` 

* Le nombre `#!python 42` n'est pas itérable, il n'est pas décomposable.

Il sera plus tard possible de définir vos propres "types" de variable et vos propres itérateurs !

## Syntaxe

``` py
for variable in itérable:
    instruction1
    instruction2
    instruction3
    ...
```

Ont dit la variable `variable` parcourt l'ensemble `itérable`, elle va "capturer" chacun des élements de l'itérable à chaque tour de boucle !

## Exemples

=== "Chaîne de caractères"

    Programme :

    ``` py
    for caractere in 'NSI':
        print(caractere)
    ```

    Sortie :

    ``` py
    N
    S
    I
    ```

=== "Tableau d'entiers"

    Programme :

    ``` py
    for valeur in [1, 5, 17]:
        print(valeur)
    ```

    Sortie :

    ```
    1
    5
    17
    ```
=== "Sans utilisation de la variable"

    Programme :

    ``` py
    for jenesersarien in [1, 2, 3, 4, 5, 6]:
        print("OK")
    ```

    Sortie :

    ```
    OK
    OK
    OK
    OK
    OK
    OK
    OK
    ```

=== "Range"

    Programme :

    ``` py
    for i in range(7):
        print(i)
    ```

    Sortie :

    ```
    0
    1
    2
    3
    4
    5
    6
    ```

## Précisions sur `#!python range`

Il est très fréquent de vouloir une variable qui doit parcourir un ensemble de nombres entiers consécutifs. On y arrive plutôt facilement avec la boucle `#!python while` :

``` py
i = 0
while i < 10:
    print(i)
    i += 1
```

Avec la boucle `#!python for`, on pourrait arriver au même résultat avec un tableau :

``` py
for i in [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]:
    print(i)

```

Mais c'est extrêmement pénible à écrire et peu générique. Heureusement, comme vous avez remarqué précedemment, l'objet de type `#!python range` permet de générer ce genre d'ensemble de nombres entiers consécutifs.

!!! abstract "Générer une plage de nombres entiers"
    L'objet `#!python range(start, stop, step)` renvoie une "séquence" de nombres entiers en partant de `#!python start` (inclus) jusqu'à `#!python stop` (exclus), en incrémentant de `#!python step` (*pas* en anglais).

    * `#!python start` est facultatif et vaut 0 par défaut.

    * `#!python step` est facultatif et vaut 1 par défaut. Mais si on veut préciser `#!python step`, alors il faut donner aussi `#!python start`, même si sa valeur est 0.

!!! note "Un peu de détails"
    On peut convertir un objet de ttype `#!python range` vers un tableau (`#!python list`) :

    ``` py
    >>> range(10)
    range(0, 10)
    >>> list(range(5))
    [0, 1, 2, 3, 4]
    >>> list(range(1, 20 , 3))
    [1, 4, 7, 10, 13, 16, 19]
    ```

    `#!python range` en fait va générer ces valeurs à la volée, on évite ainsi de stocker tout un tableau en mémoire. On parle aussi du concept plus large de **lazy evaluation** en anglais, ou évaluation parresseuse : on ne génère le nombre qu'à la demande.