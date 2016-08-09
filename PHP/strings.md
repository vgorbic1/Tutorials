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

#### Length of String
Use ```strlen()``` function to determine the length (in bytes) of a string. It is binary-safe, which means that all characters in the string are counted, reagrdless of their value.

#### Transforming a String
Use ```strtr() function to translate certain characters of a string into other charactrs. Used in transliteration to transform certain accented charactrs that cannot appear:
```php
// translate a single character
echo strtr('abc', 'a', '1'); // outputs 1bc

// translate multiple-cjaracters
$subst = array('1' => 'one', '2' => 'two');
echo strtr('123', $subst); // outputs onetwo3
```

#### Comparing, Searching and Replacing Strings
Use ```strcmp()``` or ```strcasecmp()```:
```php
$str = "Hello World";

if (strcmp($str, "hello world") === 0) {
  // We won't get here, because of case sensitivity
}

if (strcasecmp($str, "hello world") === 0) {
  // We will get here, because strcasecmp() is case-insensitive
}
```
