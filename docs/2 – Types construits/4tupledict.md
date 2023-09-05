# Tuples et Dictionnaires

[PDF de la présentation des deux structures de données](./tupledict.pdf)

## Tuple

On retient qu'un tuple (ou p-uplet) est une séquence **continue et ordonnée** d’éléments de types **possiblement différents**. C'est une structure de données **immutables** (qu'on ne peut modifier).

```py
# On construit un tuple avec des parenthèses
eleve = ('Michel', 'Dupont', 17, 175)

# On accède à un élément du tuple par son indice
print(eleve[0]) 

# Erreur ici, on ne peut pas modifier un tuple !
eleve[0] = 'Pierre'

# D'autres opérations classiques
t1 = (12, 34, 56)
t2 = (78, 90)

print(t1 + t2) # affiche (12, 34, 56, 78, 90)
print(t1 * 3) # affiche (12, 34, 56, 12, 34, 56, 12, 34, 56)

# "unpacking a tuple" ou "déballage d'un tuple", marche aussi pour les tableaux !
prenom, nom, age, taille = ('Michel', 'Dupont', 17, 175)
```


## Dictionnaire
Un dictionnaire une structure de données **non-ordonnée** qui permet une 
**association clé–valeur**.


```py
# Construction explicite d'un dictionnaire :
eleve = {
    "prénom": "Michel",
    "nom": "Dupont",
    "âge": 17,
    "taille": 175
}

# On accède à une valeur, grâce à sa clé :
print(eleve["prénom"])

# Modification d'une valeur :
eleve["age"] = 42

# Suppression d'une association :
eleve.pop("taille") # (note : ici, la méthode .pop renvoie la valeur associée à la clé, donc 175)

print(eleve.keys()) # ensemble des clés
print(eleve.values()) # ensemble des valeurs
print(eleve.items()) # ensemble des clés-valeurs

# parcours par clé 
for key in eleve:
    print(key, eleve[key])

# parcours par clé 
for key in eleve.keys():
    print(key, eleve[key])

# parcours par valeurs
for value in eleve.values():
    print(value)

# parcours par clé et valeurs
for key, value in eleve.items():
    print(key, value)
```

## Exerices

!!! example "Exercice 1"
    === "Énoncé"
        Soit le dictionnaire suivant :

        ```py
        pionniers = {
            1760: "Charles Babbage",
            1906: "Grace Murray Hopper",
            1912: "Alan Turing",
            1916: "Claude Shannon",
            1924: "Jean Bartik",
            1941: "Dennis Ritchie",
            1955: "Timothy J. Berners-Lee",
            1969: "Linus Torvalds",
            1977: "John Cena"
        }
        ```

        1. Identifier le type des clés et des valeurs du dictionnaire `pionniers`.

        2. Que renvoie pionniers[1912] ?

        3. Oups, j'ai fait une petite erreur. En fait, je voulais écrire "Linus B. Torvalds". Corrige ça !

        4. Ah décidement ! John Cena n'est pas un informaticien, tu peux l'enlever ? (méthode .pop)

        5. En fait "Charles Babbage" est né en 1761, peux-tu rectifier ça ?

        5. Ajouter la clé 1938 associée à la valeur "Donald Knuth".

        6. Ecrire le programme qui vérifie si la valeur "Bob l'Eponge" est dans le dictionnaire. 

        7. Ecrire le programme qui vérifie si la clé 1945 existe dans le dictionnaire.

        8. Ecrire le programme qui renvoie la moyenne des clés.



!!! example "Exercice 2 - Un dictionnaire de dictionnaires"
    === "Énoncé"
        ```py
        data = {
            "classe1": {
                "eleve1": {
                    "prénom": "Jean-Michel",
                    "nom": "Python",
                    "notes": {
                        "Maths": 12,
                        "NSI": 14
                    }
                }
            }
        }

        ```

        1. Afficher la valeur 'NSI' du dictionnaire data.


!!! example "Exercice 3"
    === "Énoncé"
        Soient les deux dictionnaires suivants :

        ```py
        produits = {
            'pomme': 0.5,
            'poire': 2.6,
            'orange': 1.5,
            'carotte': 0.8,
            'poireau': 0.6
        }

        arrivage = {
            'citron': 0.95,
            'oignon': 0.4,
            'banane': 1.1,
            'haricots': 0.75,
            'pêche': 1.2,
            'nectarine': 1.25,
        }
        ```

        1. De nouveaux produits arrivent en rayon. Ecrire le programme qui ajoute les
        produits de `arrivage` dans le dictionnaire `produits` !
        (ici, on recode la méthode .update)

        2. Ecrire le programme qui calcule la moyenne des prix des produits.

        3. Ecrire le programme qui détermine le plus coûteux des produits.


!!! example "Exercice 4"
    === "Énoncé"
        Soient les deux dictionnaires suivants :

        ```py
        employes = ['Pierre', 'Miriam', 'Paul', 'Charlotte', 'Jacques']
        defaut = {'poste': 'développeur', 'salaire': 2500}
        ```

        1. Ecrire le programme qui créer le dictionnaire qui utilisent les éléments de `employes` comme clé et `defaut` comme la valeur par défaut. (ici, on recode la méthode .fromkeys)

!!! example "Exercice 5"
    === "Énoncé"
        De la même manière que les listes, on peut générer des dictionnaires en compréhension. La syntaxe :

        ```py
        d = {clé:valeur for i in iterable}
        ```

        Par exemple, une solution pour le dernier exercice :

        ```py
        {e: defaut for e in employes}
        ```
        1. Ecrire une fonction `carres` qui prend en paramètre un entier n > 1 et renvoie un dictionnaire qui contient les associations (i: i * i) pour i de 1 à n. (exemple: carres(5) renvoie {1: 1, 2: 4, 3: 9, 4: 16, 5: 25})

!!! example "Exercice 6"
    === "Énoncé"
        Soit le dictionnaire et la liste suivants :
        ```py
        data = {
            "prénom": "Bob",
            "age": 25,
            "taille": 160,
            "ville": "Lima"
        }

        cles = ["prénom", "taille"]
        ```

        1. Ecrire un programme pour créer un nouveau dictionnaire en extrayant les clés `cles` du dictionnaire `data` de deux manières différentes (avec une boucle, et en compréhension).

        2. Ecrire un programme qui supprime les clés `cles` du dictionnaire `data`.
