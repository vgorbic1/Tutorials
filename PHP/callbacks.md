##Callbacks
#### Internal Functions
Prior to PHP 5.3, PHP supported limited types of callbacks. The most simple is a string containing a valid function name:
```php
$callback = "myFunction";
usort($array, $callback);
```
Using arrays to specify callbacks:
```php
// object method call:
$callback = [$obj, 'method']; // $obj->method() callback
usort($array, $callback);
// or static method:
$callback = ['SomeClass', 'method']; // SomeClass::method()
usort($array, $callback);
```
With the introduction of Closures in 5.3, you can now use a closure itself, as well as using an object as a callback if it defines the ```__invoke()``` magic method.
```php
class Sorter() {
  public function __invoke($a, $b) {
  // Sort
  }
}

$sorter = new Sorter();
usort($sorter);
```
#### Userland Functions
Prior to PHP 5.4, you could only use the simple string callbacks in userland— this was known as a dynamic function call—however, in PHP 5.4 all valid callbacks can be used.
```php
// Variable Functions
$callback = "myFunction";
$callback();

// object method call:
$callback = [$obj, 'method']; // $obj->method() callback
$callback();
// or static method:
$callback = ['SomeClass', 'method']; // SomeClass::method()
$callback();

// Closures
$callback = function() { }
$callback();

// Objects with Invoke magic method:
class invokeCallback {
  public function __invoke() { }
}

$callback = new invokeCallback();
$callback();
```
