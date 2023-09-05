# Introduction aux tableaux

:warning: [Activité Capytale](https://capytale2.ac-paris.fr/web/c/cca5-863835) :warning:


Considérons un scénario dans lequel vous devez calculer la moyenne de 100 nombres entiers saisis par l'utilisateur. Pour l'instant à votre niveau, la seule solution serait d'effectuer 100 opérations `#!python input()` pour stocker les valeurs saisies dans 100 variables différentes. Puis calculer la moyenne à partir de celles-ci. Ce serait évidemment très fastidieux, c'est pourquoi le concept de tableau devient nécessaire.


## Notion de tableau et d'indices

En programmation, un **tableau**  est une séquence ordonnée de valeurs de même type. Il se rapproche de la notion de vecteur en mathématiques.

<figure markdown>
  ![Image title](images/tableau.png){ width="500" }
  <figcaption>Représentation usuelle d'un tableau d'entiers à 6 cases (ou cellules)</figcaption>
</figure>

Stockons ce tableau dans une variable `t`. Ce tableau est **ordonné** : le 1er élement est 4, le deuxième est 2, et le dernier 12.

On repère chaque élément du tableau par sa position, le numéro de la case, qu'on appelle **indice**.

<figure markdown>
  ![Image title](images/tableau_indice.png){ width="500" }
  <figcaption>Le premier indice d'un tableau est 0 !</figcaption>
</figure>

On note `t[i]` pour désigner l'élement d'indice `i` du tableau `t`. Par exemple, dans notre exemple, `t[3]` renvoie la vlauer 42.

La **taille** ou longueur d'un tableau est le nombre d'éléments qu'il contient. Ici, le tableau `t` a une taille égale à 6.

## Tableau / liste en Python

En python, le type `#!python list` implémente le type abstrait de tableau. Un tableau est définit avec des crochets et on sépare ses éléments par des virgules. Par abus de langage on parle de liste plutôt que de tableau.

Une liste vide se déclarera par `[]`.

```py
>>> t = [4, 2, 1, 42, 78, 12]
>>> type(t)
<class 'list'>
>>> t[3]
42
>>> len(t)
6
>>> t[6]
Traceback (most recent call last):
File "<pyshell>", line 1, in <module>
IndexError: list index out of range
>>> t[-1]
12
>>> liste_vide = []
>>> len(liste_vide)
0
```

!!! note "A retenir"
    * La fonction `#!python len` renvoie la taille de la liste donnée (et même de tout autre itérable !)

    * Le premier élément d'une liste est à l'indice `#!python 0` et le dernier à l'indice `#!python len(t) - 1` 

    * L'indice `#!python -1` permet d'accèder facilement au dernier élement. 

!!! note "Euh Python ?"
    En réalité, une liste désigne une autre structure de données complètement différente en informatique (liste chaînée), ce qui prête à confusion. Il faudrait donc privilégier le terme de *tableau*.

## Modifier une liste

En python, les objets de type `list`sont modifiables (ou *mutable*) arpès leur création.

### Modifier d'un élement à l'indice

On modifie un élément du tableau par simple affectation, en écrasant sa valeur avec la nouvelle.

```py
>>> famille = ["Bart", "Lisa", "Maggie"]
>>> famille[0] = "Bartholomew" # oui, c'est son vrai nom
>>> famille
['Bartholomew', 'Lisa', 'Maggie']   
```

### Ajouter un élément en fin de liste

La méthode `#!python append` permet d'ajouter un élément en fin de liste (et donc d'augmenter la taille de la liste).

```py
>>> famille = ["Bart", "Lisa", "Maggie"]
>>> famille.append("Homer")
>>> famille
['Bartholomew', 'Lisa', 'Maggie', 'Homer']   
```

!!! note Différence entre fonctions et méthodes
    En programmation, on peut définir nos propres types grâce à l'utilisation de  classe. Une classe est composée de membres (variables) et de méthodes (fonctions) qui agissent sur ces membres. Un objet est une instance d'une classe. 
    ```py
    objet.membre
    objet.methode(arguments...)
    ```
    Par exemple, `t` est un objet de la classe `#!python list` dont la méthode `append` permet de lui ajouter un élément en fin de liste.

