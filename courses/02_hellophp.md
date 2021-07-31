# Hello PHP

## Exécution

### Balise

PHP est interprété à l'ouverture d'une balise PHP.

```php
<?php

echo "Hello php";
```

En dehors des balises PHP il n'est plus interprété.

```php
<?php

echo "Hello php";

?>

Simple texte
```

----------

### Syntaxe courte

PHP dispose d'une version courte qui doit être utilisée quand vous mélangez php avec du contenu statique. En effet quand vous dynamisez du contenu comme de l'HTML il n'est pas pratique d'utiliser la syntaxe suivante.

```php
<h1>
<?php

echo "Hello";

?>
</h1>
```

Et vous devriez utiliser le tag court PHP qui affiche une chaine de caractère.

```php
<h1><?= "Hello" ?></h1>
```

----------

### Pannel

En appuyant sur la touche `start` ou `lunch` de votre control pannel, un host et un port par défaut sont disponibles. Ils desservent le dossier public de votre serveur web, à savoir le dossier `htdocs` ou `www`.

----------

### Built in

PHP dispose d'un `Built in server`, il est utile pour développer. Vous n'êtes pas obligés d'avoir vos scripts dans le dossier public de votre serveur.

Pour démarrer le server, utilisez la commande suivante dans un terminal situé à l'emplacement de votre script.

    php -S localhost:8000

Si vous souhaitez exécuter un script situé dans un autre dossier il faut utiliser l'option target.

    php -S localhost:8000 -t my-directory

----------

### CLI

PHP peut s’exécuter avec des instructions en ligne de commande. Le mode interactive s'initialise avec l'option `-a`.

    php -a

Les instructions sont attendues et le output se fait dans le terminal.

    php > echo "Hello Cli";

----------

[Retour au sommaire](00_sommaire.md)