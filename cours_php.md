# Introduction

## Historique

PHP est un "langage de programmation" `libre`, principalement utilisé pour produire des pages Web dynamiques via un serveur HTTP, mais pouvant également fonctionner comme n'importe quel langage interprété de façon locale. PHP a permis de créer un grand nombre de sites web célèbres, comme Facebook et Wikipédia. Il est considéré comme une des bases de la création de sites web dits dynamiques mais également des applications web.

> I don't know how to stop it, there was never any intent to write a programming language.

-   1994: Rasmus Lerdorf release PHP 1 - Personal Home Page.
-   1997: Zeev Suraski et Andi Gutmans release PHP3 - Hypertext Preprocessor.
-   2000: PHP 4, powered by the Zend Engine 1.0 introduit le mot class.
-   2004: PHP 5, powered by the Zend Engine 2.0, le model objet gagne en maturité.
-   2015: PHP 7, powered by the Zend Engine 3.0, les performance sont améliorés et le typage est renforcé.

PHP est le langage le plus utilisé côté serveur (environ 80%). [W3Techs](https://w3techs.com/)

----------

## Types de donnée

PHP supporte 10 types basiques.

4 types scalaires :

-   bool (booléen)
-   int (entier)
-   float (nombre à virgule flottante, i.e. double)
-   string (chaîne de caractère)

4 types composés :

-   array (tableau)
-   object (objet)
-   [callable](https://www.php.net/manual/fr/language.types.callable.php) (fonction de rappel)
-   [iterable](https://www.php.net/manual/fr/language.types.iterable.php) (itérable)

2 types spéciaux :

-   resource (ressource)
-   NULL (nul)

----------

## Serveur

PHP est un langage Back End. Il est alors interprété par sur un serveur et il nous faut un serveur local pour développer.

En fonction de votre environnement, il existe des serveur avec **A**pache/**M**ySQL/**P**HP/PhpMyAdmin.

-   Apache

Le logiciel libre Apache HTTP Server est un serveur HTTP créé et maintenu au sein de la fondation Apache. Jusqu'en avril 2019, ce fut le serveur HTTP le plus populaire du World Wide Web.
[NetCraft - Web Server Survey](https://news.netcraft.com/archives/2021/05/31/may-2021-web-server-survey.html)

-   MySQL

MySQL est un système de gestion de bases de données relationnelles. Il est distribué sous une double licence GPL et propriétaire.

-   PhpMyAdmin

PhpMyAdmin est une application Web de gestion pour les systèmes de gestion de base de données MySQL réalisée principalement en PHP et distribuée sous licence GNU GPL.

[Xampp](https://www.apachefriends.org/fr/index.html) [Wamp](https://www.wampserver.com/) [Mamp](https://www.mamp.info/en/downloads/)

----------

## Documentation PHP

La documentation PHP est surement l'une des documentations les plus facile à comprendre. Vous pourrez la trouver sur [PHP.net](https://www.php.net).

----------

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

# Variables

## Déclarations

Le `$` permet de déclarer une variable. Le premier caractère est soit un souligné (underscore `_`), soit une lettre A-Z ou a-z. Peut venir ensuite autant de chiffre, lettre ou de souligné que souhaité.

### [Var](https://www.php.net/manual/fr/language.variables.php)

```php
$foo;
```

En cas de passage par référence il est possible de ne pas affecter de valeur à une variable. Hormis ce cas vous devez fournir une valeur, le type n'est pas à déclarer et il peut varier.

```php
$foo = true;
$foo = "Hello";
```

Une variable peut se télescoper de son bloc d’exécution.

```php
if (true) {
    $foo = "Hello";
}
echo $foo; // Hello
```

Une variable en dehors d'une fonction est dite "globale".

### [Dynamisme](https://www.php.net/manual/fr/language.variables.variable.php)

Les identifiants de variables sont dynamiques, c'est une force.

```php
$foo = "bar";
$$foo = "baz";
echo $bar; // baz
```

La bonne pratique est d'utiliser la priorité de calcul d'identifiant.

```php
$foo = "bar";
${$foo} = "baz";
echo $bar; // baz
```

Ceci peut être pratique quand vous chainer des interprétations de valeur, comme construire un objet à partir d'un identifiant dynamique stocké. Nous en aurons l'utilité un jour.

----------

### Référence

Une variable peut être déclarée comme étant une référence d'une autre variable. Sa modification modifiera l'originale.

```php
$foo = "bar";
$bar = &$foo;
$bar = "baz";
echo $foo; // baz
```

C'est utile quand une fonction modifie une variable en utilisant sa référence plutôt que d'utiliser une valeur de retour.

### [Constantes](https://www.php.net/manual/fr/language.constants.php)

Les constantes sont des espace de stockages dont la valeur ne peut pas varier. Elle est accessible en lecture mais pas en écriture.

Pour les déclarer il faut utiliser la fonction `define`.

```php
define("FOO", "Hello");
```

Pour y accéder il faut simplement utiliser l'identifiant de la constante.

```php
echo FOO; // "Hello"
```

----------

## [Types](https://www.php.net/manual/fr/language.types.php)

Null

```php
var_dump(null);
```

----------

### Primitifs

Boolean

```php
var_dump(true);
```

Integer

```php
var_dump(7);
```

Float

```php
var_dump(7.7);
```

String

```php
var_dump('foo');
```

La double quote permet d’interpoler des variables.

```php
$name = 'John';
$message = "Hello $name";
echo $message; // Hello John
```

Moins populaire le HEREDOC existe pourtant, nous passerons sur la NOWDOC. L'identifiant de fin de bloc ne doit pas être indenté.

```php
$name = 'John';
echo <<<FOO
 Hello $name
FOO;
```

----------

## Tableaux

Les tableaux ne sont pas dimensionnés et pas typés.

### [Déclaration](https://www.php.net/manual/fr/function.array.php)

Il est possible de déclarer un tableau en utilisant la fonction `array`

```php
$foo = array();
```

Il est possible de préremplir le tableau de valeurs.

```php
$foo = array('foo', 'bar', 'baz');
```

La déclaration littérale utilise les crochets.

```php
$foo = [];
```

Il est possible de préremplir le tableau de valeurs.

```php
$foo = ['foo', 'bar', 'baz'];
```

#### Associatif

Par défaut chaque élément du tableau est associé à un indice numérique pour pouvoir y accéder. Sur ce langage il est possible de choisir les indices des éléments, c'est l'équivalent d'une map.

```php
$colorList = [
    'red' => '#ff0000',
    'green' => '#00ff00',
    'blue' => '#0000ff',
];
```

----------

### [Manipulation](https://www.php.net/manual/fr/ref.array.php)

#### Accéder à un élément d'un tableau

Il faut se référer à ses indexes.

```php
echo $foo[1]; // bar
```

#### Taille

```php
echo count($foo); // 3
```

#### Supprimer un élément

La fonction `array_shift` renvoie et supprime le premier élément du tableau puis réorganise les clefs du tableau.

```php
echo array_shift($foo); // foo
```

La fonction `array_pop` renvoie et supprime le dernier élément du tableau.

```php
echo array_pop($foo); // baz
```

La méthode `splice` modifie le contenu d'un tableau en retirant des éléments et/ou en ajoutant de nouveaux éléments à même le tableau puis le ré-indexé.

```php
array_splice($foo, 2, 1);
```

#### Ajouter un élément

La fonction `array_unshift` ajoute un élément au début, renvoie sa nouvelle taille puis réorganise les clefs du tableau.

```php
echo array_unshift($foo, 'qux'); // 4
```

La fonction `array_push` ajoute un élément à la fin, renvoie sa nouvelle taille puis réorganise les clefs du tableau.

```php
echo array_push($foo, 'thud'); // 4
```

----------

## Object

Loin d’apprendre la programmation objet maintenant, penchons nous sur ce type.

Tous les objets possèdent une valeur qui est modifiée par référence : quand vous passerez un objet en argument et que vous le modifiez, vous ne modifiez pas une copie comme pour les types primitifs, il sera modifié dans le contexte d'appel.

### Déclaration

Il existe de nombreux objets intégrés et vous pouvez en définir également.

Instancier une `classe`.

```php
$obj = new stdClass();
```

Un constructeur standard est disponible avec la classe `stdClass`. C'est une classe dont vous pouvez ajouter et récupérer les attributs de façon publiques.

----------

### Manipulation

L'accès aux propriétés d'un objet se fait avec la flèche. Des propriétés non existantes peuvent être ajoutées à la volée.

```php
$obj->prop1 = true;
echo $obj->prop1; // true
```

#### Supprimer une propriété

Que ce soit pour supprimer une variable ou une propriété d'un objet, la fonction `unset` détruit la référence.

```php
unset($obj->prop1);
```

----------

### Instanceof

L'opérateur instanceof s'utilise pour vérifier si la première opérande est du type de la seconde.

```php
var_dump($obj instanceof stdClass);
```

----------

# Structures

## Opérateurs

### Arithmétiques

Les opérateurs arithmétiques effectuent une opération entre deux opérandes.

| Opération | Syntaxe | Exemple |
|--|--|--|
| Addition | + | a = a + x |
| Soustraction | - | a = a - x |
| Multiplication | * | a = a * x |
| Division | / | a = a / x |
| Modulo | % | a = a % x |
| Incrément préfixé | ++ | ++a |
| Incrément suffixé | ++ | a++ |
| Décrément préfixé | -- | --a |
| Décrément suffixé | -- | a-- |

#### Incrément

La chaine de caractères ne sera pas incrémentée dans l'ordre de valeur Unicode.

----------

### Affectation

Les opérateurs d'affectation affectent une valeur après avoir effectué un calcul, ils simplifient l'écriture d'opérations. Ils réunissent l'opérateur = et les opérateurs arithmétiques, les opérateurs binaires peuvent aussi êtres simplifiés par un opérateur d'affectation mais nous les aborderons plus tard.

| Opération | Syntaxe | Exemple |
|--|--|--|
| Affectation | = | a = x |
| Addition puis affectation | += | a += x |
| Soustraction puis affectation | -= | a -= x |
| Multiplication puis affectation | *= | a *= x |
| Division puis affectation | /= | a /= x |
| Modulo puis affectation | %= | a %= x |

#### Conversion

Pendant une opération si les valeurs ne correspondent pas au type attendu un warning sera déclenché.

----------

### Comparaison

Les opérateurs de comparaison effectuent une comparaison portant sur la valeur ou sur le type et la valeur, soit une comparaison stricte. Ils renvoient un boolean, true si les éléments sont égaux pour la comparaison ou false s'ils ne le sont pas.

| Opération | Syntaxe | Exemple |
|--|--|--|
| Supérieur | > | a > x |
| Supérieur ou égal | >= | a >= x |
| Inférieur | < | a < x |
| Inférieur ou égal | <= | a <= x |
| Égalité | == | a == x |
| Égalité Stricte | === | a === x |
| Inégalité | != | a != x |
| Inégalité stricte | !== | a !== x |

#### Égalité

Pour comparer une égalité non stricte, les valeurs seront converties. Un type peut être égal à un autre type si sa valeur convertie lui est égale. False peut être égal à une chaine vide, à une chaine qui contient 0, au nombre 0 ou à un tableau vide.

----------

### Logiques

Les opérateurs logiques renvoient uniquement des valeurs booléennes.

#### Et

L'opérateur `&&` renvoie true si ses deux opérandes valent true.

```php
var_dump(true && true);
```

#### Ou

L'opérateur `||` renvoie true si une de ses opérandes vaut true.

```php
var_dump(true || false);
```

#### Négation

L'opérateur `!` renvoie true si son opérande peut être convertie à false, sinon il renvoie false.

```php
var_dump(!false);
```

----------

### Concaténation

L'opérateur de concaténation est le point...

```php
$name = "John";
"Hello " . $name
```

L'opérateur de concaténation peut s'utiliser avec celui d'affectation

```php
$str = "Hello ";
$str .= $name;
```

----------

## Conditions

Le flux d'instructions peut être encapsulé dans des blocs qui s’exécutent si certaines conditions sont remplies. Les structures conditionnelles contrôlent les flux d'instructions et mettent en place la logique, l’algorithmique du programme.

### if else

La structure if vérifie une condition dans ses parenthèses puis exécute les instructions dans le bloc délimité par ses accolades si la condition vaut true.

> Si la condition vaut false le code ne sera pas exécuté. Dans le cas d’absence d'opérateurs, les valeurs chaine de caractères vide, 0, false, et null sont équivalentes à false.

```php
if (true == 1) {
    echo 'true';
}
```

La structure if possède une clause else qui est optionnelle. Le bloc délimité par else sera exécuté dans le cas où la condition précédente ne vaut pas true.

```php
if (true === 1) {
} else {
    echo 'true';
}
```

La clause else peut aussi posséder une condition pour que son bloc soit exécuté et ainsi continuer de tester différentes conditions pour contrôler le flux d'instructions plus précisément.

```php
if (true === 1) {
} else if (true == '1') {
    echo 'true';
} else {
}
```

#### Yoda condition

La bonne pratique quant on essaye de comparer un variable à une valeur est d'utiliser le Yoda condition.

```php
$foo = 0;
if (1 = $foo) {
}
```

Vous ne pouvez pas assigner le contenu d'une variable à une valeur. De cette manière, vous obtiendrez une erreur si par mégarde vous ne mettez qu'un seul signe égal.

----------

### Ternaire

L'opérateur ternaire est pratique pour vérifier une condition avant affectation mais pour ce faire il utilise trois opérandes. Le ? interroge la première opérande, si sa valeur peut être convertie à true alors la seconde opérande sera utilisée, sinon ce sera la troisième opérande.

```php
$foo = $operande1 ? $operande2 : $operande3;
```

----------

### Fusion Null

Il existe également l'opérateur "??" ou fusion null.

```php
$foo = $operande1 ?? $operande2;
```

L'expression retourne la seconde opérande si la première opérande est `null`, et la première opérande dans les autres cas.

En particulier, cet opérateur n'émet pas de notice ou avertissement si la partie gauche n'existe pas, exactement comme [isset()](https://www.php.net/manual/fr/function.isset.php). Ceci est particulièrement utile pour les clés des tableaux.

L'opérateur de fusion Null peut aussi s'utiliser avec l'opérateur d'affectation. On l'appelle l'opérateur de coalescence nul.

```php
$operande1 ??= $operande2;
```

----------

### switch

La structure switch n'évalue pas une condition mais la valeur de retour d'une expression afin d'exécuter les instructions suivant l'étiquette correspondant à son égalité faible.

```php
switch (2 + 3) {
    case 10:
        echo 10;
        break;
    default:
        echo 'default';
}
```

----------

### match

La structure match évalue l'expression sur la base d'une vérification d'identité d'une valeur. De la même manière qu'une instruction switch, la valeur de retour de l'expression est comparée à plusieurs alternatives. Contrairement à switch, la comparaison est un contrôle d'identité plutôt qu'un contrôle d'égalité faible.

```php
$return_value = match (expression) {  
    single_conditional_expression => return_expression,
    conditional_expression1, conditional_expression2 => return_expression,
    default => return_expression,
};
```

----------

## Exception

### try catch

L'instruction `try catch` est composée de deux blocs. Le premier bloc essaie d'exécuter une série d'instructions, si une exception est levée alors les instructions suivantes de ce bloc ne seront pas exécutées. Le bloc catch attrape l'exception dans son unique argument avant de le transmettre à son bloc contenant lui aussi des instructions destinées à traiter l'exception.

```php
try {
    echo 'try';
} catch (Throwable $e) {
    echo 'catch';
}
```

Si une erreur est levée dans le `try`, l'exécution continue dans le bloc du `catch`.

```php
try {
    new Foo();
    echo 'try';
} catch (Throwable $e) {
    echo 'catch'; // catch
}
```

Le bloc `finally` s'utilise pour exécuter des instructions après avoir essayé d'exécuter des instructions ou après avoir attrapé une erreur. Il est utile pour effectuer un traitement qu'il y ait eu des erreurs ou non.

```php
try {
    new Foo();
    echo 'try';
} catch (Throwable $e) {
    echo 'catch';
} finally {
    echo 'finally';
}
```

----------

### throw

L'instruction throw lève un levable.

```php
throw new Exception();
```

Il est possible de créer ses propres exceptions pour pouvoir attraper plus finement un type précis dans le catch mais il en existe des prédéfinies.

[Exceptions](https://www.php.net/manual/fr/reserved.exceptions.php)

```php
try {
    throw new Error();
} catch (Error $e) {
    echo 'catch error';
} catch (Exception $e) {
    echo 'catch exception';
} finally {
    echo 'finally';
}
```

----------

## Itérations

Une itération sert à répéter l'exécution d'instructions, pour parcourir un tableau ou un objet en peu de lignes il existe des structures itératives.

### while

- while (condition) [{}]

La boucle while s'appuie sur une condition. Tant que celle-ci est true, elle continuera à exécuter les instructions dans son bloc, jusqu'à ce que la condition devienne false ou qu'une instruction l'en fasse sortir.

```php
$i = 0;
while ($i < 5) {
    echo $i++;
}
```

----------

### do - while

- do [{}] while (condition);

Contrairement à la boucle while, la condition est testé à la fin de chaque itération plutôt qu'au début. Dans une boucle do-while, la première itération est toujours exécuté.

```php
$i = 0;
do {
    echo $i++;
} while ($i < 5);
```

----------

### for

-   for ([initiale]; [condition]; [increment]) [{}]

La boucle for s'appuie sur une expression initiale, une condition et une expression d'incrément pour effectuer une itération. Les expressions et la condition sont optionnelles, mais sans elles il faudra vérifier la condition d'itération à l'intérieur du bloc d'instruction.

```php
for ($i = 0; $i < 5; $i++) {
    echo $i; // 0 1 2 3 4
}
```

----------

### foreach

-   foreach ($array as $value) {}

La boucle foreach peut itérer tous les objets itérables selon leurs mécanismes d'itération. Il parcourt la première opérande sur la valeur de ses propriétés ou de ses éléments qu'il affecte à la seconde opérande.

```php
$array = ["John", "Bryan"];
foreach ($array as $value) {
    echo $value; // John, Bryan
}
```

-   foreach ($array as $key => $value) {}

Il est possible de demande l'indice du tableau ou le nom de la propriété de l'objet en cours d'itération

```php
$array = ["John", "Bryan"];
foreach ($array as $key => $value) {
    echo $key . $value; // 0John, 1Bryan
}
```

----------

### Contrôle de l'itération

#### break

L'instruction break permet d’arrêter l'exécution d'une boucle.

```php
for ($i = 0; $i < 5; $i++) {
    if ($i === 3) {
        break;
    }
    echo $i; // 0, 1, 2
}
```

#### continue

L'instruction continue permet d’arrêter l'itération en cours d'une boucle.

```php
for ($i = 0; $i < 5; $i++) {
    if ($i === 3) {
        continue;
    }
    echo $i; // 0, 1, 2, 4
}
```

----------

## Fonctions

Les fonctions sont des objets Function qui permettent d'encapsuler des instructions dans un bloc afin d'y faire appel. Les fonctions peuvent posséder des arguments afin de leur transmettre des valeurs et peuvent également retourner une valeur de fin d'instruction.

### Déclaration

-   function identifiant([param1[, param2[, ...,paramN]]]) {}

Une fonction peut être une expression ou une instruction, dans les deux cas elles sont un objet Function.

```php
function maFonction()
{
    echo "Hello";
}
```

#### return

-   return [expression = null];

L'instruction return renvoie la valeur de l'expression qui lui succède et met fin à l'exécution des instructions d'une fonction. L'expression de retour est optionnelle et sa valeur par défaut est null.

```php
function maFontion()
{
    return true;
}

echo maFontion(); // true
```

#### Les arguments

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

#### Typage

Depuis PHP7 il est possible de typer en primitif et en non primitif les arguments et la valeur de retour de la fonction.

```php
function division(float $dividende, float $diviseur = 1): float
{
    return $dividende / $diviseur;
}
```

Si vous fournissez le mauvais type la valeur sera convertie si c'est possible.

#### Portée

Une variable déclarée dans une fonction est locale: elle n'est pas disponible en dehors de la fonction. Pour qu'une fonction utilise une variable déclarée localement, il faut utiliser le mot `global`.

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

# Projet

Nous nous apprêtons à en découvrir d'avantage sur le langage PHP, je vous invite à le faire en visant des objectifs fonctionnels. De ce fait, nous allons développer un projet que vous pourrez continuer par la suite, au fur et à mesure de votre apprentissage du langage PHP.

Pour cela, nous utiliserons plusieurs outils :

## [Git](https://git-scm.com/)

Git est un logiciel de versioning, open source et gratuit.

----------

## [Composer](https://getcomposer.org/)

Composer est le package manager pour écosystème PHP, les package installables reposent sur le site associé [Packagist](https://packagist.org/).

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

# XSS

## Définition

Le cross-site scripting (abrégé XSS) est un type de faille de sécurité des sites web permettant d'injecter du contenu dans une page, provoquant ainsi des actions sur les navigateurs web visitant la page.

Il y a 3 catégories d'injection XSS possibles : reflected, stored, DOM Based. La troisième utilise le fragment de l'URL qui n'est pas envoyé à PHP et ne nous concerne pas. En revanche le deux premières nous intéressent.

### Reflected

Si une portion d'url contient de la donnée potentiellement capable d’exécuter un script comme:

```html
?name=<script>alert("Hey")</script>
```

Et si cette donnée est affichée par notre programme sans être sécurisée:

```php
echo filter_input(INPUT_GET, "name");
```

Alors il y a un problème concernant la sécurité des données de l'utilisateur qui affiche cette page. En effet JavaScript a la capacité d'enregistrer des évènements pour capturer la saisie utilisateur, la capacité de vider le stockage local du navigateur et d'envoyer ces informations à un serveur pour qu'elles soient stockées.

### Stored

Une injection XSS peut être plus persistent et concerner tous les utilisateurs si la valeur malveillante est stockée dans une base de données et ré-affichée sans protection pour tous les utilisateurs qui accèdent à une page qui fait une extraction de donnée pour l'afficher d'une façon non sécurisée.

----------

## [Filter](https://www.php.net/manual/fr/filter.filters.php)

Vous devez au niveau de vos vues échapper la donnée avant de l'afficher.

### [filter_var](https://www.php.net/manual/fr/function.filter-var.php)

`filter_var` est utile pour cela, elle prend en argument la valeur à échapper puis des drapeaux de validation ou de nettoyage. Le drapeau de nettoyage nous intéresse.

```php
echo filter_var($name, FILTER_SANITIZE_FULL_SPECIAL_CHARS);
```

### [filter_input](https://www.php.net/manual/fr/function.filter-input.php)

`filter_input` peut aussi utiliser des filtres.

```php
echo filter_input(INPUT_GET, "name", FILTER_SANITIZE_FULL_SPECIAL_CHARS);
```

----------

# Regex

## [Définition](https://www.php.net/manual/fr/reference.pcre.pattern.syntax.php)

Une expression rationnelle ou régulière représente un motif qui sera utilisé pour vérifier s'il correspond à des données que l'on souhaite comparer ou extraire.

### [preg_match](https://www.php.net/manual/fr/function.preg-match.php)

Effectue une recherche de correspondance avec une expression rationnelle standard.

```php
echo preg_match('/(foo)(bar)/', 'foobar', $matches); // 1
print_r($matches); //Array ( [0] => foobar [1] => foo [2] => bar )
```

### Filters

filter_var ou filter_input peuvent valider une donnée en fonction d'une expression régulière.

```php
echo filter_var('foobar', FILTER_VALIDATE_REGEXP, [
    "options" => [
        "regexp" => '/(foo)(bar)/'
    ]
]); // foobar
```

Nous pouvons savoir si une chaine de caractère correspond au motif passé en premier argument et également extraire les motifs correspondants. Nous allons passez en revue la syntaxe des expressions régulières pour valider nos données entrantes.

----------

## [Délimiteurs](https://www.php.net/manual/fr/regexp.reference.delimiters.php)

Lors de l'utilisation des fonctions PCRE, il est nécessaire que le motif soit encadré par des délimiteurs. Un délimiteur peut être n'importe quel caractère non alpha-numérique autre qu'un backslash ou qu'un espace.

```php
$regex = "#foobar#";
```

----------

## [Drapeaux](https://www.php.net/manual/fr/reference.pcre.pattern.modifiers.php)

Un drapeau est utile pour préciser comment la correspondance doit se faire entre le motif et les données.

| Correspondance | Flag | Syntaxe |
|--|--|--|
| Insensible à la casse | i | `#motif#i` |
| Recherche ligne par ligne | m | `#motif#m` |
| Le masque et la chaîne d'entrée sont traitées en UTF-8. | u | `#motif#u` |

```php
echo preg_match('#\x{0066}oo#u', 'foobar', $matches); // 1
```

----------

## Limites

Un motif peut comporter des limites, pour marquer le début ou la fin d'une entrée par exemple.

| Correspondance | Limite | Syntaxe |
|--|--|--|
| Début de la chaine ou de la ligne selon le drapeau | ^ | `#^motif#` |
| Fin de la chaine ou de la ligne selon le drapeau | $ | `#motif$#` |
| Limite de mot | \b | `#\bmotif#` |
| Pas limite de mot | \B | `#\Bmotif#` |

```php
echo preg_match('#^foo#', 'foobar', $matches); // 1
```

```php
echo preg_match('#bar$#', 'foobar', $matches); // 1
```

```php
echo preg_match('#\bbar#', 'foo bar', $matches); // 1
```

```php
echo preg_match('#\Bbar#', 'foobar', $matches); // 1
```

----------

## Ensemble de caractères

Les crochets regroupent un ensemble de caractères, des caractères ou des intervalles de caractères peuvent y figurer.

| Correspondance | Ensemble | Syntaxe |
|--|--|--|
| Un ensemble de caractères | [aeiou] | `#[aeiou]#` |
| Un ensemble de caractères | [a-z] | `#[a-z]#` |
| Un ensemble de caractères exclus | [^a-z] | `#[^a-z]#` |

```php
echo preg_match('#[aeiou]#', 'Hello', $matches); // 1
```

```php
echo preg_match('#[^A-Z]#', 'HELLO', $matches); // 1
```

----------

## [Classe de caractères](https://www.php.net/manual/fr/regexp.reference.character-classes.php)

Afin de décrire des ensembles de caractères plus simplement, les classes de caractères représentent des ensembles de caractères.

| Correspondance | Classe | Syntaxe |
|--|--|--|
| Tous les caractères exceptés saut de ligne et retour chariot | . | `#.#` |
| Caractères numériques | \d | `#\d#` |
| Caractères non numériques | \D | `#\D#` |
| Caractères alphabétiques et numériques | \w | `#\w#` |
| Caractères non alphabétiques et non numériques | \W | `#\W#` |
| Caractères blancs | \s | `#\s#` |
| Caractères non blancs (`\t \n \r`) | \S | `#\S#` |

```php
echo preg_match('#\d#', 'fo0', $matches); // 1
```

----------

## [Quantificateurs](https://www.php.net/manual/fr/regexp.reference.repetition.php)

Les quantificateurs permettent de quantifier des caractères dans un motif.

| Correspondance | Quantificateur | Syntaxe |
|--|--|--|
| Aucun ou plusieurs fois | * | #x*# |
| Une ou plusieurs fois | + | #x+# |
| Aucune ou une fois | ? | #x?# |
| S'il est précédé par y | (?=) | #x(?=y)# |
| S'il n'est pas précédé par y | (?!) | #x(?!y)# |
| Correspond à n occurrences | {n} | #x{n}# |
| Correspond à n occurrences ou plus | {n,} | #x{n,}# |
| Correspond à un intervalle entre n et m occurrences | {n,m} | #x{n,m}# |

```php
echo preg_match('#(foo){2}#', 'foobar', $matches); // 0
```

----------

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
$includePath = __DIR__ . "/../var/cache/";
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

Nous allons regardez a fonction qui accompagne celle observée précédemment.

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

# Sessions

## [Définition](https://www.php.net/manual/fr/reserved.variables.session.php)

Les sessions sont un moyen simple de stocker des données individuelles pour chaque utilisateur en utilisant un identifiant de session unique. Elles peuvent être utilisées pour faire persister des informations entre plusieurs pages. Les identifiants de session sont normalement envoyés au navigateur via des cookies de session, et l'identifiant est utilisé pour récupérer les données existantes de la session. L'absence d'un identifiant ou d'un cookie de session indique à PHP de créer une nouvelle session, et génère ainsi un nouvel identifiant de session.

### Mécanisme

En PHP il faudra démarrer la session, à ce moment il y a deux possibilités.

-   Si le client n'est jamais venu

PHP génère un identifiant de session unique pour le client et créé un fichier dans le dossier temporaire du serveur afin de stocker ses données. Les données que l'on voudra personnelle à l'utilisateur devront être affectée à la super globale `$_SESSION`. PHP ajoute aux entêtes de réponse un header setCookie avec l'identifiant de session afin que le navigateur enregistre ce cookie en mémoire.

-   Sinon

Un cookie existe chez le client et il envoie ce cookie dans les entêtes de la requête. Le serveur intercepte le cookie, ouvre le fichier de session de l'utilisateur avec l'identifiant de session stocké dans le cookie et peuple la super globale $_SESSION des informations dans le fichier.

### State

Avec ce mécanisme, un client peut avoir un résultat de réponse qui lui sera personnelle, pour la même adresse des clients auront des résultats différents, l'on parle alors d'application avec état, avec une mise en cache pour que les données de l'un ne soit pas disponible pour un autre. A l'inverse d'un web service.

----------

## [Start](https://www.php.net/manual/fr/function.session-start.php)

La fonction `session_start` Démarre une nouvelle session ou reprend une session existante. Vous devez l'exécuter avant qu'un affichage se produise parce que cette fonction envoie des entêtes http.

```php
session_start();
```

### Utilisation

Après avoir démarré une session, vous pouvez utiliser $_SESSION. C'est un tableau qui stock les données de l'utilisateur.

```php
if (!array_key_exists("count", $_SESSION)) {
    $_SESSION["count"] = 0;
}

echo ++$_SESSION["count"];
```

D'une requête à l'autre les valeurs de la session sont conservée grâce au mécanisme expliqué précédemment.

----------

## [Stop](https://www.php.net/manual/fr/function.session-destroy.php)

Pour détruire les données de l'utilisateur il faut utiliser `session_destroy`. Cette fonction ne détruit pas les variables globales associées à la session, de même, elle ne détruit pas le cookie de session.

```php
session_destroy();
```

Mais attention, il faut également détruire le cookie de session coté client afin qu'il ne le renvoie pas, en envoyant un programmatiquement et en fournissant une date passée.

### Utilisation

```php
session_destroy();
unset($_SESSION);
$params = session_get_cookie_params();
setcookie(
    session_name(),
    null,
    strtotime('yesterday'),
    $params["path"], $params["domain"],
    $params["secure"], $params["httponly"]
);
```

----------

## Configuration

Vous pouvez configurer la session de 3 façon différentes. Dans le php.ini, avec la fonction ini_set ou directement à l'ouverture de la session.

```php
session_start([
    "cache_limiter" => "nocache",
    "cookie_httponly" => 1,
    "cookie_path" => "/",
    "use_cookies" => 1,
    "use_only_cookies" => 1,
    "use_strict_mode" => 1,
    "use_trans_sid" => 0,
]);
```

----------

### Lifetime

La durée de vie de la session n'est pas contrôlée, nous allons étudier les directives correspondant à sa durée de vie sur le disque et sa fréquence de nettoyage et la durée de vie du cookie. Par défaut la durée de vie du cookie vaut 0, le cookie est valide jusqu’à ce que le navigateur se ferme et sans limite de durée de vie ce qui est recommandé par php.net.

```php
ini_set("session.cookie_lifetime", 0);
```

Mais vous pouvez avoir besoin que le cookie possède une date d'expiration précise que le navigateur reste ouvert ou non. Dans ce cas en précisant une date d'expiration, le cookie ne sera plus utilisé quand la date d'expiration est dépassée, que le client soit actif ou non. L'impact est que si le client navigue depuis un certain temps et atteint la date d'expiration il se retrouve déconnecté du service même s'il est actif durant toute cette période. En précisant une date d'expiration il faut envoyer manuellement un cookie pour repousser la date d'expiration pour qu'elle corresponde à la date courante de rafraichissement plus celle d'expiration. Pour une expiration par exemple de 10 minutes sans que l'utilisateur se retrouve déconnecté malgré son activité il vaut mieux définir le cookie sans passer par la directive.

```php
ini_set("session.cookie_lifetime", 3600);
$params = session_get_cookie_params();
setcookie(
    session_name(),
    "",
    strtotime('+1 hour'),
    $params["path"],
    $params["domain"],
    $params["secure"],
    $params["httponly"]
); 
```

### Garbage

La gestion de la durée de vie coté client a été abordée avec les cookies mais la durée de vie sur le disque peut aussi être configurée. La directive `gc_maxlifetime` définit une date d'expiration de la durée de vie du fichier sur le disque, si cette date arrive à expiration et que le garbage collector est appelé il supprimera le fichier. Le passage du GC peut être régulé en utilisant `gc_probability` et `gc_divisor`, dans l'exemple suivant le garbage est appelé avec une probabilité de 1/10.

```php
ini_set("session.gc_maxlifetime", 3600);
ini_set("session.gc_divisor", 10);
ini_set("session.gc_probability", 1);
```

### Regenerate

Pour se protéger efficacement contre la `fixation de session`, il faut penser à renouveler l'identifiant à chaque changement de privilège puis à chaque intervalle de temps régulier.

```php
session_regenerate_id(true);
```

----------

# PDO

## [Définition](https://www.php.net/manual/fr/book.pdo.php)

L'extension PHP Data Objects (PDO) définit une excellente interface pour accéder à une base de données depuis PHP. Chaque pilote de base de données implémenté dans l'interface PDO peut utiliser des fonctionnalités spécifiques de chacune des bases de données en utilisant des extensions de fonctions. Notez que vous ne pouvez exécuter aucune fonction de base de données en utilisant l'extension PDO par elle-même ; vous devez utiliser un driver PDO spécifique à la base de données pour accéder au serveur de base de données.

### Configuration

Dans le fichier `php.ini`, l'extension de votre driver doit être présente et linkée.

```ini
extension=mysqli
```

Les extensions se trouvent dans `php/ext/`. Pour l'extension décrite le fichier suivant doit être présent: `php_pdo_mysql.dll`.

### Prérequis

Les prérequis pour manipuler une base de données est la connaissances d'un langage de base de données ainsi que sa structuration.

----------

## [Instanciation](https://www.php.net/manual/fr/pdo.construct.php)

Le `Data Source Name` en argument un doit posséder au moins **le type de drive et le host**.

```php
$dbh = new PDO(
    "mysql:host=some_hostlhost;dbname=some_database_name;charset=UTF8",
    "user",
    "password", [
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION
    ]
);
```

Il est important de **spécifier en option le mode erreur** à exceptions afin de pouvoir attraper les levables facilement et ne pas tester chaque exécution.

----------

## [Prepare](https://www.php.net/manual/fr/pdo.prepare.php)

Prépare une requête à l'exécution et retourne un objet.

### Requête

```php
$sth = $dbh->prepare("SELECT * FROM `my_table`");
```

### Valeurs

Afin de se prémunir de toute interprétation, et donc d'injection SQL, il est préférable de **spécifier les valeurs en dehors de la chaine de caractère SQL**

```php
$sth = $dbh->prepare("SELECT * FROM `my_table` WHERE `id`=:id");
$sth->bindValue(":id", 4);
```

### [Exécution](https://www.php.net/manual/fr/pdostatement.execute.php)

Exécute une requête préparée.

```php
$sth->execute();
```

### [Lecture](https://www.php.net/manual/fr/pdostatement.execute.php)

-   Lire une ligne

```php
$raw = $sth->fetch();
```

-   Lire plusieurs lignes

```php
$raws = $sth->fetchAll();
```

-   Personnaliser le mode de lecture

```php
$sth->setFetchMode(PDO::FETCH::ASSOC);
```

----------

## [Transaction](https://www.php.net/manual/fr/pdo.transactions.php)

Dans le cas de plusieurs exécution, il est important de pouvoir annuler l'une d'entre elle si une erreur apparait. **La transaction permet de valider ou d'annuler un ensemble exécutions** contenu dans un bloc.

### [Open](https://www.php.net/manual/fr/pdo.begintransaction.php)

Démarre une transaction.

```php
$dbh->beginTransaction();
```

### [Cancel](https://www.php.net/manual/fr/pdo.rollback.php)

Annule une transaction.

```php
$dbh->rollBack();
```

### [Valid](https://www.php.net/manual/fr/pdo.commit.php)

Valide une transaction.

```php
$dbh->commit();
```

----------

## [Static](https://www.php.net/manual/fr/language.variables.scope.php#language.variables.scope.static)

Le statisme peut aider à limiter le nombre d'instance en vie de PDO. Une variable statique a une portée locale uniquement, mais elle ne perd pas sa valeur lorsque le script appelle la fonction.

```php
function foo () {
    static $bar = 0;
    return ++$bar;
}
echo foo(); // 1
echo foo(); // 2
```










## Rewrited

Comme vous le constatez il n'est pas possible par défaut d'obtenir des url personnalisées. Ainsi vous exposez le nom de vos scripts et êtes limités pour fournir des url user friendly ce qui est une mauvaise pratique.

> Que vous utilisiez l'une ou l'autre des exécutions il nous faut activer la réécriture d'URL, c'est à dire le fait de pouvoir avoir l'url [http://localhost/user/2](http://localhost/user/2) et qu'on ne tombe pas sur une page objet non trouvé. En PHP toutes les url doivent exécuter votre script principal, votre index.php situé à la racine de votre dossier public. C'est le point d'entré de votre programme.

### .htaccess

Pour ce faire nous allons dans un fichier donner des directive au server apache. Le fichier .htaccess contient ces directives.

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