### Supprimer un élément

La métode `remove` permet de supprimer la première occurrence de l'élément (et seulement la première). À condition bien entendu que l'élément soit dans la liste.

```py
>>> matieres = ["nsi", "maths", "anglais", "français", "maths"]
>>> matieres.remove("maths")
>>> matieres
["nsi", "anglais", "français", "maths"]
>>> matieres.remove("espagnol")
Traceback (most recent call last):
File "<pyshell>", line 1, in <module>
ValueError: list.remove(x): x not in list
```


## Parcourir une liste

Il existe principalement deux méthodes pour parcourir une liste : par ses éléments ou par les indices. Mais dans les deux cas on utilise une boucle `#!python for`.


### Parcours par élément

```py
famille = ["Bart", "Lisa", "Maggie"]
for membre in famille:
    print(membre)
```

Affiche :

```
Bart
Lisa
Maggie
```

### Parcours par indice

Chaque élément étant accessible par son indice (de `#!python 0` à `#!python len(liste) - 1`), il suffit de faire parcourir à une variable `i` l'ensemble des entiers de `#!python 0` à `#!python len(liste) - 1`, par l'instruction `#!python range(len(liste))` :

```py
famille = ["Bart", "Lisa", "Maggie"]
for i in range(len(famille)):
    print(i, famille[i])
```

Affiche :

```
0 Bart
1 Lisa
2 Maggie
```

### Parcours par élément et indice

Parfois on veut avoir l'indice et l'élement en même temps, on peut alors utiliser la fonction `#!python enumerate`.

```py
famille = ["Bart", "Lisa", "Maggie"]
for i, membre in enumerate(famille):
    print(i, membre)
```

Affiche :

```
0 Bart
1 Lisa
2 Maggie
```


## Créer une liste

### Initialisation explicite

```py
tableau = [11, 19, 21, 29, 46]
```

### Avec une bouble for

On crée une liste vide, puis on lui ajoute les éléments au fur et à mesure grâce à une boucle for. Par exemple, création d'une liste contenant les entiers multiples de 3 ou de 5 inférieurs à 100 :


```py
multiples = []
for k in range(101):
    if k % 3 == 0 or k % 5 == 0:
        multiples.append(k)
```

### Élements identiques

Il est souvent pratique d'initialiser une liste de taille donnée, souvent en la remplissant de la même valeur, souvent 0. Par exemple, pour produire une liste contenant 26 zéros:

```py
>>> lst = 26 * [0]
>>> lst
[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```

### Liste en compréhension

#### Syntaxe de base

Sûrement la meilleure feature du langage Python. Elle permet de générer des listes complexes rapidement. La syntaxe la plus simple est :

```py
tableau = [expression for element in iterable]
```

Imaginons que veuille énumérer les 10 premiers carrées. En utilisant une boucle for :

```py
tab = []
for k in range(10):
    tab.append(k ** 2)
```

On peut générer cette liste plus facilement en compréhension, en "rentrant" la boucle `for` dans les crochets de définition de la liste :

```py
tab = [k ** 2 for k in range(10)]
```

Pour chaque élément `k` de l'itérable `#!python range(10)`, on génère l'élément `#!python k ** 2` de la liste !

#### Syntaxe avec filtre

La syntaxe d'une liste en compréhension avec filtre :

```py
tableau = [expression for element in iterable if condition]
```

Par exemple, on souhaite garder les valeurs positives de la liste suivante :

```py
tab = [11, 28, -16, -18, -10, 16, 10, 16, 2, 7, 23, 22, -4, -2, 19, 16, 22, -8]

```

Avec une boucle for, une solution serait :

```py
tab_positif = []
for val in tab:
    if val >= 0:
        tab_positif.append(val)
```

On peut créer la même chose en compréhension, en incluant l'instruction conditionnelle `#!python if` dans la définition de la liste :


```py
tab_positif = [val for val in tab if val >= 0]
```

## Exercices

