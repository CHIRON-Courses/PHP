# Super Globales

## [Définition](https://www.php.net/manual/fr/language.variables.superglobals.php)

Les Superglobales sont des variables internes qui sont toujours disponibles, quel que soit le contexte. Plusieurs variables prédéfinies en PHP sont "superglobales", ce qui signifie qu'elles sont disponibles quel que soit le contexte du script. Il est inutile de faire `global $variable;` avant d'y accéder dans les fonctions ou les méthodes.

----------

### Accès

Pour accéder à une super globale vous pouvez l'utiliser comme n'importe quelle variable.

```php
var_dump($_SERVER);
```

Vous constaterez que c'est un tableau associatif et pouvez accéder à ses éléments avec ses indices.

```php
echo $_SERVER["REMOTE_ADDR"]; // ::1
```

Le problème avec ces variables c'est qu'elles sont disponibles en écriture.

```php
$_SERVER = null;
```

Mais ce sont pourtant des valeurs que nous souhaitons comme constante pour ne pas être induit en erreur.

Le second problème est la vérification à faire avant d'accéder à un élément du tableau pour ne pas risquer de se prendre une notice.

```php
if (array_key_exists("REMOTE_ADDR", $_SERVER)) {
    echo $_SERVER["REMOTE_ADDR"]; // ::1
}
```

> Accéder directement à une super globale est une mauvaise pratique.

----------

### [filter_input](https://www.php.net/manual/fr/function.filter-input.php)

Une meilleur pratique pour accéder aux variables globales et l'utilisation de `filter_input`. Vous pouvez accéder à un élément d'une super globale et sa valeur sera constante, peut importe le traitement qu'il sera fait à la variable.

```php
echo filter_input(INPUT_SERVER, "REMOTE_ADDR"); // ::1
```

Si l'élément n'est pas présent la valeur de retour sera `null`.

L'utilisation de `filter_input` devra être systématique pour accéder à ces variables, il faut noter que ce n'est pas encore implémenté pour `$_SESSION`.

----------

## [Server](https://www.php.net/manual/fr/reserved.variables.server.php)

`$_SERVER` est un tableau contenant des informations comme les en-têtes, dossiers et chemins du script. Les entrées de ce tableau sont créées par le serveur web. Il n'y a aucune garantie que tous les serveurs les rempliront tous .

----------

## [Get](https://www.php.net/manual/fr/reserved.variables.get.php)

Un tableau associatif des valeurs passées au script courant via les paramètres d'URL (aussi connue sous le nom de "query string"). Notez que ce tableau n'est pas seulement rempli pour les requêtes GET, mais plutôt pour toutes les requêtes avec un query string.

Par exemple pour l'url suivante `/?foo=bar` vous pouvez constatez que le tableau contient:

```php
array(1) {
  ["foo"]=>
  string(3) "bar"
}
```

Cela sera pratique pour récupérer des paramètres via l'url.

----------

## [Post](https://www.php.net/manual/fr/reserved.variables.post.php)

Un tableau associatif des valeurs passées au script courant via le protocole HTTP et la méthode POST lors de l'utilisation de la chaîne `application/x-www-form-urlencoded` ou `multipart/form-data` comme en-tête HTTP Content-Type dans la requête.

Donc si une requête possède une méthode `POST` et une entête `application/x-www-form-urlencoded` ou `multipart/form-data` généré automatiquement par les formulaires, alors le tableau associatif sera peuplé de la donnée postée.

### **Formulaire**

Pour envoyer une requête en `POST` avec un formulaire vous devez utiliser l'attribut `method` de la balise form.

```html
<form method="post" action="">
```

### **Input**

Pour qu'une valeur soit postée depuis un élément de formulaire, il faut que l'élément d’interaction possède une valeur sur son attribut `name`.

```html
<input name="foo" />
```

En postant le formulaire détaillé avec un button ou un input submit le tableau des POST sera peuplé de la manière suivante.

```php
array(1) {
    ["foo"]=>
    string(3) "valeur tapée par l'utilisateur"
}
```

----------

## [Cookie](https://www.php.net/manual/fr/reserved.variables.cookies.php)

Un tableau associatif de variables, passé au script courant, via des cookies HTTP.

### Créer un cookie

La fonction [setcookie](https://www.php.net/manual/en/function.setcookie) permet la création de cookie.

```php
$hello = "world";
 
setcookie('hello', $hello, strtotime('+30 days'));
```

### Récupérer la valeur d'un cookie

Et c'est la que la variable Superglobale entre en jeu.

```php
echo filter_input(INPUT_COOKIE, "hello"); // world
```

### Supprimer un cookie

Ça peut paraitre bizarre, mais pour supprimer un cookie, il va falloir utiliser la fonction `setcookie()` et lui mettre une datetime dépassé.

```php
setcookie('hello', null, strtotime('yesterday'));
```

La bonne pratique voudrait qu'on supprime à la fois la paire clé-valeur dans la Superglobale et le cookie dans le navigateur.

```php
if (isset($_COOKIE['hello'])) {
    unset($_COOKIE['hello']);
    setcookie('hello', null, strtotime('yesterday'));
    echo "Cookie supprimé";
} else {
    echo "Ce cookie n'existe pas/plus";
}
```

----------

[Retour au sommaire](00_sommaire.md)