# Tables de données

## Introduction et vocabulaire

La façon la plus naturelle et simple de structurer des données est de les organiser sous la forme d'une **table** : bulletins scolaires, extrait de compte bancaire, statistiques sportives etc. Un exemple de table :

| Nom        | Prénom   | Poste             | Taille | Poids |
| ---------- | -------- | ----------------- | ------ | ----- |
| Mbappé     | Kylian   | Attaquant         | 179    | 78    |
| Griezmann  | Antoine  | Attaquant         | 173    | 73    |
| Giroud     | Oliver   | Attaquant         | 192    | 92    |
| Lloris     | Hugo     | Gardien de but    | 188    | 78    |
| Tchouaméni | Aurélien | Milieu de terrain | 185    | 75    |
| Koundé     | Jules    | Défenseur         | 178    | 70    |

Le vocabulaire est le suivant :

* Une **table** est un ensemble d'**enregistrements**.

* Un enregistrement contient les **valeurs** correspondants aux **champs** (ou **attributs**, ou encore **descripteurs**) de la table.

Par exemple, dans la table précédente :

* `Nom`, `Prénom`, `Poste`, `Taille`, `Poids` sont des champs (comme Didier). On peut noter que chaque champ est défini par un **type** (entier, flottant, chaîne de caractères etc.). 
  
* Chaque ligne est un enregistrement. Il y a 6 enregistrements dans cet table.

* `Mbappé` est une valeur du champ `Nom` pour le premier enregistrement.

!!!info "En statistique mathématique"
    Il est aussi très courant de manipuler des tables en statistique mathématique. On alors parle de variables/caractères pour les champs, et d'individus/mesures pour les enregistrements. Beaucoup de termes différents pour parler de la même chose donc. Comme dirait Pierre Dac, *rien n'est plus semblable à l'identique que ce qui est pareil à la même chose*.

## Représentation d'une table en Python

### Représentation d'un enregistrement

Il existe deux manières communes de représenter un enregistrement. Puisqu'un tableau ne peux pas contenir des valeurs de différents types, un **p-uplet** (ou tuple) semble être une bonne première approche :

```py
enregistrement = ('Mbappé', 'Kylian', 'Attaquant', 179, 78)
```

Hélas, pour accéder aux valeurs de cet enregistrement, il est nécessaire d'utiliser des indices :

```py
>>> enregistrement[3]
179
```

On préférera alors utiliser un **p-uplet nommé** qui permet en quelque sorte de "nommer les indices" avec leur champ correspondant. Un p-uplet nommé se créer normalement en Python avec la classe `namedtuple`, mais pour des raisons pédagogiques on utilisera un simple **dictionnaire** qui fonctionne de la même manière :

```py
enregistrement = {
    'nom'    : 'Mbappé',
    'prénom' : 'Kylian',
    'poste'  : 'Attaquant',
    'taille' : 179,
    'poids'  : 78
}
```

Et donc si on veut accéder au champ `Taille` de la table :

```py
>>> enregistrement1['taille']
179
```

### Représentation d'une table

Une table est une collection d'enregistrements, donc on la représenter sous la forme d'une liste d'enregistrements, une **liste de p-uplet nommé** :

```py
table = [
    {'nom' : 'Mbappé', 'prénom' : 'Kylian', 'poste' : 'Attaquant', 'taille' : 179, 'poids' : 78 },
    {'nom' : 'Griezmann', 'prénom' : 'Antoine', 'poste' : 'Attaquant', 'taille' : 173, 'poids' : 73 },
    # etc.
]
```

## Fichiers CSV

<!-- ### Fichier texte tabulé

Comment enregistrer une table dans un fichier ? Il existe deux manières courantes. La première est de séparer les enregistrements par des **sauts à la ligne** et les valeurs par des **tabulations** dans un bête fichier texte :

```
"Mbappé"	"Kylian"	"Attaquant" 179	78
"Griezmann"	"Antoine"	"Attaquant" 173	73
"Giroud"    "Oliver"    "Attaquant" 192 92
```

On ajoute des guillemets autour des valeurs de type chaîne de caractères, car certaines d'entre elles pourraient contenir des sauts à la ligne (`\n`) ou des tabulation (`\ t`) qu'on ne voudrait pas confondre avec ceux structurant le fichier.

### Fichier CSV -->

Les tables sont fréquemment enregistrées dans des fichiers au format `.csv` (*comma separated values*). C'est un simple fichier texte où :

* La première ligne définit les champs.

* Chaque ligne correspond à un enregistrement.

* Les champs et les valeurs sont séparés par un *délimiteur*, généralement par une **virgule**.

* Les guillemets `"` peuvent être utilisés pour délimiter le contenu d'une châine de caractères.

Par exemple, le début de la table précédente s'écrirait comme :

```csv
Nom,Prénom,Poste,Taille,Poids
Mbappé,Kylian,Attaquant,179,78
Griezmann,Antoine,Attaquant,173,73
Giroud,Oliver,Attaquant,192,92
```

