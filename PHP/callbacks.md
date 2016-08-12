##Callbacks
#### Internal Functions
Prior to PHP 5.3, PHP supported limited types of callbacks. The most simple is a string containing a valid function name:
```php
$callback = "myFunction";
usort($array, $callback);
```
