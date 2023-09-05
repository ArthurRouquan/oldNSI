# Opérations sur les tables

Pour tous ces exercices, on s'appuiera sur [cette table](harrypotter.csv). Pour rappel le code à adapter pour importer un fichier csv :

```py
import csv

file = open('harrypotter.csv', 'r')
table_hp = list(csv.DictReader(file, delimiter=','))
```

Ici, on s'intéresse aux **opérations classiques** sur les tables.

## Recherche de valeurs

!!!example "Appartient à"
    On souhaite d'abord vérifier qu'une valeur appartient à une table ou non. Pour cela il suffit de parcourir les enregistrements de la table et vérifier que la valeur recherchée est une valeur de l'enregistrement.

    ```py
    def appartient(valeur, table: list) -> bool:
        '''
        Renvoie True si et seulement **si** la valeur apparaît dans les valeurs de la table.
        '''
        for e in table: # e pour enregistrement
            for v in e. ... () : # v pour ...
                if v == ...
                    return ...
        return ...
    ```

    1. Compléter ce code.

    2. Simplifier ce code en utilisant l'opérateur d'appartenance `#!python in`.

    3. Que renvoie `#!python appartient('Harry Potter', table_hp)` ?


!!!example "Appartient à (suivant un champ)"
    Adapter la fonction précédente pour qu'elle prenne en paramètre un champ et qu'elle recherche si la valeur est présente pour le champ précisé. La signature de la fonction :

    ```py
    def appartient(valeur, champ: str, table: list) -> bool:
    ```


!!!example "Recherche"

    On souhaite désormais récupérer certaines données si la valeur recherchée est trouvée.

    Adapter la fonction précédente pour qu'elle renvoie la liste des valeurs correspondant à un second champ (de retour) lorsque la valeur cherchée est trouvée (dans un premier champ de recherche). La signature de la fonction :

    ```py
    def recherche(valeur, champ1: str, champ2: str, table: list) -> list:
    ```

    Un exemple :

    ```py
    >>> recherche('Hufflepuff', 'House', 'Character Name', table_hp)
    ['Cedric Diggory', 'Nymphadora Tonks', 'Susan Bones', 'Pomona Sprout', 'Leanne', 'Justin Finch-Fletchley', 'Zacharias Smith', 'Ernest Macmillan']
    ```

## Agrégation

L'**agrégation** est une fonction qui transforme une liste d'éléments en une unique valeur. Vous connaissez déjà moults fonctions d'aggrégation : **somme** d'une liste, **moyenne** d'une liste, **maximum**/**minimum** d'une liste, **nombre d'éléments** d'une liste etc.


!!!example "Aggrégation avec condition"
    Il est bien utile d'armer une telle fonction avec une **condition**. Par exemple, écrivez la fonction `compte` qui prend en paramètre une valeur, un champ et une table et renvoie le nombre d'occurences de la valeur dans le champ de la table.

    ```py
    >>> compte('Female', 'Gender', table_hp)
    42
    ```

## Sélection

Une **sélection** revient à créer une nouvelle table en extrayant les enregistrements d'une table existante vérifiant une certaine condition. 

Par exemple, on pourrait sélectionner les personnages de Serdaigle (Ravenclaw) :

| Character ID | Character Name     | Species             | Gender | House     | Patronus | Wand (Wood) | Wand (Core)        |
| ------------ | ------------------ | ------------------- | ------ | --------- | -------- | ----------- | ------------------ |
| 25           | Luna Lovegood      | Human               | Female | Ravenclaw | Hare     |             |                    |
| 28           | Gilderoy Lockhart  | Human               | Male   | Ravenclaw |          | Cherry      | Dragon Heartstring |
| 38           | Sybill Trelawney   | Human               | Female | Ravenclaw |          | Hazel       | Unicorn Hair       |
| 39           | Moaning Myrtle     | Ghost               | Female | Ravenclaw |          |             |                    |
| 41           | Quirinus Quirrell  | Human               | Male   | Ravenclaw |          | Alder       | Unicorn Hair       |
| 43           | Garrick Ollivander | Human               | Male   | Ravenclaw |          | Hornbeam    | Dragon Heartstring |
| 54           | Helena Ravenclaw   | Ghost               | Female | Ravenclaw |          |             |                    |
| 55           | Cho Chang          | Human               | Female | Ravenclaw | Swan     |             |                    |
| 59           | Filius Flitwick    | Human (Part-Goblin) | Male   | Ravenclaw |          |             |                    |
| 101          | Padma Patil        | Human               | Female | Ravenclaw |          |             |                    |
| 119          | Michael Corner     | Human               | Male   | Ravenclaw | Squirrel |             |                    |
| 124          | Marcus Belby       | Human               | Male   | Ravenclaw |          |             |                    |

