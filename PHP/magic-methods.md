##Magic Methods
Magic methods perform functionality in addition to that of ordinary functions/methods.

####__construct()

####__destruct()

####__call()
If you call a method that has not been defined, the class’s ```__call()``` method will be called instead.
```php
class Car {
  public function __call($name, $arguments) {
    echo "hello world!";
  }
}

$car = new Car();
$car->hello();  // since there is no such method in that class, __call() will be called.
```
