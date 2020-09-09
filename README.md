# tp_js_2de

## TP de Javascript pour élèves de 2de - durée 1H

#### Interrogation par API de données publiques 

#### Prérequis, connaître les bases du HTML et le principe des balises

Le but de ce TP est de vous faire découvrir l'utilisation d'un langage web, le JavaScript (ou JS) et le principe d'un service web

JavaScript est un langage de programmation de scripts principalement employé dans les pages web interactives. Avec les technologies HTML et CSS, JavaScript est l'une des technologies cœur du web [... Wikipedia](https://fr.wikipedia.org/wiki/JavaScript)

Vous allez utiliser ce langage pour interroger une playlist partagée sur [Deezer](https://www.deezer.com)

Vous devrez faire afficher :
  * le titre et la description de la playlist
  * les titres, artistes et durées des différentes chansons
  
L'idée n'est pas de vous apprendre le langage en une heure mais d'en utiliser une partie pour interagir avec un site distant


### 1 - Construction du cadre HTML

Dans un premier temps, vous allez construire deux pages HTML, une pour l'accueil des visiteurs et l'autre pour la présentation des chansons.

Vous téléchargerez ensuite un fichiers CSS et des images pour le rendre agréable à voir.

**1.1 Créez un dossier** `tpjs` sur le bureau de votre ordinateur et ouvrez un éditeur de texte standard (Notepad++, Wordpad, ...)

**1.2 Créez un fichier** `my_music.html` et enregistrez le dans le dossier

**-> Copiez le corps du code HTML** suivant avec notamment l'appel à la fiche CSS `<link rel="stylesheet" href="style.css" />`

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <link rel="stylesheet" href="style.css" />
        <title>Toto - Ma musique</title>
    </head>
    
    <body>
      <div id="bloc_page">
      
    </div>
    </body>
</html>    
```

A l'intérieur des balises `<body>` et `<div id="bloc_page">`, insérez successivement

**-> le header de la page** contenant l'entête de la page et les éléments de navigation 

```
            <header>
                <div id="titre_principal">
                    <div id="logo">
                        <h1>Toto</h1>    
                    </div>
                    <h2>Toute ma musique</h2>
                </div>
                
                <nav>
                    <ul>
                        <li><a href="#">Accueil</a></li>
                        <li><a href="#">Musique</a></li>
                    </ul>
                </nav>
            </header>
```


**-> la bannière** contenant une image

```
            <div id="banniere_image">
                <div id="banniere_description">
                    Bienvenue à tous ...
                 </div>
            </div>
```


**-> le contenu principal de la page** avec une partie `article` contenant un titre et du texte aléatoire et une partie `aside` contenant des infos sur l'auteur

```
            <section>
                <article>
                    <h1><img src="images/ico_epingle.png" class="ico_categorie" />Je suis un grand amateur de musique</h1>
                    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam nec sagittis massa. Nulla facilisi. Cras id arcu lorem, et semper purus. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Duis vel enim mi, in lobortis sem. Vestibulum luctus elit eu libero ultrices id fermentum sem sagittis. Nulla imperdiet mauris sed sapien dignissim id aliquam est aliquam. Maecenas non odio ipsum, a elementum nisi. Mauris non erat eu erat placerat convallis. Mauris in pretium urna. Cras laoreet molestie odio, consequat consequat velit commodo eu. Integer vitae lectus ac nunc posuere pellentesque non at eros. Suspendisse non lectus lorem.</p>
                </article>
                <aside>
                    <h1>À propos de l'auteur</h1>
                    <img src="images/bulle.png" alt="" id="fleche_bulle" />
                    
                    <p>Laisse-moi le temps de me présenter&nbsp;: je m'appelle Toto</p>
                    <p>Voici la musique que j'écoute.</p>
                </aside>
            </section>
```

**1.3 Créez un autre fichier**  `call_deezer.html` au même endroit que le précédent. Reprenez de la même façon, le corps du code HTML et le header (pas la bannière, ni le contenu)

A la place du contenu précédent, copiez celui-ci 

```
            <section>
                <article>
                    <h1><img src="images/ico_epingle.png" alt="Catégorie voyage" class="ico_categorie" />Ma Playlist</h1>
                    <h2 id='presplaylist'>
                    </h2>
                    <h4 id='playlist'>
                    </h4>

                </article>       
            </section>
```

Ce contenu indique notamment deux éléments vides pour l'instant identifiés par 
  * `id='presplaylist'` qui servira à présenter la playlist (titre et description)
  * `id='playlist'` qui servira à présenter les chansons

**1.4 Modifiez les liens de navigation** dans ces deux fichiers pour que les deux liens de navigation soient fonctionnels (voir les éléments `<a href=` dans la navigation)

A partir de là, le contenu HTML est lisible (mais moche). Vous pouvez le tester dans un navigateur

**1.5 Téléchargez le fichier ZIP** suivant [tpjs.zip](https://github.com/bastiendoreau/tp_js_2de/raw/master/tpjs.zip) et extrayez les données dans le dossier `tpjs`

Et voilà, votre site est joli (vide mais joli)


### 2 - L'API de Deezer

Deezer, comme beaucoup d'entreprises a envie de permettre à d'autres applications d'utiliser son contenu. Pour cela elle a créé une [API](https://fr.wikipedia.org/wiki/Interface_de_programmation), c'est à dire un service web permettant d'obtenir des données de la base de données de Deezer.

Pour proposer le maximum d'information en peu de place, le format des données est du texte pur structuré de façon précise. Pour Deezer, le format présenté est le [JSON](https://fr.wikipedia.org/wiki/JavaScript_Object_Notation). Les autres formats structurés que l'on peut trouver pour des services web sont le XML ou encore le YAML par exemple.

Le JSON permet de présenter des objets et des listes d'objets, ci dessous l'objet `classe` comprend un objet `id` ayant comme valeur 123, un objet `classe2de` et un dernier objet `listusers` qui est un tableau contenant des objets `users` chacun définis par un nom et prénom


```
{
    "classe": {
        "id": 123,
        "classe2de": "Seconde B",
        "listusers": {
            "users": [
                { "nom": "Dupont", "prenom": "Toto" },
                { "nom": "Durand", "prenom": "Titi" },
                { "nom": "Duchemin", "prenom": "Kéké" }
            ]
        }
    }
}
```

Si à cet instant du TP, vous vous sentez perdu, allez [ici](http://www.perdu.com/)

**Quelqu'un a créé une playlist** sur Deezer, l'a partagé et l'a rendu publique, il vous a juste fourni le numéro de sa playlist `8095604822`

La page web de Deezer suivante montre comment appeler une playlist par l'API -> [https://developers.deezer.com/api/playlist](https://developers.deezer.com/api/playlist)

Vous pourrez aussi voir sur cette page les différentes informations que l'on peut trouver par l'appel d'une playlist

Définissez l'URL permettant d'appeler la bonne playlist, ouvrez la dans une page web (de préférence sur Firefox) et notez le titre de la playlist ainsi que son auteur (faites vérifier par votre professeur)

Comme vous pouvez le voir dans le menu de gauche, Deezer permet d'interroger beaucoup d'autres éléments, un album, un artiste ...

Maintenant que vous savez où sont les données en JSON, vous allez les chercher pour les intégrer à votre site


### 3 - Principe du Javascript

La Javascript est un langage de programmation qui doit être éxécuté (càd lu et compris). C'est le navigateur (ou d'autres fichiers javascript) qui pourront éxécuter ce code.

C'est donc le navigateur du client (celui qui ouvre la page web) qui est utilisé, et pas le serveur qui fait ce travail. Avantage : c'est le client qui doit fournir de la puissance de calcul et pas le serveur ; inconvénient : le navigateur du client doit être à jour ou le script JS peut planter.

Ainsi, on retrouve un script JS directement dans une page HTML. On le trouve en général en fin de page, juste avant la fermeture de la balise `body`, il sera donc éxécuté après la lecture du HTML.

Insérez le script suivant juste avant la balise  `</body>` dans la page `my_music.html` puis actualisez la page

```
<script>
    var saisie = prompt('Ecrire du texte');
    saisie = "Vous avez écrit "+saisie
    alert(saisie)
</script>
```

Analysons ce script :
  * En premier lieu, on peut voir que ce script JS pour être identifié comme tel est entre des balises `<script>` et `</script>` 
  * la première ligne va ouvrir une fenêtre demandant une saisie à l'utilisateur gràce à la commande `prompt` et enregistrer le résultat dans la variable `saisie`
  * `saisie` doit être déclarée comme variable grace au mot-clé `var`
  * On peut modifier cette variable, ici on a rajouté du texte devant. Le texte rajouté doit être entre guillemets pour bien indiquer qu'il s'agit de texte et pas de commandes JS
  * On peut afficher dans une fenêtre le contenu d'une variable avec la commande `alert`
  
Vous allez faire un premier exercice simple (toujours dans `my_music.html`). Supprimez tout d'abord le script précédent.

Vous devez faire un script calculant l'IMC (indice de masse corporelle) d'une personne.

Dans ce script demandez le poids en kg, puis la taille en mètres. Effectuez le calcul suivant `IMC=poids/(taille*taille)` et affichez l'IMC

Le résultat est inférieur à 1 ou supérieur à 100 ? Cliquez [ici](https://media.giphy.com/media/12vVdbq7jtkiSk/giphy.mp4)

Le résultat est compris entre 15 et 40 ? vous pouvez continuer le TP

Un des gros intérêts du JS est aussi l'interaction avec des élements de la page web.

Le principe est de distinguer un élément de la page par un identifiant et d'exécuter du script en lien avec cet élément en particulier.

Créez une page HTML `mdp.html` et insérez le code suivant

```
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>Vérification de mots de passe</title>
</head>
<body>
    <form>
        <p>
            <label for="mdp1">Saisissez le mot de passe</label> :
            <input type="password" name="mdp1" id="mdp1" required>
        </p>
        <p>
            <label for="mdp2">Confirmez le mot de passe</label> :
            <input type="password" name="mdp2" id="mdp2" required>
        </p>

        <button onclick="validate()">Valider</button><br>
    </form>
</body>
</html>
```

Vous avez écrit un formulaire demandant un mot de passe ainsi que sa confirmation. Vous pouvez voir dans la balise `button` le texte `onclick="validate()`. Cela indique que lorsqu'un utilisateur cliquera sur ce bouton, la fonction `validate` d'un script sera appelée

Rajoutez le script suivant dans cette page, actualisez la page et testez le formulaire

```
    <script  type="text/javascript">
    function validate() { 
        var m1 =  document.getElementById("mdp1").value;
        var m2 =  document.getElementById("mdp2").value;

        if (m1!=m2) {
            alert("Les mots de passe sont différents. Recommencez")
            return false;
            }
        else {
            alert("Les mots de passe sont identiques. C'est bon");
            return true;
            }
    }
    </script>
```

Analysons ce script :
  * la fonction validate se déclare avec le mot-clé `function` et avec des parenthèses. Son contenu est entre `{` et `}`
  * on récupère une valeur d'un élément HTML par son `id`. `document.getElementById("mdp1")` va chercher ce qu'il y a dans l'élément HTML contenant `id="mdp1"`
  * le JS est un langage de programmation, il est possible d'utiliser des boucles, des conditions, ... Ici, on fait une condition sur l'égalité entre les variables m1 et m2


Pour aller plus loin dans le javascript :
  * Cours sur le javascript [openclassroom](https://openclassrooms.com/fr/courses/1916641-dynamisez-vos-sites-web-avec-javascript)
  * Tester son script rapidement dans une interface en ligne [JSFiddle](https://jsfiddle.net/)
  
### 4 - Appel de l'API en JS

Vous allez maintenant utiliser une fonction toute faite `XMLHttpRequest` pour faire une requête HTTP vers l'API de Deezer

Dans un premier temps, vous allez intégrer un script qui va télécharger le code permettant d'utiliser ces fonctions. Placez ce premier script en bas de votre page `call_deezer.html` (juste avant la balise `</body>`)

```
    <script
        src="https://code.jquery.com/jquery-3.3.1.min.js"
        integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
        crossorigin="anonymous">
    </script>
```

Juste au dessus, créez un nouveau script qui utilisera la fonction `XMLHttpRequest`. Ce script va :
  * créer un objet XMLHttpRequest
  * définir l'URL sur laquelle on veut pointer
  * écrire une fonction qui sera effectuée si la requête est réussie (c'est là qu'on a placé un point de contrôle avec `alert("ok")`
  * lancer la requête `xhr.send();`

```
<script>
    // Definition d'un objet XMLHttpRequest 
    var xhr = new XMLHttpRequest();

    //defintion d"une variable pour l'URL de Deezer
    var url = "https://api.deezer.com/playlist/8095604822"
    
    // on cree une fonction qui sera appelee quand l'etat de la requete sera modifiee (qd toutes les infos seront recuperees)
    xhr.onreadystatechange = function() {
      // on verifie que la requete est reussie (code HTTP 200)
      if (xhr.readyState == 4 && xhr.status == 200) 
      { 
        // On verifie qu'on arrive bien jusqu'ici
        alert("ok")
      }
    }; // Fin de la fonction
    
    // On lance la requete HTTP de type GET avec la bonne URL
    xhr.open("GET", url, true);   
    xhr.send();
</script>
```

Que se passe-t-il ?  --> Rien. La requête ne marche pas ou quelque chose bloque. Voyons ce qu'il se passe en regardant la console du navigateur

Dans Firefox, ouvrir le menu puis `Développement web` puis `Outils de développement`, la console s'ouvre. Cliquez sur l'onglet `Console` (sous Chromium menu, `plus d'outils` et `outils de développement`)

Le point de blocage est expliqué --> `l’en-tête CORS « Access-Control-Allow-Origin » est manquant`

Aïe, cela signifie que cette API n'est pas faite pour être utilisée par une simple page web mais par un serveur. Heureusement, il est possible de passer par un serveur qui enverra cette URL à votre place. Vous allez donc devoir tricher et modifier votre url. 

Remplacez

```
    //defintion d"une variable pour l'URL de Deezer
    var url = "https://api.deezer.com/playlist/8095604822"
```

par 

```
    //defintion d"une variable pour l'URL permettant de contourner le blocage de Deezer  
    var url_heroku = "https://cors-anywhere.herokuapp.com/"

    //defintion d"une variable pour l'URL de Deezer
    var url_deezer = "https://api.deezer.com/playlist/8095604822"
    
    // on cree une nouvelle URL a partir des deux URLs
    var url = url_heroku + url_deezer
```

Cela fonctionne, on voit le message d'alerte.

Maintenant, vous allez remplacez ce message d'alerte par le code suivant qui récupère le contenu de la requête en JSON et appelle une nouvelle fonction

```
        // On recupere le contenu de la requete (xhr.responseText) en la traduisant en JSON
        var jsonData = JSON.parse(xhr.responseText);
        
        // On appelle la fonction getPlaylist en lui envoyant le JSON en parametre
        getPlaylist(jsonData);
```

Et bien sur écrire la fonction `getPlaylist` après `xhr.send` et avant la balise de fin de script `</script>`

```
    // fonction permettant de boucler sur toutes les donnees de la liste tracks (voir le résultat du JSON)
    // On recuperera le lien de la chanson, son titre, son auteur et sa duree, on placera toutes ces infos
    // dans du code HTML
    function getPlaylist(data) {
        var outputPl = ""; // Ouverture de la liste des chansons
        var pub;
        
        // Boucle sur toutes les chansons , on remplit l'element outputPl avec des informations lues dans le JSON
        for (var pub in data.tracks.data) {
    
            outputPl += "<a href=\"" + data.tracks.data[pub].link + "\">" + data.tracks.data[pub].title + "</a>  "+ 
            " -> " + data.tracks.data[pub].artist.name;
    
            outputPl += " (" + data.tracks.data[pub].duration + " s)";
    
            outputPl += "</br></br> ";
        }
        outputPl += ""; // Fermeture de la liste
    
        // on place le contenu que l'on vient de creer dans le code HTML ayant l'id playlist
        document.getElementById("playlist").innerHTML = outputPl;
    }
```

Bravo, vous avez utilisé un service web et codé en JS pour appeler une API

Dernier exercice, vous devez écrire une fonction `getPresplaylist` permettant de recuperer le titre de la playlist, sa description, son auteur et le nb de chansons.

Le contenu doit être envoyé dans l'élément HTML ayant l'id `presplaylist`