Cela consiste donc à créer une liste en parcourant la table existante et en sélectionnant les enregistrements selon un critère : c'est exactement ainsi qu'on crée une **liste en compréhension avec filtre**.

La table précédente a été obtenu grâce à la ligne de code :

```py
table_serdaigle = [e for e in table_hp if e['House'] == 'Ravenclaw']
```

!!!example "Exercices sur la sélection"
    1. Créer la table des personnages d'espèce "Ghost"
    2. Créer la table des personnages féminins et de Gryffondor.
    3. Créer la table des personnages masculins dont le nombre de lettres de leur nom est pair.
 
## Projection

On peut également avoir à extraire d'une table certaines colonnes, c'est-à-dire seulement des données d'un ou plusieurs champs. On appelle également cette opération **projection**.


!!! note "Origine du mot projection"
    En mathématique, on parle de projection quand on passe d'une dimension à une dimension inférieure. Typiquement, on peut projetter un point dans l'espace (3D) sur un plan (2D). Dans le cas des tables, une colonne peut être vu comme une dimension. En effet, il n'est pas rare de traiter un enregistrement comme un simple vecteur. 


Il s'agit donc de créer une nouvelle table (liste) dont les enregistrements sont des dictionnaires qui ne contiennent que les couples champ: valeur des enregistrements de la table initiale pour les champs précisés (sous forme d'une liste par exemple).


!!!example "La projection en code"

    1. Compléter la fonction de projection:

        ```py
        def projection(table: list, liste_champs: list) -> list:
            '''
            Renvoie une table (liste de dictinonaires) des enregistrements de table ne contenant uniquement
            les champs appartenant à liste_champs.
            '''
            table_proj = ...
            for e in ...:
                table_proj.append({c: v for c, v in ... if ... })
            return ...
        ```

    2. Utiliser cette fonction pour créer une table en extrayant les colonnes "Character Name" et "House" de la table d'exemple.

## Tri

Il est parfois utile d'ordonner les enregistrements en les triant suivant les valeurs d'une ou plusieurs colonnes.

Par chance, Python est fourni avec deux fonctions de base pour trier une liste, la méthode `sort` et la fonction `sorted`. 

### Différence entre `sort` et `sorted`

 * La méthode `sort` tri **en place** la liste à laquelle on la lui applique. C'est-à-dire qu'elle **modifie directement** la liste. Elle ne renvoie rien.

 ```python
 >>> tab = [5, 4, 8, 1, 2, 3]
 >>> tab.sort()
 >>> tab
 [1, 2, 3, 4, 5, 8]
 ```

 * La fonction `#!python sorted` quant à elle renvoie une **nouvelle liste**, elle ne modifie pas la liste donnée en argument.

 ```python
 >>> tab = [5, 4, 8, 1, 2, 3]
 >>> sorted(tab)
 [1, 2, 3, 4, 5, 8]
 >>> tab
 [5, 4, 8, 1, 2, 3]
 ```

### Ordre de tri 

Pour ordonner de manière décroissante, on se sert du paramètre booléen `reverse`. 

```python
>>> sorted([5, 4, 8, 1, 2, 3], reverse=True)
[8, 5, 4, 3, 2, 1]
```

### Clé de tri

#### Tri des types classiques

* Les **nombres** (`#!python int`, `#!python float`) sont triées classiquement :

```py
>>> sorted([5, 4, 8, 1, 2, 3])
[1, 2, 3, 4, 5, 8]
```

