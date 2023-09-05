# Les fonctions

:warning: [Activité Capytale à rendre jusqu'au 12 octobre](https://capytale2.ac-paris.fr/web/c/3e70-741354/mlc) :warning:

Une fonction est un bloc d'instruction qui ne s'exécute que lorsqu'il est appelé. Vous pouvez transmettre des données, appelées arguments, à une fonction. Une fonction peut renvoyer des données comme résultat.

Une fonction en programmation est donc semblable au concept de fonctions en mathématiques.

<div style="text-align:center"><img src="../images/fonction.png" /></div>

Vous avez déjà en fait manipulé tout un tas de fonctions : 
`#!python print`, `#!python input`, `#!python int`, `#!python type` etc.

!!! note "Exemple"
    La fonction `#!python bin` prend un nombre entier (type `#!python int`) comme **argument** et **renvoie** son écriture binaire :

    ``` py
    >>> bin(42)
    '0b101010'
    ```



Une fonction permet donc d'**organiser** son code en le découpant en sous-programmes qui ont une tâche bien précises. Non seulement cela vous permet de réutiliser une fonction à tout moment dans un programme, mais aussi de rendre votre code plus lisible, plus facile à modifier et à corriger.

!!! note "Tester les exemples"
    Lire simplement les programmes ne suffit pas ! Copier le code dans une console Python, sur Pyzo, sur l'IDLE Python, sur un éditeur quelconque... éxecute-le et n'hésitez pas à le modifier pour comprendre ce qu'il se passe !

## Syntaxe

### Créer une fonction

En python, une fonction se crée avec le mot-clef `#!python def` :

``` py
def ma_fonction():
    print('Bonjour depuis une fonction :)')
```

Une fois le code de ma fonction écrit, il ne s'exécute pas directement. Pour cela, il faut explicitement l'appeler !

### Appeler une fonction

Pour appeler une fonction dans le programme, on l'appelle grâce à son nom suivi de sa liste d'arguments entre parenthèses. Ici, la fonction ne demande aucun argument, ni ne renvoie de valeur.


``` py
def ma_fonction():
    print('Bonjour depuis une fonction :)')

ma_fonction()
```

### Passer des arguments

On peut transmettre des données aux fonctions par le biais d'arguments. Les arguments sont spécifiés après le nom de la fonction, à l'intérieur des parenthèses. Vous pouvez ajouter autant d'arguments que vous le souhaitez, il suffit de les séparer par une virgule.


``` py
def saluer_dupont(prenom):
    print(f'Bonjour {prenom} Dupont, ça va ?')

saluer_dupont('Jean')
saluer_dupont('Pierre')
saluer_dupont('Jacques')
```

Ici la fonction `#!python saluer_dupont` capture un argument, une chaîne de caractère, dans une variable que l'on a nommée `#!python prenom`. Lorsque la fonction est appelée, par exemple `#!python saluer_dupont('Jean')`, le paramètre `prenom` prend comme valeur `#!python 'Jean'` et le corps de la fonction est ensuite exécuté. 

!!! note "D'un point de vue sémantique"
    * `prenom` est un **argument** à l'extérieur de la fonction, au moment de son appel. On dit qu'on lui **passe** l'argument.
    
    * `prenom` est un **paramètre** à l'intérieur de la fonction.


On peut passer plusieurs arguments :

``` py
def saluer(prenom, nom):
    print(f'Bonjour {prenom} {nom}, ça va ?')

saluer('Arthur', 'Rouquan')
saluer('Leoš', 'Janáček')
saluer('Cho', 'Chikun')
```

Si vous ne passez qu'un argument, par exemple `#!python saluer('Bob')`, vous aurez droit à une erreur !

### Renvoyer/retourner une valeur

**Renvoyer** une valeur depuis une fonction se fait grâce au mot-clef `#!python return` :

``` py
def double(nombre):
    return nombre * 2

print(double(4))
```

### Syntaxe générale

``` py
def nom_de_la_fonction(argument1, argument2, ...):
    # intructions
    return valeur_renvoyee
```

## Quelques exemples démonstratifs

### Test de parité -- Lisibilité

Pour tester si un nombre est pair, on regarde si le reste de la division de celui-ci par 2 vaut 0. On peut définir une fonction `est_pair` qui nous renvoie `True` si le nombre est pair, `False` sinon :

``` py
def est_pair(nombre):
    return nombre % 2 == 0
```

Ici, on **nomme** explicitement l'intention du code. Ces deux codes sont strictement identiques, mais le dernier est beaucoup plus clair !

``` py
if n % 2 == 0:
    # blabla
```

``` py
if est_pair(n):
    # blabla
```

Qui plus est, il existe une manière plus rapide de tester la parité d'un entier. S'il faudrait alors modifier chacune des égalités dans le premier cas, dans le second cas il suffirait de modifier juste le corps de la fonction `est_pair`.


### Somme des entiers -- Généricité

Imaginons le programme qui calcule la somme des entiers naturels jusqu'à 1000 :

``` py
s = 0
for i in range(1, 1001):
    s += i
print(s)
```

Transformons-le en une fonction. Un des principes clefs de la programmation est de **généraliser** ses fonctions, de les rendre génériques. Ici, l'objectif est de pouvoir utiliser cette fonction quand on en aura besoin, et éventuellement pour calculer la somme des entiers jusqu'à n'importe quelle valeur $n$, pas nécessairement 1000. Cette valeur $n$ va être le paramètre de la fonction. Et on ne veut plus afficher la somme, mais que cette somme soit renvoyée par la fonction (pour l'affecter à une variable, ou bien pour l'afficher ensuite).

``` py
def somme(n):
    s = 0
    for i in range(1, n + 1):
        s += i
    return s
```

Si l'on exécute :

``` py
>>> somme(42)
903
```

## Quelques subtilités

### S'éjecter du code avec `#!python return`

L'emploi du mot-clef `#!python return` provoque une éjection du code : tout ce qui suit cette instruction ne sera pas exécuté.

``` py
def bidon(n):
    if n % 2 == 0:
        print(f'Ce texte est affiché car {n} est pair.')
        return 'Bravo !'
    else:
        return 'Mauvais choix de nombre...'
    print('Ce texte ne sera jamais affiché.')

print(bidon(12))
```

### Respecter l'ordre des arguments

``` py
def repete_lettres(chaine, nombre):
    sortie = ''
    for caractere in chaine:
        sortie += nombre * caractere
    return sortie
```

Il faut alors respecter l'ordre des paramètres lors de l'appel de la fonction :

``` py
>>> repete_lettres('NSI', 3)
'NNNSSSIII'
>>> repete_lettres(3, 'NSI')
Traceback (most recent call last):
File "<pyshell>", line 1, in <module>
File "", line 3, in repete_lettres
    for lettre in chaine:
TypeError: 'int' object is not iterable
```

### La portée des variables

#### Variables locales

Les paramètres d'une fonction, ainsi que les variables déclarées à l'intérieur du corps de la fonction **n'existent que dans le corps de cette fonction**. Il n'est pas possible d'y faire référence depuis une autre instruction, et ce même si la fonction a été appelée.


``` py
def aire_rectangle(longueur, largeur):
    aire = longueur * largeur
    return aire
```

``` py
>>> aire_rectangle(6, 3)
18
>>> longueur
NameError: name 'longueur' is not defined
>>> aire
NameError: name 'aire' is not defined
```

#### Variables globales

Même si c'est possible, il est fortement recommandé de ne pas utiliser dans le corps d'une fonction des variables définies à l'extérieur de cette fonction. En effet, si plusieurs fonctions agissent sur ces variables, le programme peut aboutir à des valeurs ou des comportements non prévus. On parle alors d'**effet de bord**.

=== "Pas bien"
    ``` py
    a = 5
    def fonction_idiote(n):
        return n + a

    fonction_idiote(1)
    ```

=== "Bien"
    ``` py
    a = 5
    def fonction_idiote(n, m):
        return n + m

    fonction_idiote(1, a)
    ```

## Correction des exercices

### Exercice 1 -- Maximum

!!! abstract "Énoncé"
    Écrire une fonction `maximum` qui prend deux nombres en paramètres et qui renvoie le plus grand des deux.
    
=== "Programme attendu"
    ``` py
    def maximum(x, y):
        if x > y:
            return x
        else:
            return y
    ```

    Exemple d'utilisation :
    
    ``` py
    >>> maximum(17, 38)
    38
    >>> maximum(120, 2)
    120
    ```

=== "Avec une condition ternaire"

    ``` py
    def maximum(x, y):
        return x if x > y else y
    ```

    !!! note "Opérateur ternaire"    
        L'**opérateur ternaire** permet de simplifier la syntaxe de certaines opérations conditionnelles :
        ```py
        on_true if condition else on_false
        ```
        Ici la valeur `on_true` est renvoyée si `condition` est évaluée à `True`, `on_false` sinon.

### Exercice 2 -- Maximum entre 3 nombres

!!! abstract "Énoncé"
    Écrire une fonction `maximum3` qui prend trois nombres en paramètres et qui renvoie le plus grand des trois.

=== "Programme attendu"
    ``` py
    def maximum3(x, y, z):
        if x > y and x > z:
            return x
        elif y > z:
            return y
        else:
            return z
    ```

    On effectue au plus 2 conditions ici. En effet, si `x > y` est faux alors Python ne va évaluer le second membre de l'opérateur `and`, à savoir `x > z` (cette optimisation est appelée *short-circuit evaluation* en anglais), car la condition sera quoiqu'il arrive fausse.

=== "En réutilisant la fonction précédente"
    ``` py
    def maximum3(x, y, z):
        if x > y and x > z:
            return x
        else:
            return maximum(y, z)
    ```

    En utilisant une condition ternaire :

    ``` py
    def maximum3(x, y, z):
        return x if x > y and x > z else maximum(y, z)
    ```

=== "Ou encore..."
    ``` py
    def maximum3(x, y, z):
        return maximum(maximum(x, y), maximum(y, z))
    ```

    Mais ce programme n'est pas efficient, on effectue toujours 3 comparaisons. En effet, chaque fontion `maximum` fera une comparaison.

!!! warning "Analyse de vos solutions"
    Une remarque concernant ce genre de solutions :

    ``` py
    def maximum3(x, y, z):
        if maximum(x, y) > z:
            return maximum(x, y)
        else:
            return z
    ```

    Ici, `#!python maximum(x, y)` est calculé une deuxième fois inutilement si la condition est vraie. Imaginez si la fonction `maximum` prenait 10 minutes à s'exécuter... une solution serait de stocker le résultat de cette fonction :

    ``` py
    def maximum3(x, y, z):
        max_xy = maximum(x, y)
        if max_xy > z:
            return max_xy
        else:
            return z
    ```

 
### Exercice 3 -- Compter le nombre de voyelles

!!! abstract "Énoncé"
    Écrire une fonction `nombre_voyelles` qui prend une chaîne de caractères (minuscules) en paramètre et renvoie le nombre de voyelles qu'elle contient.

=== "Avec l'opérateur d'appartenance `in`"
    ``` py
    def nombre_voyelles(chaine):
        nombre_voyelles = 0
        for caractere in chaine:
            if caractere in 'aeiouy':
                nombre_voyelles += 1
        return nombre_voyelles
    ```

=== "Méthode naïve"
    ```py
    def nombre_voyelles(chaine):
        nombre_voyelles = 0
        for l in chaine:
            if l == 'a' or l == 'e' or l == 'i' or l == 'o' or l == 'u' or l == 'y':
                nombre_voyelles += 1
        return nombre_voyelles
    ```

=== "Flex"
    ```py
    def nombre_voyelles(chaine):
        return sum(1 for caractere in chaine if caractere in 'aeiouy')
    ```

    Ici, on utilise une **expression génératrice** avec un filtre que l'on agrège avec `#!python sum`. 


### Exercice 4 -- Factorielle

!!! abstract "Énoncé"

    Écrire une fonction `factorielle` qui prend un nombre $n$ en paramètre et renvoie $𝑛!$, c'est-à-dire le produit des termes de 1 à $n$  (inclus) :
    $$
        n! = \prod_{i=1}^n i
    $$

=== "Programme attendu"
    ```py
    def factorielle(n):
        produit = 1
        for terme in range(2, n + 1):
            produit *= terme
        return produit
    ```

=== "Version de Lucas"
    ```py
    def factorielle(n):
        for terme in range(2, n):
            n *= terme
        return n
    ```

=== "Version récursive"
    ```py
    def factorielle(n):
        return 1 if n == 1 else n * factorielle(n - 1)
    ```

    Une fonction est dites **récursive** si elle s'appelle elle-même. Ici notre **condition d'arrêt** de la récursion est le cas de base $n = 1$.

### Exercice 5 -- Leet Speak

!!! abstract "Énoncé"

    Écrire une fonction `leet_speak` qui prend en paramètre une chaine de caractères (en minuscules) et qui renvoie sa traduction en « Leet Speak ». C'est-à-dire la même chaîne de caractères en ayant remplacé :
        
    * les a par des 4
    
    * les e par des 3

    * les s par des 5

    * les i par des 1

    * les o par des 0

=== "Programme attendu"
    ```py
    def leet_speak(chaine):
        resultat = ''
        for caractere in chaine:
            if caractere == 'a':
                resultat += '4'
            elif caractere == 'e':
                resultat += '3'
            elif caractere == 's':
                resultat += '5'
            elif caractere == 'i':
                resultat += '1'
            elif caractere == 'o':
                resultat += '0'
            else:
                resultat += caractere
        return resultat
    ```

=== "Avec un dictionnaire"
    ```py
    def leet_speak(chaine):
        table = {
            'a': '4',
            'e': '3',
            's': '5',
            'i': '1',
            'o': '0'
        }
        resultat = ''
        for caractere in chaine:
            if caractere in table:
                resultat += table[caractere]
            else:
                resultat += caractere
        return resultat
    ```


=== "Flex"
    ```py
    def leet_speak(chaine):
        table = {'a': '4', 'e': '3', 's': '5', 'i': '1', 'o': '0'}
        return ''.join([table[l] if c in table else c for c in chaine])
    ```

    La variable `table` contient un **dictionnaire**, c'est une structure de données qui permet d'associer des clés avec des valeurs. Par exemple la clé `#!python 'a'` est associée à la valeur `#!python '4'`. Ainsi `#!python table['a']` renvoie la valeur `#!python '4'`. La seconde ligne utilise une **compréhension de liste** pour générer une liste de caractères que l'on transforme en une chaîne de caractères avec la méthode `join`.


### Exercice 6 -- Test de primalité

!!! abstract "Énoncé"

    Écrire une fonction `est_premier` qui prend un entier positif en paramètre et renvoie `True` si ce nombre est premier, `False` sinon.

=== "Programme attendu"
    ```py
    def est_premier(n):
        if n <= 1: # cas de base
            return False
        
        for i in range(2, n):
            if n % i == 0:
                return False
        return True
    ```

=== "Flex"
    ```py
    def est_premier(n):
        return False if n <= 1 else all(n % i != 0 for i in range(2, n))
    ```

    La fonction `#!python all` renvoie `True` si tous les éléments de l'itérable (ici une expression génératrice) donnée sont `True`. Sinon, elle renvoie `False`. On utilise ensuite une condition ternaire pour séparer le cas de base du cas général.

### Exercice 7 -- Un nombre presque parfait

!!! abstract "Énoncé"

    Écrire une fonction `est_parfait` qui prend un nombre en paramètre et renvoie `True` si ce nombre est parfait, `False` sinon.

!!! info "Définition"
    Un nombre est parfait si la moitié de la somme de ses diviseurs. Ainsi 6 est un nombre parfait car ses diviseurs entiers sont 1, 2, 3 et 6, et il vérifie bien 6 = (1 + 2 + 3 + 6) / 2.

=== "Programme attendu"
    ```py
    def est_parfait(n):
        somme_diviseurs = 0
        for i in range(1, n + 1):
            if n % i == 0:
                somme_diviseurs += i
        return n == somme_diviseurs / 2
    ```

=== "Flex"
    ```py
    def est_parfait(n):
        return n == sum(i for i in range(1, n) if n % i == 0)
    ```

### Exercice 8 -- Base décimal vers base binaire

!!! abstract "Énoncé"

    Écrire une fonction `binaire` qui prend un nombre en base 10 en paramètre et renvoie sa représentation binaire sous forme d'une chaîne de caractères.

=== "Programme attendu"
    ```py
    def binaire(n):
        if n == 0: # cas de base
            return '0'
        
        resultat = ''
        while n != 0:
            reste = n % 2
            resultat = str(reste) + resultat
            n //= 2
        return resultat
    ```

    On "traduit" l'algorithme des divisions successives par 2 que l'on a vu en cours en lignes de code Python. A chaque itération on **concatène** le reste et notre résultat dans le bon sens.

=== "Avec une liste"
    ```py
    def binaire(n):
        if n == 0:
            return '0'
        
        bits = []
        while n != 0:
            bits.append(str(n % 2))
            n //= 2
        return ''.join(reversed(bits))
    ```

    On ajoute au fur et à mesure les bits trouvés dans une liste. On renverse les élements avec la fonction `reversed` (ou avec la méthode `.reverse()`) puis on convertit notre liste de caractères en une chaîne de caractères avec la méthode `.join` (ou avec une simple boucle for).


=== "Méthode des soustractions"
    ```py
    def plus_grande_puissance_2(n):
        p = 0
        while 2 ** p <= n:
            p += 1
        return p - 1


    def binaire(n):
        if n == 0:
            return '0'

        puissances = []
        while n != 0:
            p = plus_grande_puissance_2(n)
            puissances.append(p)
            n -= 2 ** p
        
        bits = ['0'] * (puissances[0] + 1)
        for p in puissances:
            bits[p] = '1'
        return ''.join(reversed(bits))
    ```

    Une première approche naïve. A chaque itération, on détermine la plus grande puissance de 2 `p` et on la soustrait de notre nomnbre `n`. Une fois toutes les puissances trouvées, on détermine le nombre binaire associé à ces puissances.

=== "Méthode des soustractions optimisée"
    ```py
    def plus_grande_puissance_2(n):
        p = 0
        while 1 << p <= n:
            p += 1
        return p - 1


    def binaire(n):
        if n == 0:
            return '0'

        p = plus_grande_puissance_2(n)
        n -= 1 << p
        bits = ['0'] * p + ['1']

        while n != 0:
            p -= 1
            while 1 << p > n:
                p -= 1
            n -= 1 << p
            bits[p] = '1'
        
        bits.reverse()
        return ''.join(bits)
    ```

    L'opérateur *shift* `x << y` permet de décaler le nombre `x` de `y` bits vers la gauche. Ainsi, `2 ** p` est équivalent à `1 << p`, mais empiriquement plus rapide. Cette fois-ci on calcule la plus grande puissance de 2 une seule fois, puis dans la boucle principale on décrémente cette puissance au fur et à mesure.

=== "Comparaison"
    <div style="text-align:center"><img src="../images/binary.svg" /></div>

### Exercice 9 -- Base décimale vers base $b$

!!! abstract "Énoncé"
    Écrire fonction `convertir` qui prend un nombre  𝑛  en base 10 et un nombre $𝑏 \leq 16$ en paramètres et renvoie la représentation du nombre $n$ en base $b$ sous forme d'une chaîne de caractères.

=== "Programme attendu"
    ```py
    def convertir(n, base):
        if n == 0:
            return '0'

        resultat = ''
        while n != 0:
            reste = n % base

            if reste == 10:
                chiffre = 'A'
            elif reste == 11:
                chiffre = 'B'
            elif reste == 12:
                chiffre = 'C'
            elif reste == 13:
                chiffre = 'D'
            elif reste == 14:
                chiffre = 'E'
            elif reste == 15:
                chiffre = 'F'
            else:
                chiffre = str(reste)

            resultat = chiffre + resultat
            n //= base

        return resultat
    ```

=== "Plus malin"
    ```py
    def convertir(n, base):
        resultat = ''
        while n != 0:
            resultat = '0123456789ABCDEF'[n % base] + resultat
            n //= base
        return resultat or '0'
    ```

    Ici, on utilise le fait qu'une chaîne de caractères est en fait un tableau de caractères (immutable). L'opérateur d'accès à l'index `[]` fonctionne ! Petit tricks à la fin avec **l'opérateur Elvis**... je laisse votre curiosité vous guider sur Wikipédia ;) `#!python return resultat or '0'` est équivalent à `#!python return resultat if resultat != '' else '0'`. Il faut croire que l'opérateur logique `or` ne renvoie pas que des booléens...
