## Closures
PHP 5.3 added anonymous functions, otherwise known as Closures. Closures allow you to define anonymous functions that can be passed around as callbacks. Closures can be used as callbacks for any function that accepted traditional callbacks prior to 5.3, such as usort().
```php
$closure = function($who) {
  echo "Hello $who";
}

$closure("World"); // displays "Hello World"
```
```$closure``` variable is actually an instance of the ```Closure``` class.

A closure encapsulates its scope, meaning that it has no access to the scope in which it is defined or executed. It is, however, possible to inherit variables from the parent scope (where the closure is defined) into the closure with the ```use``` keyword. This inherits the variables by-value, that is, a copy is made available inside the closure using its original name:
```php
function createGreeter($who) {
  return function() use ($who) {
    echo "Hello $who";
  };
}

$greeter = createGreeter("World");
$greeter(); // displays "Hello World"
```
#### Using ```$this``` in closures
```php
class foo {
  public function getClosure() {
    return function() { 
      return $this; 
    };
  }
}

class bar {
  public function __construct() {
    $foo = new foo();
    $func = $foo->getClosure();
    $obj = $func(); // PHP 5.3: $obj == null
      // PHP 5.4: $obj == foo, not bar
  }
}
```
In PHP 5.4 and later, when a closure is defined within an object scope, ```this``` is determined by the object within whose scope it is defined (or in which it is inherited for child classes). This can be changed after the fact by using the ```bindTo``` and (static) ```bind``` methods of the closure class. Using either of these methods will not modify the closure itself; instead it will create a clone of the closure with ```$this``` modified.

It is possible to change the $this independently from the scope, meaning that unlike a regular method you may not have access to all of the methods on ```$this``` unless the scope is also the same class of which $this is an instance.
```
class Greeter {
  public function getClosure() {
    return function() {
      echo $this->hello;
      $this->world();
    };
  }
}

class WorldGreeter {
  public $hello = "Hello ";
  private function world() { echo "World"; }
}
```
Here we have a class ```Greeter```, which returns a closure that outputs a property, ```$this->hello```, and then calls a method ```$this->world()```, neither of which exist in the ```Greeter``` class. We then create another—completely separate—class, ```WorldGreeter```, which has both the property and method we wish to call.

To allow this to work, we can rebind ```$this``` to an instance of ```WorldGreeter``` by calling the ```Closure->bindTo()``` method on our closure.
```php
$greeter = new Greeter();
$closure = $greeter->getClosure();
$worldGreeter = new WorldGreeter();
// Rebind $this and scope to $worldGreeter
$newClosure = $closure->bindTo($worldGreeter, 'WorldGreeter');
$newClosure(); // Hello World
```
or using static ```bind()```
```php
$greeter = new Greeter();
$closure = $greeter->getClosure();
$worldGreeter = new WorldGreeter();
// Rebind $this and scope to $worldGreeter
$newClosure = Closure::bind($closure, $worldGreeter, 'WorldGreeter');
$newClosure(); // Hello World
```
To unbind a closure, pass in null for the new ```$this```.
