# La boucle while

Lorsqu'on souhaite répéter une série d'instructions plusieurs fois d'affilé, les boucles sont l'outil adpaté. Il en existe deux types en Python, la boucle bornée `for` (pour) et la boucle non-bornée `while` (tant que). Sa syntaxe est la suivante :

``` py
while condition_est_vraie:
    instruction1
    instruction2
    instruction3
    ...
```
Tant que la condition est **vraie**, alors le bloc **indenté** est exécutée. La condition est vérifiée en **entrée** de la boucle, les instructions peuvent être donc totalement ignorées. La condition est réévaluée à la fin du bloc d'instructions indenté.

!!! note "Indentation"
    C'est le décalage par rapport à la marge - qu'on appelle indentation - qui détermine quelles sont les instructions à répéter !
    
## Quelques exemples

### Un premier exemple

Si l'on exécute ce programme :

``` py
x = 1
while x < 10:
    print('x a pour valeur', x)
    x *= 2  # Syntaxe abrégée pour x = x * 2
print('Fin')
```

On obtient la sortie :

```
x a pour valeur 1
x a pour valeur 2
x a pour valeur 4
x a pour valeur 8
Fin
```

Que vaut `x` à la fin de la boucle ?

### Un exemple un peu utile

> Combien de fois doit-on plier une feuille de papier pour que son épaisseur dépasse la hauteur de la Tour Eiffel (324 m) ?

On suppose une feuille de papier classique, d'épaisseur de 0.1 mm. Plier la feuille en deux revient à multiplier son épaisseur par deux.

``` py
epaisseur = 0.0001
nombre_pliages = 0

while epaisseur < 324:
    epaisseur = 2 * epaisseur
    nombre_pliages += 1

print("Il faut", nombre_pliages, "pliages.")
```

## Quelques précautions

!!! Warning "Boucle infinie"
    La boucle while est une boucle non-bornée, elle peut donc être infinie. Par exemple :

    ``` py
    toto = 1
    while toto < 10:
        toto = 2
        print('Encore un tour...')
    print('Fin')
    ```

!!! Warning "Pas d'entreé dans la boucle"
    Parfois la condition est fausse dès le début, le code de la boucle sera donc ignorée :

    ``` py
    i = 1
    while i >= 1:
        i += 1
        print('Ce texte ne sera jamais affiché.')
    print('Fin')
    ```

    C'est parfois un effet souhaité dans certains algorithmes.

!!! success "Conseils"
    
    * Toujours traduire while en "tant que" pour mieux raisonner sur la condition.

    * Raisonner sur les bornes extrêmes de votre condition. Que vaudra ma condition au tout début (juste avant la boucle) ? Et à la toute fin (dernière itération) ?
