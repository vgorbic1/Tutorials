##Magic Methods
Magic methods perform functionality in addition to that of ordinary functions/methods.

####__construct()
The ```__construct``` was introduced in PHP5 and it is the right way to define your, well, constructors (in PHP4 you used the name of the class for a constructor). You are not required to define a constructor in your class, but if you wish to pass any parameters on object construction then you need one.
```php
class Database {
  protected $userName;
  protected $password;
  protected $dbName;

  public function __construct ( $UserName, $Password, $DbName ) {
    $this->userName = $UserName;
    $this->password = $Password;
    $this->dbName = $DbName;
  }
}

// and you would use this as:
$db = new Database ( 'user_name', 'password', 'database_name' );
```

####__destruct()
PHP 5 introduces a destructor concept similar to that of other object-oriented languages, such as C++. The destructor method will be called as soon as there are no other references to a particular object, or in any order during the shutdown sequence.
```php
class MyDestructableClass {
   function __construct() {
       print "In constructor\n";
       $this->name = "MyDestructableClass";
   }

   function __destruct() {
       print "Destroying " . $this->name . "\n";
   }
}

$obj = new MyDestructableClass();
```

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
