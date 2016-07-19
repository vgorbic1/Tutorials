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
