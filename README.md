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

**1.1 Créez un dossier** `tpjs` sur le bureau de votre ordinateur

**1.2** Ouvrez un éditeur de texte standard (Notepad++, Wordpad, ...), **créez un fichier** `my_music.html` et enregistrez le dans le dossier

Copiez le corps du code suivant avec notamment l'appel à la fiche CSS `<link rel="stylesheet" href="style.css" />`

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


**-> le corps de la page** avec une partie `article` contenant un titre et du texte aléatoire et une partie `aside` contenant des infos sur l'auteur

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

**1.3**

### 2 - L'API de Deezer

### 3 - Appel de l'API en JS
