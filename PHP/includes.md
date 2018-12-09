## Including Code from other files

Normally, ```include()``` is the only command you need. It continues processing the code even included file is missing.
- ```require()``` is used when the file is mandatory.
- ```require_once()``` and ```include_once``` is to ensure that the external file doesn't reset any variables that may bhave been assigned  a new value elsewhere.

To find the absolute path to the site's server root:
```php
include($_SERVER['DOCUMENT_ROOT'].'/includes/filename.php;
```
Another way is to find the path to the main index.php file:
```php
<?php // index.php in the root of applicaton
  $root = realpath(dirname(__FILE__));
?>
```
Now ```$root``` value is the absolute path to the index.php and the root of the application. 

[More on paths here](https://phpdelusions.net/articles/paths).
