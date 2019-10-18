## Including Code from other files

Normally, ```include()``` is the only command you need. It continues processing the code even included file is missing.
- ```require()``` is used when the file is mandatory. Simply we can say if file is not found include will produce warnings but require will produce fatal error.
- ```require_once()``` and ```include_once``` is to ensure that the external file doesn't reset any variables that may bhave been assigned  a new value elsewhere. ```require``` includes specific file but ```require_once``` does that only if it has not been included before. ```require_once``` checks file has been included before or not and only include file if file has not been included.

If you have to include a file on different files several times then you must use ```require_once```.

```include()``` will include the file but ```include_once()``` will include file if the file has not been included before. Exactly same difference as ```require``` and ```require_once``` but it will show include behavior. 

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
