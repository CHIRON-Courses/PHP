# Fonctions

Les fonctions sont des objets Function qui permettent d'encapsuler des instructions dans un bloc afin d'y faire appel. Les fonctions peuvent posséder des arguments afin de leur transmettre des valeurs et peuvent également retourner une valeur de fin d'instruction.

## Déclaration

-   function identifiant([param1[, param2[, ...,paramN]]]) {}

Une fonction peut être une expression ou une instruction, dans les deux cas elles sont un objet Function.

```php
function maFonction()
{
    echo "Hello";
}
```

La première ligne est, ce qu'on appelle, la signature de la fonction. Dans notre exemple :

```php
function maFonction()
```

Ce qui suit est le bloc d'instruction de la fonction, réprésenté par des accolades `{}`.

Pour utiliser une fonction, il suffit de l'appeler grâce à sa signature.

```php
maFonction();
```

### return

-   return [expression = null];

L'instruction return renvoie la valeur de l'expression qui lui succède et met fin à l'exécution des instructions d'une fonction. L'expression de retour est optionnelle et sa valeur par défaut est null.

```php
function maFontion()
{
    return true;
}

echo maFontion(); // true
```

### Les arguments

La signature d'une fonction peut comporter des arguments ou paramètres, ce sont des valeurs ou des objets qui seront transmis sous forme de variables locales à la fonction. Les objets sont passés par référence ce qui signifie qu'ils ne sont pas copiés et que leurs modifications au sein de la fonction impactent l'objet en dehors de la fonction.

Il est possible de déclarer plusieurs arguments dans la signature d'une fonction.

```php
function division($dividende, $diviseur)
{
    return $dividende / $diviseur;
}
echo division(10, 2); // 5
```

Les arguments peuvent être optionnels en leur affectant une valeur dans la signature.

```php
function division($dividende, $diviseur = 1)
{
    return $dividende / $diviseur;
}
```

### Typage

Depuis PHP7 il est possible de typer en primitif et en non primitif les arguments et la valeur de retour de la fonction.

```php
function division(float $dividende, float $diviseur = 1): float
{
    return $dividende / $diviseur;
}
```

Si vous fournissez le mauvais type la valeur sera convertie si c'est possible.

### Portée

Une variable déclarée dans une fonction est locale : elle n'est pas disponible en dehors du bloc d'instruction de la fonction. Pour qu'une fonction utilise une variable déclarée localement, il faut utiliser le mot `global`.

```php
$message = "Hello";

function helloWorld(): string
{
    global $message;
    return "$message World";
}

echo helloWorld(); // Hello World
```

----------

[Retour au sommaire](00_sommaire.md)