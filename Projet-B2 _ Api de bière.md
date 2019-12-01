# Projet B2 : Api de bière
## Membre du groupe :
### - ***Costin Gibaux***
### - ***Julien Chigot***
<br>

# Sommaire :

<br>

- [Projet B2 : Api de bière](#projet-b2--api-de-bi%c3%a8re)
  - [Membre du groupe :](#membre-du-groupe)
    - [- ***Costin Gibaux***](#costin-gibaux)
    - [- ***Julien Chigot***](#julien-chigot)
- [Sommaire :](#sommaire)
  - [Descriptif de l'api choisi](#descriptif-de-lapi-choisi)
  - [Installation et lancement de notre projet](#installation-et-lancement-de-notre-projet)
  - [Page d'accueil](#page-daccueil)
  - [API](#API)
  - [Conclusion](#conclusion)


<br>
<br>

## Descriptif de l'api choisi :
<br>

Le nom de notre ***api*** est : [Punk API](https://punkapi.com/documentation/v2)

C'est une API qui regroupe énormément de bière brassé dans le monde entier.

<br>
<br>
<br>
<br>
<br>

## Installation et lancement de notre projet :
<br>

Pour installer notre projet il faut suivre les étapes suivantes :

- Tout d'abord rendez vous sur notre [gitlab](https://gitlab.com/CGibaux/api-beer) afin de télécharger notre projet.
- Ensuite il vous faudra soit cloner notre projet :
![clone](../api-beer/src/assets/img/markdown/clone.png)

<br>

- Soit télécharger le .zip :
![dl-zippng](../api-beer/src/assets/img/markdown/dl-zippng.png)

<br>

- Une fois fait, il suffit de lancer votre terminal et de vous rendre dans votre projet : 
![cmd](../api-beer/src/assets/img/markdown/cmd.png)

<br>

- Après vous être rendu sur votre terminal, il vous suffit de rentrer la commande suivante :
```
npm install
```
- Maintenant que les [dépendances](https://flaviocopes.com/package-json/) sont téléchargés, ils vous faut lancer votre serveur afin de pouvoir regarder notre projet. Pour ce faire il suffit d'éxecuter la commande suivante (toujours dans le même cmd) :
```
npm run serve
```

<br>

***Voilà notre projet est lancé, nous pouvons désormais regarder plus en profondeur le projet.***

<br>
<br>
<br>
<br>
<br>

## Page d'accueil :
<br>

Sur la page d'accueil se trouve notre carousel (laisser le carousel faire défiler les images, il se peut qu'il se trouve un trésor dans les deux dernières images.)

<br>
<br>
<br>
<br>
<br>

 ## API :
 
 <br>
 
 Sur la page vous pouvez trouver plusieurs fonctionnalités.
 
Premièrement quand vous êtes sur la page en haut vous trouverez la première page de bière affichée de base. Vous avez le choix entre défiler entre les pages avec les boutons pour changer de page (Previous and Next).
 
Sinon il y a en haut 4 barres de recherche qui vous permettent d'affiner votre recherche à votre guise. 

La première cherche en fonction du nom, la seconde vous permet de mettre un degré d'alcool et la recherche va vous mettre toute les bières avec le même degré d'alcool ou plus que votre recherche.

Les deux dernières sont selon la date sois d'avant la première brassade soit après.

<br>
<br>
<br>
<br>
<br>

## Conclusion :

<br>

Notre projet vous propose une variétée de bières que vous pouvez simplement regarder en les défilant à l'aide des pages ou si vous rechercher une bière précisément vous pouvez la trouver (si elle se trouve dans l'API) avec nos barre de recherche.

