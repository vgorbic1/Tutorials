## Registry
By taking the Singleton pattern a little further, we can implement the Registry pattern. This allows us to use any object as a Singleton without it being written specifically that way.

Think of it like a team manager that brings players off the playing field and sends new ones in as required. We use Registry classes to manage a finite amount of class instances, so that we don’t need to keep on reinstantiating classes that the Registry already
contains instances of.

![registry](https://cloud.githubusercontent.com/assets/13823751/17859983/52fbd8aa-6851-11e6-80ac-2ab98f5bd57f.jpg)

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
