##Singleton
The Singleton is probably the simplest design pattern. Its goal is to provide access to a single resource that is never duplicated, but that is made available to any portion of an application that requests it without the need to keep track of its existence. The most typical example of this pattern is a database connection, which normally only needs to be created once at the beginning of a script and then used throughout its code. Here’s an example implementation:
```php
class DB {
  private static $_singleton;
  private $_connection;
  
  private function __construct($dsn) {
    $this->_connection = new PDO($dsn);
  }
  
  public static function getInstance() {
    if (is_null(self::$_singleton)) {
      self::$_singleton = new DB();
    }
    return self::$_singleton;
  }
}

$db = DB::getInstance();
```
We have made the constructor private, which effectively ensures that the class can only be instantiated from within itself. ```getInstance()``` method, which checks whether the static property ```$_singleton``` has been initialized and, if it hasn’t, sets it to a new instance of DB. From this point on, ```getInstance()``` will never attempt to create a new instance of DB, and instead will always return the ```initialized $_connection```, thus ensuring that a database connection is not created more than once.
