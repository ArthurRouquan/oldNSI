# Page dynamique : JavaScript

Une page web peut aussi comporter du code **JavaScript** qui est exécuté par le navigateur Web du client. Le langage de programmation JavaScript  (abrégé JS) permet de modifier dynamiquement le contenu d'une page web, de manipuler et de mettre à jour le document HTML, le style CSS et même d'interagir avec des éléments multimédias, des formulaires et des données.

Il est important de noter que le serveur Web fournit ici toujours la **même** page web (les mêmes fichiers HTML, CSS et JS) aux différents clients. Le serveur Web peut aussi générer dynamiquement du contenu en utilisant des langages de programmation *côté serveur* (*backend*) tels que PHP, Python, Ruby, Java, ou des frameworks tels que Node.js et générer une réponse personnalisée pour chaque client.

## Un premier script JS

=== "Document HTML"
    ```html title="page.html" hl_lines="5 11"
    <!DOCTYPE html>
    <html>
      <head>
        <title>Un premier script</title>
        <script src="/script.js"></script> <!-- (1)! -->
      </head>
      <body>
        <h1>Une page web extrêmement dynamique</h1>
        <p>
          Pour changer la couleur de l'arrière-plan :
          <button onclick="change_couleur()">Cliquez ici !</button> <!-- (2)! -->
        </p>
      </body>
    </html>
    ```

    1. On lie le script JavaScript `script.js` au document HTML. 

    2. Quand l'utilisateur clique sur le bouton, la fonction `change_couleur` est exécutée.

=== "Script JS"
    ```js title="script.js"
    console.log("Démarrage du script..."); //(1)! 

    function change_couleur()
    {
      if (document.body.style.backgroundColor === 'lightblue') {
          document.body.style.backgroundColor = 'lightcoral';
      } else {
          document.body.style.backgroundColor = 'lightblue';
      }
    }
    ```

    1. Affiche du texte dans la console.
   
!!! question
    Modifier la page Web pour rajouter plusieurs boutons qui change la couleur de l'arrière-plan. On veut aboutir à :

    ```html
    <button onclick="change_couleur('red')">Rouge</button>
    ```

## 🎲 Un lancer de dès


!!! note "Modifier un élément HTML suivant son identifiant"
    ```html title="page.html" hl_lines="3"
    <script src="script.js"></script>

    <p id="toto">Oui</p>
    <button onclick="modifier_texte()">Clic</button>
    ```

    ```js title="script.js" hl_lines="3"
    function modifier_texte()
    {
      var toto = document.getElementById("toto");
      toto.innerHTML = "Non";
    }
    ```

!!! note "Nombre aléatoire en JavaScript"
    Pour tirer un entier aléatoirement en JavaScript entre `0` et `max` (extrémités incluses) : 
    ```js
    var resultat = Math.floor(Math.random() * max);
    ```

!!! question
    Générer une page web qui puisse simuler un lancer de dès à 6 faces (une amélioration serait de proposer des dès à 20 faces et 100 faces). Inclure un style CSS !