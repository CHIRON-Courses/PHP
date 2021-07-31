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

Dans le cas de plusieurs exécution, il est important de pouvoir annuler l'une d'entre elle si une erreur apparait. **La transaction permet de valider ou d'annuler un ensemble exécution** contenu dans un bloc.

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

----------

[Retour au sommaire](00_sommaire.md)