# Flux distant

## Récupération

La fonction `file_get_contents` permet également de faire une requête http pour obtenir un flux distant. Il faut spécifier son argument `use_include_path` à `false` et fournir un contexte avec `stream_context_create`.

### Contexte

Le contexte permet de spécifier la méthode, les entêtes, le body et d'autres informations.

```php
$context = [
    "http" => [
        'method' => 'POST',
        'header'=> "Content-type: application/json\r\n"
                 . "Content-Length: " . strlen($data) . "\r\n",
        'content' => $data
    ]
];
```

### Réponse

Pour obtenir les informations de réponse comme le status code et les entêtes, après avoir fait une requête avec `file_get_contents`, une variable locale nommée `$http_response_header` sera disponible juste après fournissant les informations.

```php
$body = file_get_content($url, false, $context);
var_dump($http_response_header);
```

[HTTP Response Header](https://www.php.net/manual/fr/reserved.variables.httpresponseheader.php)

----------

## Émission

### [Headers](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Response_fields)

Les entêtes d'une réponse correspond à des instructions que le navigateur doit prendre en compte, par exemple pour stocker la réponse en cache, ou pour formater son corps.

#### [header](https://www.php.net/manual/fr/function.header.php)

La fonction `header` permet de spécifier une entête.

Pour formater un document en XML par exemple.

```php
header("Content-Type: application/xml")
```

Pour demander l'interprétation d'une image.

```php
header("Content-Type: image/png")
```

Pour formater un document en json par exemple.

```php
header("Content-Type: application/json")
```

Vous remarquez que par défaut le type de contenu est `text/html`, il peut se configurer dans le fichier `php.ini`.

#### Redirection

Pour demander une redirection au navigateur le header location dit être utilisé.

```php
header("Location: /some-url")
```

----------
    
## [Status](https://developer.mozilla.org/fr/docs/Web/HTTP/Status)

Un code de status d'une réponse indique son état, son status. Il est composé d'un nombre et d'un texte associé normalisé.

Vous avez déjà rencontré des pages 404, ceci est un code de status. Il y a 5 catégories de code pour indiquer une information, un succès, une redirection, une erreur ou une erreur interne.

Pour définir le status d'une réponse en PHP il faut utiliser la fonction `header`, le protocole et sa version doivent être spécifiés. Vous remarquez que par défaut le status est 200 OK.

```php
header("HTTP/1.1 404 Not Found")
```

----------

[Retour au sommaire](00_sommaire.md)