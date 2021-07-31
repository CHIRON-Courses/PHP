# Projet

Nous nous apprêtons à en découvrir d'avantage sur le langage PHP, je vous invite à le faire en visant des objectifs fonctionnels. De ce fait, nous allons développer un projet que vous pourrez continuer par la suite, au fur et à mesure de votre apprentissage du langage PHP.

Pour cela, nous utiliserons plusieurs outils :

## [Git](https://git-scm.com/)

Git est un logiciel de versioning, open source et gratuit.

----------

## [Composer](https://getcomposer.org/)

Composer est le package manager pour écosystème PHP, les packages installables reposent sur le site associé [Packagist](https://packagist.org/).

Il sera utile pour installer des dépendances comme une librairie, un framework, pour initialiser un projet afin que sa version de PHP soit explicite ou encore pour charger vos classes...

----------

## Modèle-Vue-Contrôleur

**Modèle-Vue-Contrôleur** ou **MVC** est un motif d'architecture logicielle destiné aux interfaces graphiques lancé en 1978 et très populaire pour les applications web. Le motif est composé de trois types de modules ayant trois responsabilités différentes : les modèles, les vues et les contrôleurs.

-   Un modèle (Model) contient les données à afficher.
-   Une vue (View) contient la présentation de l'interface graphique.
-   Un contrôleur (Controller) contient la logique concernant les actions effectuées par l'utilisateur.

Ce motif est utilisé par de nombreux frameworks pour applications web tels que Ruby on Rails, Symfony, Laravel ou AngularJS.

----------

### Structure

Bien que nous soyons en procédural, nous suivrons comme organisation de projet celle du cadre applicatif Symfony qui sera étudié plus tard en prenant quelques libertés.

    project-name/
    |
    ├─ Controller/
    ├─ Dao/
    ├─ Model/
    └─ View/

----------

### [include](https://www.php.net/manual/fr/function.include.php)

L'instruction de langage include inclut et exécute le fichier spécifié. Il ne possède pas de valeur de retour et en cas de fichier non trouvé il déclenche un warning.

Les variables sont disponibles dans le fichier inclut.

```php
include './../templates/home/home.php';
```

L'instruction du langage `require` est similaire mais il possède une valeur de retour et provoque une erreur fatale si le fichier n'est pas trouvé.

----------

[Retour au sommaire](00_sommaire.md)