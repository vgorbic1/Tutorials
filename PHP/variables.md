## Variables

#### Global
Global variables are declared outside a function.

#### Heredoc
Heredoc is an alternative way for encapsulating strings. This text needs any double quotes:
```php
$tobe = <<<EOT
  To Be or not to be, that is the question \n
  Weather tis $my_var in the mind to suffer
  The Slings and Arrows of outrageous Fortune
EOT;
```
You can use anything instead the word EOT! OUTPUT or anything else will work! There should be nothing on the same line after the initial identifier, not even a space! The closing identifier has to be the very first item on the line (it cannot be indented at all) and can only be followed by a semicolon! People use EOT or EOD because it is unlikely to find them in a string.

#### Variables embedded in a string
Only double quotes allow for inserting a variable:
```php
$string = "this text allows for this $word inserted";
```
To get the type of any variable use:
```php
gettype($your_variable);
```
#### Variable variables
Variable variables is a variable whose name is contained in another variable:
```php
$name = 'foo';
$$name = 'bar';

echo $foo; // displays 'bar'
```
In other words content of one variable references another variable. Now you can do this:
```php
$name = `123';
$$name = '456';
echo ${'123'}; didplays '456';
```
Variable variables are a very powerful tool and should be used with extreme care.

#### Inspecting content of variables
- ```echo```.
- ```print_r()```. It provides a little more info than ```echo```
- ```var_dump()```. It also displays the type and the length.

#### Determine if a variable exists
```php
if (isset($x)) {
  // Do something if $x is set
} elseif (!isset($x) {
  // Do something if $x is not set
}
```
If variable exists and is anything but NULL, TRUE will be returned. 

#### Determine if a variable is empty
```php
$x = "0";
if (empty($x)) {
  // true
```
Returns TRUE if value passed to it is NULL, or any value that can be coerced to false, oncludeing an empty string, an empty array, integer zero, and string 0.
