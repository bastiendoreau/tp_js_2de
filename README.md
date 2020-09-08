# tp_js_2de

## TP de Javascript pour élèves de 2de - durée 1H

#### Prérequis, connaître les bases du HTML et le principe des balises

Le but de ce TP est de vous faire découvrir l'utilisation d'un langage web, le JavaScript (ou JS)

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

Pour proposer le maximum d'information en peu de place, le format des données est du texte pur structuré de façon précise. Pour Deezer, le format présenté est le [JSON](https://fr.wikipedia.org/wiki/JavaScript_Object_Notation). Les autres formats structurés que l'on peut trouver pour des services web sont le XML ou encore le CSV par exemple.

Si à cet instant du TP, vous vous sentez perdu, allez [ici](http://www.perdu.com/)

**Quelqu'un a créé une playlist** sur Deezer, l'a partagé et l'a rendu publique, il vous a juste fourni le numéro de sa playlist `8095604822`

La page web de Deezer suivante montre comment appeler une playlist par l'API -> [https://developers.deezer.com/api/playlist](https://developers.deezer.com/api/playlist)

Vous pourrez aussi voir sur cette page les différentes informations que l'on peut trouver par l'appel d'une playlist

Définissez l'URL permettant d'appeler la bonne playlist, ouvrez la dans une page web (de préférence sur Firefox) et notez le titre de la playlist ainsi que son auteur

Comme vous pouvez le voir dans le menu de gauche, Deezer permet d'interroger beaucoup d'autres éléments, un album, un artiste ...


### 3 - Appel de l'API en JS