!!!example "Un autre exemple de délimiteur"
    * Télécharger  [ce fichier .csv](./pokedex.csv) et l'ouvrir avec LibreOffice Calc. Observer l'importance de préciser les délimiteurs.

    * L'ouvrir ensuite avec un éditeur de texte (notepad++) pour observer sa construction.

### Charger un fichier CSV avec Python

#### From scratch

Ouvrir un fichier en Python se fait grâce à la fonction `#!python open`. La méthode `#!python .readlines` permet ensuite de récupérer l'ensemble des lignes dans une liste.

```py
>>> fichier = open('pokedex.csv')
>>> lignes = fichier.readlines()
>>> lignes[0]
'No;Nom;Type;PV;Attaque;Défense;Vitesse;ASpé;DSpé;Talent;Nom US;code'
>>> lignes[6]
'6;Dracaufeu;feu,vol;78;84;78;100;109;85;Brasier,Force Soleil;Charizard;63266\n'
```
Il va falloir un peu travailler ces chaînes de caractères pour parvenir à des tuples/tuples nommés. La méthode `.split` appliquée à une chaîne de caractère permet de la 
scinder suivant un délimiteur donné en paramètre.

```py
>>> "oui bonjour ça va".split(' ')
['oui', 'bonjour', 'ça', 'va']
>>> chaine = "Un peu, trop, de virgules, non?"
>>> chaine.split(',')
['Un peu', ' trop', ' de virgules', ' non?']
```

La méthode `.strip` appliquée à une chaîne de caractère en renvoie une nouvelle sans les espaces, les tabulations et les retours à la ligne aux extremités.

```py
>>> chaine = "    oui   bonjour    \n"
>>> chaine.strip()
'oui   bonjour'
```

!!!example "Récupérer les champs"
    * Dans un nouveau script Python, copier le code suivant :
    ```py
    fichier = open('pokedex.csv', 'r', encoding = 'UTF-8') # 'r' pour lecture seule
    lignes = fichier.readlines()
    lignes = # à compléter
    champs = # à compléter
    ```

    * Ecrire le code pour supprimer le retour à la ligne `\n` à la fin de chaque ligne de la liste `lignes`. On générera une liste en compréhension.

    * Ecrire la code pour récupérer les champs (les clés de notre futur dictionnaire) sous la forme d'une liste de chaînes de caractères.  

Transformer un enregistrement en un p-uplet est plus subtil car il nécessaire de convertir certaines valeurs.

```py
>>> lignes[1]
'1;Bulbizarre;plante,poison;45;49;49;45;65;65;Engrais,Chlorophylle;Bulbasaur;77140'
>>> lignes[1].split(';')
['1', 'Bulbizarre', 'plante,poison', '45', '49', '49', '45', '65', '65', 'Engrais,Chlorophylle', 'Bulbasaur', '77140']
```

On peut manuellement convertir certaines valeurs dans son bon type :

```py
vals = lignes[1].split(';')
enregistrement = (int(vals[0]), vals[1], vals[2], int(vals[3]), int(vals[4]), int(vals[5]), int(vals[6]), int(vals[7]), int(vals[8]), vals[9], vals[10], int(vals[11]))
print(enregistrement)
```

Le code affiche :

```py
(1, 'Bulbizarre', 'plante,poison', 45, 49, 49, 45, 65, 65, 'Engrais,Chlorophylle', 'Bulbasaur', 77140)
```



!!!example "Récupérer les enregistrements"
    * Adapter ce code pour transformer tous les enregistrements de table en p-uplet.

    * Finalement, à partir des champs et des enregistrements, construire la liste des dictionnaires représentant la table.

!!!note "Une conversion un peu plus propre"
    Il peut être assez déconcertant de manipuler des fonctions comme des valeurs :

    ```py
    valeurs = lignes[1].split(';')
    types = [int, str, str, int, int, int, int, int, int, str, str, int]
    enregistrement = [t(v) for t, v in zip(types, valeurs)]
    ```

    Pour rappel, la fonction `#!python zip` permet d'itérer sur deux itérables en même temps.


Evidemment ce code ne fonctionnera que pour le fichier csv fourni. Pour plus de généricité, une piste serait de détecter automatiquement le type des valeurs.

#### Grâce à la bibliothèque `csv`

La bibliothèque `csv` permet de lire et d'écrire des fichiers csv rapidement. Par exemple, la fonction `DictReader` remplace tout notre code précédent :

```py
import csv

fichier = open('pokedex.csv', 'r', encoding='UTF-8')

table = csv.DictReader(fichier, delimiter=';')

table = list(table) # table est de type 'csv.DictReader', on la convertit ici en une liste de dictionnaires

print(table[0])

fichier.close() # fermeture du fichier
```

Le code affiche :

```py
{'No': '1', 'Nom': 'Bulbizarre', 'Type': 'plante,poison', 'PV': '45', 'Attaque': '49', 'Défense': '49', 'Vitesse': '45', 'ASpé': '65', 'DSpé': '65', 'Talent': 'Engrais,Chlorophylle', 'Nom US': 'Bulbasaur', 'code': '77140'}
```

La conversion des valeurs ne se fait hélas pas automatiquement. 