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
Use ```strtr()``` function to translate certain characters of a string into other charactrs. Used in transliteration to transform certain accented charactrs that cannot appear:
```php
// translate a single character
echo strtr('abc', 'a', '1'); // outputs 1bc

// translate multiple-cjaracters
$subst = array('1' => 'one', '2' => 'two');
echo strtr('123', $subst); // outputs onetwo3
```

#### Comparing Strings
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

#### Simple Searching Functionality
The simplest way to search inside a string is to use the ```strpos()``` and ```strstr()``` families of functions.

**strpos()**

Used to find the position of a substring (called the needle) inside a string (the haystack) It returns either the numeric position of the needle's first occurrence within the haystack, or false if a match cound not be found:
```php
$haystach = "abcdefg";
$needle = 'abc';

if (strpos($haystack, $needle) !== calse) {
  echo 'Found';
}
```
You can specify the third parameter to strpos() to indicate that you want the search to start from a specific position within the haystack.
```php
$haystach = "123456123456";
$needle = '123';

echo strpos($heystack, $needle);  // outputs 0
echo strpos($heystack, $needle, 1 ); // outputs 6
```

**strstr()**

Used to search the haystack for a needle. It is slower than ```strpos()``` The function returns the portion of the haystack that starts with the needle istead of the position:

```php
$haystack = '123456';
$needle = '34';
echo strstr($haystack, $needle); // outputs 3456
```
You can specify the third parameter to strstr() to indicate that you want the search to start from a specific position within the haystack.

#### Matching Against a Mask
Use ```strspn()``` function to match a string against a "whitelist" mask of allowed characters. It returns the length of the initial segment of the string that contains any of the chartacters specified in the mask:
```php
$string ='133445abcdef';
$mask = '12345';

echo strspn($string, $mask); // outputs 6
```
Use ```strcspn()``` with a "blacklist" mask, to specify which caracters are disallowed. It returns the length of the initial segment of the string that does not contain any of the characters from the mask.
Specify two optional characters that define the starting position and the length of the string to examine.

#### Simple Search and Replace Operations
Use ```str_replace()``` as a simple substitution of a string. Or as cse-insensitive ```str_ireplace```:
```php
// Outputs Hello Reader
echo str_replace("World", "Reader", "Hello World");
```
Optionally, you can specify a third parameter, passed by reference, tha the function fills, upon return, with the number of substitutions made:
```php
$a = 0; 
str_replace('a', 'b', 'a1a1a1', $a);
echo $a; // outputs 3
```
If you need to search and replace more than one needle at a time, you can pass the first two arguments to ```str_replace()``` in the form of arrays:
```php
// outputs Bonjure Monde
echo str_replace( 
  array("Hello", "World"), 
  array("Bonjour", "Monde"),
  "Hello World" );
  ```
  The first element of the search array is replaced by the first element of the replacement array.
  ```php
  // outputs Bye Bye
  echo str_replace(
    array("Hello", "World"),
    "Bye",
    "Hello World");
    ```
    Sinc only the needle argument is an array, both search terms are replaced by the same string resultin in "Bye Bye".
    
    Combining ```substr_replace()``` with ```strpos()```:
    ```php
    $user = "david@example.com";
    $name = substr_replace($user, "", strpos($user, '@'));
    echo "Hello " . $name;
    ```
    
