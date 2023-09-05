# Compléments sur les listes

## Copie de listes

### Un exemple déroutant

```py
>>> listA = [1, 2, 3]
>>> listB = listA
>>> listA.append(7)
>>> listB
[1, 2, 3, 7]
>>> listB.append(8)
>>> listA
[1, 2, 3, 7, 8]
```

Tout se passe comme si les listes `listA` et `listB` étaient devenus des clones «synchronisés» depuis l'affectation `listB = listA`.

<iframe width="800" height="300" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=listA%20%3D%20%5B1,%202,%203%5D%0AlistB%20%3D%20listA%0AlistA.append%287%29%0AlistB.append%288%29%0A&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Les deux variables `listA` et `listB` désginent **la même liste**. Elles ne stockent pas la liste mais une **référence** de celle-ci ! Une variable est une référence vers une adresse en mémoire. Si deux variables font référence à la même adresse, alors elles sont totalement identiques : toute modification de l'une entraîne une modification de l'autre.

### Copier une liste proprement

Trois façons :

```py
>>> listA = [3, 4, 5]
>>> listB = listA.copy() 
>>> listC = list(listA)
>>> listD = listA[:] # slice
```

### Pourquoi une référence ?

Quand vous passez des arguments à une fonction, ils sont **copiés**. Vous ne manipulez pas l'argument en lui-même.

```py
def incremente(x):
    x += 1

a = 1
incremente(a)
print(a)
```

Cet exemple affiche `1`, car `a` n'est pas modifié par la fonction ! Pourtant quand je passe une liste :

```py
def ajoute_1(liste):
    liste.append(1)

t = [1, 2, 3, 4]
ajoute_1(t)
print(t)
```

Ici le programme affiche `[1, 2, 3, 4, 1]` ! La référence est bien copiée, mais elle réfere toujours à la liste en mémoire !
Ainsi, manipuler `t` ou le paramètre `liste` revient à manipuler la même liste.  Une réference correspond à une adresse dans la mémoire, elle est stockée sur 32 ou 64 bits suivant votre machine.

Copier une liste est coûteux, c'est pour cela qu'on préfère les passer **par référence** (Python le fait automatiquement) au lieu de les passer par copie. Lorsque vous manipulez de gros objets (listes, matrices, dictionnaires, ensembles etc.) les variables que vous utilisez sont des références et non pas l'objet en lui-même.

## Les slices

Encore du **sucre syntaxique**. Cela permet de sélectionner rapidement une partie du tableau :

### Version simple

```py
tableau[debut:fin]
```

```py
>>> t = [2, 5, 8, 4, 1, 14, 54, 0]
>>> t[2:6]
[8, 4, 1, 14]
>>> t[0:3]
[2, 5, 8]
>>> t[0:len(t)]
[2, 5, 8, 4, 1, 14, 54, 0]
```

Attention une slice renvoie une copie de votre liste, elle ne la modifie pas !

Si on ne spécifie pas `debut`, alors on part du début de la liste !

```py
>>> t[:3]
[2, 5, 8]
>>> t[:1]
[2]
```

Et si on ne spécifie pas `fin`, on sélectionne jusqu'à la fin de la liste !

```py
>>> t[5:]
[14, 54, 0]
>>> t[2:]
[8, 4, 1, 14, 54, 0]
```

Et si on ne spécifie ni `debut`, ni `fin` :

```py
>>> t[:]
[2, 5, 8, 4, 1, 14, 54, 0]
```

On renvoie directement tout le tableau ! Ici, `#!python t[:]` renvoie bien une **copie** de votre liste !

!!! example "Exercice 1"
    === "Énoncé"
        Soit le tableau suivant :
        ```py
        t = ['pif', 'paf', 'pouf', 'pouet', 'oh', 'chien', 'chat', 'lapin', 'ah', 'kiwi', 'pomme']
        ```

        1. Sans utiliser une slice, extraire les élements de l'indice 5 à l'indice 7 (inclus) dans une nouvelle liste `animaux`.

        2. Proposez une alternative avec une slice.

!!! example "Exercice 2"
    === "Énoncé"
        Soit le tableau suivant :
        ```py
        t = [2, 5, 8, 4, 1, 14, 54, 0]
        ```
        Comment faire la somme des 4 premiers termes sans utiliser le parcours par indice ?



### Avec un pas

On peut spécifier le pas :

```py
tableau[debut:fin:pas]
```

Par exemple, je peux sélectionner un élement sur deux avec :

```py
>>> t = [2, 5, 8, 4, 1, 14, 54, 0]
>>> t[::2]
[2, 8, 1, 54]
```

Je peux même renverser une liste en mettant un pas à -1 :

```py
>>> t = [2, 5, 8, 4, 1, 14, 54, 0]
>>> t[::-1]
[0, 54, 14, 1, 4, 8, 5, 2]
```

Mais ici, on préfera la méthode `.reverse` (modifie la liste) ou la fonction `reversed` (renvoie une nouvelle liste) qui sont beaucoup plus explicites et claires.

!!! example "Exercice 3"
    === "Énoncé"
        Soit le tableau suivant :
        ```py
        t = [2, 5, 8, 4, 1, 14, 54, 0]
        ```

        Ici, on n'utilise ni les slices, ni la méthode `.reverse` ou fonction `reversed`.

        1. Comment renverser la liste `t` dans une autre liste `t_renverse` ?

        2. Comment renverser la liste `t` en place, c'est-à-dire sans créer une nouvelle liste, en modifidant directement `t` ?

## D'autres méthodes utiles (Hord-Programme)

Ces méthodes/fonctions ne sont pas à apprendre, car vous pouvez toutes les coder avec des `if`, `for` etc. Elles sont justes utiles à connaître car très souvent utilisées.


```py
>>> t = ["Bleu", "Rouge", "Blanc", "Noir"]


>>> t.insert(1, "Vert") # insertion à l'idice
>>> t
['Bleu', 'Vert', 'Rouge', 'Blanc', 'Noir']


>>> t2 = ['pomme', 'poire', 'orange']
>>> t.extend(t2) # extension avec une autre liste (modifie t)
>>> t
['Bleu', 'Vert', 'Rouge', 'Blanc', 'Noir', 'pomme', 'poire', 'orange']

>>> t + ["oui", "non", "?"] # Idem, mais on renvoie une nouvelle liste (on ne modifie pas t) !
['Bleu', 'Vert', 'Rouge', 'Blanc', 'Noir', 'pomme', 'poire', 'orange', 'oui', 'non', '?']


>>> t.count('non') # renvoie le nombre d'occurences de l'élément donné
1


>>> t = [2, 10, 5, 8, 4, 1, 14, 54, 0]
>>> t.sort() # tri la liste de nombres
>>> t
[0, 1, 2, 4, 5, 8, 10, 14, 54]

>>> t = [2, 10, 5, 8, 4, 1, 14, 54, 0]
>>> sorted(t) # tri, mais ne mofidie pas t
[0, 1, 2, 4, 5, 8, 10, 14, 54]
>>> t
[2, 10, 5, 8, 4, 1, 14, 54, 0]


>>> liste = []
>>> if len(liste) == 0: # pour vérifier si une liste est vide
        print("Votre liste est vide !")
Votre liste est vide !

>>> if not liste: # pour vérifier si une liste est vide
        print("Votre liste est vide !")
Votre liste est vide !
```


