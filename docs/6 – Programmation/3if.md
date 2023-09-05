# L'instruction conditionnelle if

L'instruction conditionnelle `#!python if` permet de décider si des instructions doivent être exécutées suivant une certaine condition.

``` py
if une_certaine_condition:
    instruction1
    instruction2
    ...
```

Ainsi si la condition s'évalue à `#!python True` (vrai), alors la suite d'instructions indentées sera exécutée. Sinon ce bloc sera ignoré.

!!! tip "Un caractère important"
    Ne pas oublier le caractère `:` à la fin de la condition, juste avant l'indentation !

## Ecrire une condition : Les booléens

En mathématiques, une **proposition** est une phrase qui est soit **vraie**, soit **fausse**. Par exemple, la proposition "1 plus 1 égal 11" est fausse, tandis que la proposition "7 plus 2 égal 9" est vraie.

En python, ces deux affirmations s'écriront `#!python 1 + 1 == 11` et `#!python 7 + 2 == 9` (notez bien le double signe égal, le signe égal simple étant réservé pour l'affectation). Ce sont des expressions que Python va évaluer :

``` py
>>> 1 + 1 == 11
False
>>> 7 + 2 == 9
True
>>> type(False)
<class 'bool'>
```

Elles nous renvoient une valeur booléenne, c'est-à-dire de type `#!python bool`. Les autres opérateurs usuelles de comparaison sont disponibles :

| Opérateur | Signification | Symbole mathématiques | 
| --- | :--- | --- |
| `#!python ==` | "est égale à" | $=$ |
| `#!python !=` | "est différent de" | $\ne$ |
| `#!python <` | "est inférieur à" | $<$ |
| `#!python <=` | "est inférieur ou égale à" | $\leq$ |
| `#!python >` | "est supérieur à" | $>$ |
| `#!python >=` | "est supérieur ou égale à" | $\geq$ |

!!! tip "Retenir l'ordre des caractères des opérateurs de comparaison"
    Parfois on s'emmêle les pinceaux et on ne sait plus si c'est `<=` ou bien `=<`. On remarque en fait une certaine cohérence entre `<=`, `>=`, et `!=`... le signe `=`est toujours à la fin !

!!! note "Les opérateurs de compraison pour d'autres types"
    Parfois cela fait sens de vouloir tester si deux chaînes de caractères sont identiques, et il est tout naturel d'utiliser l'opérateur `==` dans ce cas :

    ``` py
    >>> devoir_paul = "La réponse est 42."
    >>> devoir_pierre = "La réponse est 42."
    >>> devoir_paul == devoir_pierre
    True
    ```

Parfois on veut vérifier plusieurs conditions. On utilise les opérateurs logiques `#!python not`, `#!python and` et `#!python or` (respectivement non, et, ou). Quelques exemples d'utilisation :

``` py
>>> not True
False
>>> not False
True
```

``` py
>>> moyenne = 15
>>> est_mention_AB = moyenne >= 12 and moyenne < 14
>>> est_mention_AB 
False
```

``` py
>>> couleur = 'rouge'
>>> est_primaire = couleur == 'rouge' or couleur == 'bleu' or couleur == 'vert'
>>> est_primaire
True
```
Voici la table de vérité de ces trois opérateurs logiques :

| C1 | C2 | C1 and C2 | C1 or C2 | not C1 |
| --- |--- |--- |--- |--- |
| False :x: | False :x:| False :x:| False :x:| True :white_check_mark: |
| False  :x:| True :white_check_mark: | False :x:| True :white_check_mark: | True :white_check_mark: |
| True :white_check_mark: | False :x:| False :x:| True :white_check_mark: | False :x:|
| True :white_check_mark: | True :white_check_mark: | True :white_check_mark: | True :white_check_mark: | False :x:|



## Exemples

Quelques codes à essayer pour différentes entrées.

### `if`

``` py
age = int(input('Donne moi ton age : '))

if n >= 18:
    print("Tu es majeur !")
```

### `else`

Le mot-clef `else` permet de faire le branchement "sinon". Il n'y a pas de condition à mettre.

``` py
if une_certaine_condition:
    # si la condition est évaluée à True, on exécute :
    instruction1
    instruction2
    ...
else:
    # si la condition est évaluée à False, on exécute :
    instruction1
    instruction2
    ...
```

``` py
age = int(input('Donne moi ton age : '))

if n >= 18:
    print('Tu es majeur !')
else:
    print('Tu es mineur !')
```

### Imbrication `if else`

On peut s'amuser à imbriquer des conditions dans des conditions.

``` py
moyenne = int(input('Ta moyenne au bac : '))

if moyenne < 8:
    print("Coup dur. Raté.")
else:
    if moyenne < 10:
        print("Repêchage.")
    else:
        if moyenne < 12:
            print("Admis.")
        else:
            if moyenne < 14:
                print("Mention AB.")
            else:
                if moyenne < 16:
                    print("Mention B.")
                else:
                    print("Mention TB.")
```

La syntaxe peut être rendue plus lisible grace au mot-clef `elif` (contraction de `else if`, "sinon si") :

``` py
moyenne = int(input('Ta moyenne au bac : '))

if moyenne < 8:
    print("Coup dur. Raté.")
elif moyenne < 10:
    print("Repêchage.")
elif moyenne < 12:
    print("Admis.")
elif moyenne < 14:
    print("Mention AB.")
elif moyenne < 16:
    print("Mention B.")
else:
    print("Mention TB.")
```

On remarque bien l'aspect séquentiel des tests.