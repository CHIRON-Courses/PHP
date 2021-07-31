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

[Retour au sommaire](00_sommaire.md)