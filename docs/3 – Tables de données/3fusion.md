# Fusion de tables

Dans la vie réelle, une base de données se compose de **plusieurs** tables de données plus ou moins reliées entre-elles. Parfois deux tables partagent un même champ qui va nous permettre de réaliser une fusion de ces tables, c'est l'opération de **jointure**.

## Un premier exemple

Par exemple, présentons deux tables :

| Nom            | Espèce | Force | Statut        |
| -------------- | ------ | ----- | ------------- |
| Dark Vador     | Humain | oui   | Sith          |
| Obi-Wan Kenobi | Humain | oui   | Jedi          |
| R2-D2          | Droïde | non   | Astromécano   |
| Rey            | Humain | oui   | Jedi          |
| Han Solo       | Humain | non   | Contrebandier |
| Leia Organa    | Humain | oui   | Sénatrice     |
| C-3PO          | Droïde | non   | Protocole     |
| Luke Skywalker | Humain | oui   | Jedi          |
| Padmé Amidala  | Humain | non   | Sénatrice     |
| Dark Sidious   | Humain | oui   | Sith          |

| Nom               | Affiliation |
| ----------------- | ----------- |
| Dark Vador        | Empire      |
| Obi-Wan Kenobi    | République  |
| R2-D2             | République  |
| Rey               | Rébellion   |
| Han Solo          | Rébellion   |
| Grand Moff Tarkin | Empire      |
| Leia Organa       | Rébellion   |
| C-3PO             | République  |
| Luke Skywalker    | Rébellion   |
| Padmé Amidala     | République  |
| Dark Sidious      | Empire      |

Ces deux tables partagent le même champ "Nom", on peut donc les fusionner sur ce champ. C'est-à-dire construire une nouvelle table qui contient les valeurs des deux tables ( à condition donc qu'elles possèdent un champ commun) :

| Nom            | Espèce | Force | Statut        | Affiliation |
| -------------- | ------ | ----- | ------------- | ----------- |
| Dark Vador     | Humain | oui   | Sith          | Empire      |
| Obi-Wan Kenobi | Humain | oui   | Jedi          | République  |
| R2-D2          | Droïde | non   | Astromécano   | République  |
| Rey            | Humain | oui   | Jedi          | Rébellion   |
| Han Solo       | Humain | non   | Contrebandier | Rébellion   |
| Leia Organa    | Humain | oui   | Sénatrice     | Rébellion   |
| C-3PO          | Droïde | non   | Protocole     | République  |
| Luke Skywalker | Humain | oui   | Jedi          | Rébellion   |
| Padmé Amidala  | Humain | non   | Sénatrice     | République  |
| Dark Sidious   | Humain | oui   | Sith          | Empire      |


## Exercices

!!!note "Les deux tables à fusionner au format csv"
    [table1](table1.csv) et [table2](table2.csv).


!!!example "Fusion par jointure"
    La fusion par jointure consiste à :

    - créer une **table vide** qui accueillera les enregistrements contruits en fusionnant ceux des deux tables
    - **parcourir les enregistrements** de la première table
    - pour chacun des enregistrements de la deuxième  table, regarder si les enregistrements ont la même valeur pour le champ commun
    - si c'est le cas, créer une copie de l'enregistrement de la première table, à laquelle on ajoute les données (champ: valeur) de la deuxième table.

    ```python
    def fusion(table1: list, table2: list, champ: str) -> list:
        nouvelle_table = ...
        for e1 in table1: # e pour enregistrement
            for e2 in table2:
                if ...:
                    e = dict(e1)
                    for champ in ...:
                        if ...:
                            e[champ] = ...
                    nouvelle_table.append(...)
        return ...
    ```