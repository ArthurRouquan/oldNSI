# Représentation des entiers relatifs

## Le bit de signe

Dans la partie précédente, on a vu comment représenter un nombre entier **positif** en binaire. On s'interesse maintenant à la représentation des nombres entiers **relatifs**, et donc il faut étendre cette représentation aux entiers **négatifs**.

Une première idée est de réserver un bit d'information pour distinguer les nombres postifs des nombres négatifs, c'est le **bit de signe** : on dit que le nombre est **signé**. 



!!! question "Mais où placer ce bit ?"
    Ce bit se situe toujours devant, sur le bit de poids fort, il vaut :
    
    * 0 si positif $+$
   
    * 1 si négatif $-$

    De cette manière, si le nombre est positif, la représentation reste **inchangée**. À ce stade, 6 se code `110` et -6 en `1100`... mais `1100` représente aussi l'entier 14. Pour lever cette ambiguité, il faut alors spécifier explicitement la taille en bits de l'entier utilisé, ce qui indiquera alors la position du bit de signe.



!!! info "Les tailles courantes des entiers"
    La plupart des langages de programmation offrent souvent 4 types d'entiers codés sur 8, 16, 32 ou 64 bits (1, 2, 4 ou 8 octets) que l'on peut définir comme signé ou non suivant l'utilisation souhaitée. Par exemple en Julia, on peut déclarer une variable `UInt32` ou `Int32` (`U` pour Unsgined, non-signé).
    
    En python, le type `int` est un peu particulier car il utilise un nombre variable de bits pour stocker un entier, il n'y a donc aucun soucis à se faire. Pour s'en convaincre, il suffit d'essayer de calculer une très grosse puissance. 

L'entier 6 codé sur un octet signé s'écrit `0000 0110`, mais son opposé -6 ? `1000 0110` ? On peut faire mieux, car cette méthode de représentation a deux inconvénients :

* 0 peut être codé par `0000 0000` (+0) et `1000 0000` (-0), on perd donc une valeur possible.

* L'addition entre deux nombres relatifs ne fonctionne plus. On souhaite réutiliser les circuits électroniques d'addition binaire classiques !

Pour palier à ces problèmes, il existe une autre méthode qui consiste à représenter un entier relatif par un entier naturel, **le complément à 2**.

## Le complément à 2

* En binaire **non-signé** : Sur 8 bits, on représente les entiers positifs de 0 à 255 (inclus). Les entiers dont le bit de poids fort est égal à `0` sont compris entre 0 et 127, et ceux dont le bit de poids fort est égal à `1` sont compris entre 128 et 255. Rien de nouveau donc.

* En binaire **signé** : Sur 8 bits, les nombres de 0 à 127 conservent la même représentation (positifs, car avec 0 en bit de poids fort). L'astuce est d'ensuite représenter les entiers négatifs de -128 à -1 pour les nombres donc le bit de poids fort est égal à `1`.

![](./images/complément.png)


Et l'addition marche parfaitement 127 + (-128) = `0111 1111` + `1000 0000` = `1111 1111` = -1 ! On peut donc utiliser les mêmes circuits électroniques d'addition pour les soustractions.


!!! info "Un bit en moins ?"
    Si un octet peut coder un nombre entre 0 et 255, un octet signé lui ne pourra coder qu'un nombre entre -127 et 128 ! On represente cependant toujours le même nombre de valeurs, c'est-à-dire $2^n$ valeurs.


!!! note "Écrire la représentation binaire d'un entier négatif"
    Il existe une méthode rapide pour obtenir le complément à 2 d'un entier négatif :

    1. On code sa valeur absolue en binaire sur un nombre de bits spécifique préalablement choisi+ (8, 16, 32 etc.).

    2. On inverse tous les bits.

    3. On ajoute 1.

    Par exemple, le complément à 2 de $-42$. On a $(42)_{10} = (0010 1010)_2$. En inversant les bits, on obient $(1101 01001)_2$. Finalement, on ajoute 1 : $(1101 01010)_2 = (-42)_{10}$.

    Sauriez-vous justifier cette procédure ?


!!! Example "Exercice 1"
    Donner l'intervalle de nombres entiers relatifs que l'on peut représenter sur :

    1. 4 bits

    2. 16 bits

    3. 64 bits


!!! note "Intervalle"
    Avec $n$ bits, on peut représenter :

    * Les entiers positifs (non-signés) $[\![0, 2^n - 1]\!]$

    * Les entiers relatifs (signés, positifs et négatifs) $[\![- 2^{n-1}, 2^{n-1} - 1]\!]$

    On represente toujours $2^n$ valeurs.

!!! Example "Exercice 2"

    1. Convertir en complément à 2 les nombres 12 et -53.

    2. Effectuer l'addition en binaire de ces deux nombres, et vérifier que le résultat est correct.

!!! Example "Exercice 3"
    Quels sont les entiers relatifs dont la représentation binaire en complément à 2 (sur 8 bits) est:

    1. `01100111`

    2. `10011001`

!!! Example "Exercice 4"
    1. Vérifier que sur 8 bits, `10000000` représente -128 et `11111111` représente -1.
    
    2. Vérifier en effectuant l'addition en binaire, que 42 + (-42) = 0