!!! example "Exercice 1"
    === "Énoncé" 
        Dans la liste suivante:
        
        - remplacer `"Loki"` par `"Thor"`
        - ajouter `"Dr. Strange"`
        - supprimer l'intrus.

        ```python
        avengers = ["Black Widow", "Captain America", "Loki", "Iron Man", "Hulk", "Batman", "Hawkeye"]
        ```
        
    === "Solution" 
        ```python
        avengers[2] = 'Thor'
        avengers.append('Dr. Strange')
        avengers.remove('Batman')
        ```
        
!!! example "Exercice 2"
    === "Énoncé" 
        Construire une liste de 100 éléments tous égaux à 0. Puis remplacer tous les éléments d'indice impair par des 1.

    === "Solution" 
        ```python
        tab = [0] * 100
        for i in range(100):
            if i % 2 != 0:
                tab[i] = 1
        ```

        Ou plus optimisé :

        ```python
        tab = [0] * 100
        for i in range(50):
            tab[2 * i + 1] = 1
        ```

        Ou en liste de compréhension (et condition ternaire) :

        ```python
        tab = [0 if i % 2 == 0 else 1 for i in range(100)]
        ```


        

!!! example "Exercice 3"
    === "Énoncé"
        Trouvez le nombre qui est **exactement à la même place** dans la liste `list1` et dans la liste `list2`, sachant que :

        - les deux listes ont la même taille
        - vous n'avez droit qu'à une seule boucle ```for```. 

        ```python
        list1 = [8468, 4560, 3941, 3328, 7, 9910, 9208, 8400, 6502, 1076, 5921, 6720, 948, 9561, 7391, 7745, 9007, 9707, 4370, 9636, 5265, 2638, 8919, 7814, 5142, 1060, 6971, 4065, 4629, 4490, 2480, 9180, 5623, 6600, 1764, 9846, 7605, 8271, 4681, 2818, 832, 5280, 3170, 8965, 4332, 3198, 9454, 2025, 2373, 4067]
        list2 = [9093, 2559, 9664, 8075, 4525, 5847, 67, 8932, 5049, 5241, 5886, 1393, 9413, 8872, 2560, 4636, 9004, 7586, 1461, 350, 2627, 2187, 7778, 8933, 351, 7097, 356, 4110, 1393, 4864, 1088, 3904, 5623, 8040, 7273, 1114, 4394, 4108, 7123, 8001, 5715, 7215, 7460, 5829, 9513, 1256, 4052, 1585, 1608, 3941]
        ```
        
    === "Solution"
        ```python
        list1 = [8468, 4560, 3941, 3328, 7, 9910, 9208, 8400, 6502, 1076, 5921, 6720, 948, 9561, 7391, 7745, 9007, 9707, 4370, 9636, 5265, 2638, 8919, 7814, 5142, 1060, 6971, 4065, 4629, 4490, 2480, 9180, 5623, 6600, 1764, 9846, 7605, 8271, 4681, 2818, 832, 5280, 3170, 8965, 4332, 3198, 9454, 2025, 2373, 4067]
        list2 = [9093, 2559, 9664, 8075, 4525, 5847, 67, 8932, 5049, 5241, 5886, 1393, 9413, 8872, 2560, 4636, 9004, 7586, 1461, 350, 2627, 2187, 7778, 8933, 351, 7097, 356, 4110, 1393, 4864, 1088, 3904, 5623, 8040, 7273, 1114, 4394, 4108, 7123, 8001, 5715, 7215, 7460, 5829, 9513, 1256, 4052, 1585, 1608, 3941]

        for i in range(len(list1)):
            if list1[i] == list2[i]:
                print(list1[i])
        ```

        Ici, on aurait bien aimé parcourir par élément et non par indice. Il existe une fonction justement qui permet de combiner plusieurs itérables entre-eux, la fonction `#!python zip` !

        ```python
        for e1, e2 in zip(list1, list2):
            if e1 == e2:
                print(e1)
        ```
        
        C'est plus joli, non ? C'est sûrement trop avancé. Mon tuteur ne veut pas que je vous fasse de vous des experts de Python. Mais sachez que cette fonction se retrouve dans quasiment tous les langages de programmation respectables. Sinon, codez-la.


        

