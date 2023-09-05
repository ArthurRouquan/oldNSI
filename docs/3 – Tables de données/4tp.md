# TP Pokédex

Dans tout ce TP, on manipulera la table contenue dans [ce fichier](pokedex.csv). 

1. Commencez par ouvrir le fichier avec l'éditeur de texte. Contrôlez le délimiteur utilisé.
2. Importez les données dans une table.
3. Existe-t-il un pokemon dont le nom est `Apireine` ? Si oui, quel est son `'Nom US'`?
4. Modifiez la table pour ne conserver que les champs: 
    ```python
    'Nom', 'Type', 'PV', 'Attaque', 'Défense', 'code'
    ```
5. Combien de pokemons ont une `'Attaque'` supérieure ou égale à 50?
6. À partir de la table initiale, créez une nouvelle table qui ne contient que les pokemons de type `'Plante'`.
7. Créez une nouvelle table triée sur le champ `'PV'` par ordre décroissant.
8. [Voici une table](coordonnees_communes.csv){:target="_blank"} des coordonnées géographiques des communes françaises. Créez une nouvelle table en fusionnant les deux tables sur le champ `'code'`.
9. Créez une carte avec folium pour localiser les pokémons !

!!! info "Créer une carte avec le module `folium`"
    Le module `folium` de Python permet de créer une carte au format `html` grâce à [OpenStreetMap](https://www.openstreetmap.fr/) et le module `webbrowser` permet de l'afficher dans un navigateur.

    ```python linenums='1'
    import folium
    import webbrowser

    pos = [48.8704, 2.31673] # coordonnées géographiques

    c = folium.Map(location=pos, zoom_start=15) # création d'une carte centré en `pos`

    folium.Marker(location=pos, popup="Qui habite ici ?").add_to(c) # ajout d'un marqueur sur la carte
    
    c.save('maCarte.html') # sauvegarde la carte au format HTML
    webbrowser.open('maCarte.html') # affiche la carte dans un navigateur
    ```

    Il est possible d'ajouter autant de marqueurs que souhaité.