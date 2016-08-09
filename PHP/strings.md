## Strings
In PHP strings in single quotes and double quotes are used differently.
- Single quotes represent simple strings, in which almost all characters are used literally.
- Double quotes encapsulate complex strings that allow for special escape sequences and for variable substitution, ahich makes it possible to embed the value of a variable deirctly in a string, without the need for any special operator.

#### Variable iterpolation
```php
$me = 'Davey';
$names = array('Smith', 'Jones', 'Jackson');

echo "Thee cannot be more than two {$me}s!";
echo "Citation: {$names[1]}[1987]}";
```

#### Heredoc
Heredoc behaves like double quotes in every way:
```php
$who = "World";
echo <<<TEXT
So I said, "Hello $who"
TEXT;

// displays So I said, "Hello World"
```

#### Nowdoc (PHP 5.3)
In nowdoc no interpolation is done, and the entire string is considered literal, so all $ and escape sequences are ignored:
```php
$who = "World";
echo <<<'TEXT'
So I said, "Hello $who"
TEXT;

// displays So I said, "Hello $who"
```