!!! example "Exercice 4"
    === "Énoncé" 
        On considère la liste 
        
        ```python
        temp = [11, 28, -16, -18, -10, 16, 10, 16, 2, 7, 23, 22, -4, -2, 19, 16, 22, -8, 18, -14, 29, -1, 16, 22, -5, 6, 2, -4, 9, -17, -13, 22, 14, 24, 22, -9, -18, -9, 25, -11, 17, 17, 25, -10, 2, -18, 29, 14, -16, 7]
        ```

        Construire la liste `temp_pos` qui ne contient que les éléments positifs de `temp`. 
    === "Solution" 
        ```python
        temp_pos = []
        for t in temp:
            if t >= 0:
                temp_pos.append(t)
        ```

        Vous avez voulu utliser la méthode `.remove` ? Ne pas **ajouter ni retirer** d'éléments de la liste pendant que vous la **parcourez** ! Modifier ses éléments est OK.
        
        Autre solution (liste en compréhension) :

        ```python
        temp_pos = [t for t in temp if t >= 0]
        ```
        

!!! example "Exercice 5 (BNS)"
    === "Énoncé" 
        Programmer la fonction `recherche`, prenant en paramètre un tableau non vide `tab` (type `list`) d'entiers et un entier `n`, et qui renvoie l'indice de la dernière occurrence de l'élément cherché. Si l'élément n'est pas présent, la fonction renvoie la longueur du tableau.

        Exemples :

        ```python 
        >>> recherche([5, 3],1)
        2
        >>> recherche([2,4],2)
        0
        >>> recherche([2,3,5,2,4],2)
        3

        ```
    
    === "Solution" 
        <!-- ```python linenums='1'
        def recherche(tab: list, n: int) -> int:
            '''
            Renvoie l'indice de la dernière occurence de l'entier n dans la liste tab.
            Si tab est vide, renvoie la longueur de la liste tab.
            '''
            indice_max = len(tab) # valeur par défaut si tab est vide
            for i in range(len(tab)):
                if tab[i] == n:
                    indice_max = i
            return i
        ``` -->


!!! example "Exercice 6"
    === "Énoncé" 
        Construire une liste de taille 26 contenant le nombre d'occurences de chaque lettre de l'alphabet dans le texte suivant:

        ```python 
        texte_long = '''
        mpaowhuqhvyywtvypjkfrrasexnwzrgpargvpjlfbjsxxjipjgkyscgdiqswpvpbzigfkljhicuftshk
        qekwqojwchsgyuvakynjpxlacrnbojawdisjzbcqjflhgqofhccdxnqpbnxcxcypawaqgzbikretwlkf
        qodnoseirzvssdczsyczqjbugcgjuorxciblnojkvygxqirysffsmjyokjdsxlymjokgodupumjoxcmi
        teeenikwlkzidirjnmexsmqjefsgpbpoynusfpudmxwcwrzzqzuobjtlyshbvvgjkhoujsdlnsyfshuu
        mfmqmssbyrzybswyswbdmqmcwsdudrfdnmlmnchossxcwarfmpkrcqcyvyjkplzexrnebukxhqbnzkgh
        nalfpkxghypaimemqzmcreozagufiljxdmgrwftyajtonfisefxujtdmpgxttugxhvpgdqhvgzohovbe
        qaafwqfiokzhtbxgoxpzzvbswlxdtykgufqevlmjjrddufrogzsfzzuaqpqfzinvmfpcylgftkkhqylp
        rgzywwefwghhrivsjtvbbcixhztwujdqqesdertmtwdricrzmwsibhstsgnnxbvqnyklcbrcxtycvcww
        ojphbqyrjffndkgwqfqvarfupklwwixekudmbspqtydkegltqvwjzfooscehpnfwvvnkrxsfakwezvol
        mpvnprcrwomddjneyrhpxmnrveibxqxcjluezypvsbfudilpjdqflsdhwucjgtusxjjcnewamoewwjhu
        '''
        ```
        
    === "Solution" 
        <!-- ```python linenums='1'
        occurences = 26 * [0]
        for lettre in texte_long:
            indice = ord(lettre) - ord('a')
            occurences[indice] += 1
        ``` -->
        