# Projet Part II

Maintenant que le projet est bien avancée avec l'affichage de plusieurs page distincte. Nous allons implémenter un router afin de gérer de manière plus efficace le projet.

## Refactoring

Pour cela nous devrons revoir une bonne partie du code du projet.

### Structure

Et nous allons commencer par revoir la structure du projet.

    project-name/
    |
    ├─ config/
    ├─ public/
    ├─ src/
	|	|
	|	├─ Controller/
	|	├─ Entity/
	|	└─ Repository/
	|
    └─ templates/

Comme vous le constatez il n'est pas possible par défaut d'obtenir des url personnalisées. Ainsi vous exposez le nom de vos scripts et êtes limités pour fournir des url user friendly ce qui est une mauvaise pratique.

> Que vous utilisiez l'une ou l'autre des exécutions il nous faut activer la réécriture d'URL, c'est à dire le fait de pouvoir avoir l'url [http://localhost/user/2](http://localhost/user/2) et qu'on ne tombe pas sur une page objet non trouvé. En PHP toutes les url doivent exécuter votre script principal, votre index.php situé à la racine de votre dossier public. C'est le point d'entré de votre programme.

### .htaccess

Pour remédier à cela nous allons, dans un fichier, donner des directives au server apache. Le fichier `.htaccess` contient ces directives.

```
# Deny access to the .htaccess file and will trigger a 403 status code
<Files .htaccess>
    order allow,deny
    deny from all
</Files>
#Turn RewriteEngine to On
RewriteEngine On
#Deliver static file
RewriteCond %{REQUEST_FILENAME} -f
RewriteRule ^ - [L]
#Trigger index.php and add query string append flag
RewriteRule ^(.*)$ index.php [QSA,L]
```

Ce fichier donne les directives suivantes:

-   Interdit sa consultation.
-   Active le write engine.
-   Permet que les fichiers présents sur disque soit délivrés.
-   Réécrit toutes les url vers le fichier index.php en lui passant les paramètres d'url s'ils sont présents.

### [Fonctions de bufferisation de sortie](https://www.php.net/manual/fr/ref.outcontrol.php)

Les fonctions de bufferisation de sortie vont permettre debufferiser (mettre en mémoire tampon) tout élément de sortie qui serai envoyé au client jusqu'à ce qu'on flush ce qui a été mis en tampon.

#### [ob_start](https://www.php.net/manual/fr/function.ob-start.php)

La fonction `ob_start()` enclenche la temporisation de sortie.

```php
ob_start();

echo "Ce texte a été mis en mémoire tampon";
```

#### [ob_end_flush](https://www.php.net/manual/fr/function.ob-end-flush.php)

La fonction `ob_end_flush` envoie les données du tampon de sortie et éteint la temporisation de sortie.

```php
ob_start();

echo "Le texte qui s'affiche à présent a été mis en mémoire tampon";

ob_end_flush();
```

#### [ob_end_clean](https://www.php.net/manual/fr/function.ob-end-clean.php)

La fonction `ob_end_clean` détruit les données du tampon de sortie et éteint la temporisation de sortie

```php
ob_start();

echo "Ce texte ne s'affiche jamais car il a été supprimé de la mémoire tampon";

ob_end_clean();
```

----------

[Retour au sommaire](00_sommaire.md)