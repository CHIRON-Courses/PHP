# Fichiers

## [JSON](https://fr.wikipedia.org/wiki/JavaScript_Object_Notation)

La notation objet de JavaScript est le format d'inter échanges le plus utilisé. Ce n'est pas pour autant que c'est le bon format pour du stockage local dans des fichiers "plats". Néanmoins dotons nous de cette capacité syntaxique.

Avant de stocker vos données vous devez les convertir et pourquoi pas en JSON.

### [json_encode](https://www.php.net/manual/fr/function.json-encode.php)

Pour convertir un tableau ou un objet en chaine de caractère JSON valide il faut utiliser `json_encode`.

```php
$json = json_encode($data);
```

### [json_decode](https://www.php.net/manual/fr/function.json-decode.php)

Pour convertir une chaine de caractère au format json en tableau ou objet il faut utiliser `json_decode`.

```php
$data = json_decode($json);
```

En effet quand vous allez récupérer une donnée dans un fichier, vous voulez surement l'utiliser dans votre programme.

----------

## Sérialisation

La sérialisation consiste à obtenir une représentation au format chaine de caractère d'une valeur, pas particulièrement un tableau ou un objet.

### [serialize](https://www.php.net/manual/fr/function.serialize.php)

Génère une représentation stockable d'une valeur. C'est une technique pratique pour stocker ou passer des valeurs PHP entre scripts, sans perdre leur structure ni leur type.

```php
$serialized = serialize($data);
```

### [unserialize](https://www.php.net/manual/fr/function.unserialize.php)

Crée une variable PHP à partir d'une valeur sérialisée.

```php
$data = unserialize($serialized);
```

----------

## Écriture

Il existe de nombreuses fonctions pour écrire dans un fichier. Nous allons regardez les plus directe car le stockage en fichier ne devrait concerner que le cache.

### [file_put_contents](https://www.php.net/manual/fr/function.file-put-contents.php)

Écrit des données dans un fichier, si le fichier n'existe pas, il sera créé. Sinon, le fichier existant sera écrasé, si l'option FILE_APPEND n'est pas définie.

```php
$size = file_put_contents("my-file", $json);
```

> Cette fonction correspond à faire un `fopen`, `fwrite` et `fclose` consécutivement.

### [Chemin](https://www.php.net/manual/fr/language.constants.predefined.php)

Pour ne pas avoir de problèmes avec l'`include_path` ou la relativité des chemins, je vous conseil d’utiliser la constante magique `__DIR__`. Cette constante nous donne le chemin du répertoire en cours ou le script s’exécute.

```php
$includePath = __DIR__ . "/../mondossier";
```

### [Séparateur](https://www.php.net/manual/fr/dir.constants.php)

Concernant les séparateurs, sur linux c'est le slash et sur window c'est l'antislash. Linux acceptera également l'antislash, si vous êtes jusqu’au-boutiste vous pouvez utiliser la constante `DIRECTORY_SEPARATOR` qui nous donne en fonction du système le caractère qui sert de séparateur.

```php
$includePath = __DIR__ 
    . DIRECTORY_SEPARATOR .".."
    . DIRECTORY_SEPARATOR . "foo"
    . DIRECTORY_SEPARATOR . "bar"
    . DIRECTORY_SEPARATOR;
```

```php
$includePath = implode(DIRECTORY_SEPARATOR, [__DIR__, "..", "foo", "bar", ""]);
```

----------

## Lecture

Nous allons regardez la fonction qui accompagne celle observée précédemment.

### [file_get_contents](https://www.php.net/manual/fr/function.file-get-contents.php)

Lit tout un fichier dans une chaîne.

```php
$json = file_get_content("var/cache/my-file");
```

Cependant si le fichier n'existe pas vous aurez un warning, regardons des fonctions pour vérifier qu'un fichier existe.

### [is_file](https://www.php.net/manual/fr/function.is-file.php)

Pour savoir si un fichier existe et uniquement si c'est un fichier contrairement à `file_exists` il faut utiliser `is_file`.

```php
$bool = is_file($fileName);
```

----------

[Retour au sommaire](00_sommaire.md)