* Les **chaînes de caractères** (`#!python str`) sont triées par ordre alphabétique :

```py
>>> sorted(['bateau', 'cuisine', 'arbre', 'dinde'])
['arbre', 'bateau', 'cuisine', 'dinde']
```

* Les **tableaux** (`#!python list`) ou les **p-uplets** (`#!python tuple`) sont triés par ordre **lexicographique** : on trie suivant le premier élément, puis le deuxième etc.

```py
>>> sorted([(1, 2), (2, 5), (1, 1), (1, 3), (0, 1), (2, 6)])
[(0, 1), (1, 1), (1, 2), (1, 3), (2, 5), (2, 6)]
```

#### Tri personnalisé

`#!python sort` et `#!python sorted` ont un paramètre nommé `key` qui permet de spécifier une **fonction qui est appelée sur chaque élément de la liste avant d’effectuer des comparaisons**. Ainsi, cette fonction renvoie la plupart du temps un nombre, car les entiers et flottants sont facilement comparables. Cette fonction est parfois appelée *projecteur*, car elle projette les élements de la liste vers une valeur comparable (typiquement `#!python int`). Sa signature usuel :

```py
def projecteur(element_de_la_liste) -> int:
```

!!! Check "Un premier exemple"

    Par exemple, on peut trier une liste de couples de nombre suivant le second nombre grâce à un projecteur  :

    ```py
    def second_proj(t: tuple) -> int:
        return t[1]
    ```

    ```py
    >>> tab = [(1, 2), (2, 5), (1, 1), (1, 3), (0, 1), (2, 2)]
    >>> sorted(tab, key=second_proj)
    [(1, 1), (0, 1), (1, 2), (2, 2), (1, 3), (2, 5)]
    ```

!!! Check "Un second exemple"

    Pour trier une liste de dictionnaires (*une table*), il faut nécessairement
    spécifier un projecteur pour obtenir des éléments comparables.
    En effet, deux dictionnaires sont par défaut incomparables.

    ```py
    releve =[{'Nom': 'Alice', 'Anglais': 17, 'Info': 18, 'Maths': 16},
             {'Nom': 'Bob',   'Anglais': 19, 'Info': 13, 'Maths': 14},
             {'Nom': 'Carol', 'Anglais': 15, 'Info': 17, 'Maths': 19}]
    ```

    On peut trier la table suivant la note d'informatique grâce au projecteur :

    ```py
    def info_proj(d: dict):
        return d['Info']
    ```

    Ce projecteur prend donc un dictionnaire (*un enregistrement*) et
    renvoie la valeur à la clé "Info" (*le champ "Info"*).

    ```py
    >>> sorted(releve, key=info_proj)
    [
        {'Nom': 'Bob',   'Anglais': 19, 'Info': 13, 'Maths': 14},
        {'Nom': 'Carol', 'Anglais': 15, 'Info': 17, 'Maths': 19},
        {'Nom': 'Alice', 'Anglais': 17, 'Info': 18, 'Maths': 16},
    ]
    ```

#### Exercices

!!!example "Trier suivant la moyenne général"

    On travaille avec la même table `releve` que précedemment.
    
    1. Ecrire le projecteur `moyenne_proj` qui permet de trier les enregistrements suivant la moyenne générale.

    2. En utilisant le paramètre `reverse`, trier la table `reverse` par ordre décroissant de moyenne générale.

!!!example "De retour à Poudlard"

    1. Trier la table `table_hp` selon le champ `Character Name`.

    2. Trier la table `table_hp` selon le champ `"House"`, **puis** `"Character Name"`. (on rappelle que Python sait trier par défaut des tuples...)

!!!example "Encore des projecteurs"
    On travaille maintenant sur la [table des pays](countries.csv). Il faudra écrire les bons projecteurs pour répondre aux questions suivantes :

    1. Afficher le nom des pays par ordre décroissant de superficie.

    2. Afficher les 10 pays les moins peuplés, dans l’ordre inverse de leur population, sous la forme (pays, population).

    3. Afficher les 8 pays possédant la plus grande densité de population, dans l’ordre inverse de densité, sous la forme (pays, densité). (attention aux conversions !)