## Registry
By taking the Singleton pattern a little further, we can implement the Registry pattern. This allows us to use any object as a Singleton without it being written specifically that way.

The Registry pattern can be useful, if, for example, for the bulk of your application, you use the same database connection, but need to connect to an alternate database to perform a small set of tasks every now and then. If your DB class is implemented as a Singleton, this is impossible (unless you implement two separate classes, that is)—but a Registry makes it very easy:
```php
class Registry {
  private static $_register;
  public static function add(&$item, $name = null) {
    if (is_object($item) && is_null($name)) {
      $name = get_class($item);
    } elseif (is_null($name)) {
      $msg = "You must provide a name for non-objects";
      throw new Exception($msg);
    }
    $name = strtolower($name);
    self::$_register[$name] = $item;
  }

  public static function &get($name) {
    $name = strtolower($name);
    if (array_key_exists($name, self::$_register)) {
      return self::$_register[$name];
    } else {
      $msg = "'$name' is not registered.";
      throw new Exception($msg);
    }
  }
  
  public static function exists($name) {
    $name = strtolower($name);
    if (array_key_exists($name, self::$_register)) {
      return true;
    } else {
      return false;
    }
  }
}

$db = new DB();
Registry::add($db);

// Later on
if (Registry::exists('DB')) {
  $db = Registry::get('DB');
} else {
  die('We lost our Database connection somewhere. Bear with us.');
}
```
