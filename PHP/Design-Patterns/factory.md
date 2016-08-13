##Factory
The Factory pattern is used in scenarios where you have a generic class (the factory) that provides the facilities for creating instances of one or more separate “specialized” classes that handle the same task in different ways.

A good situation for which the Factory pattern provides an excellent solution is the management of multiple storage mechanisms for a given task. For example, consider configuration storage, which could be provided by data stores like INI files, databases or XML files interchangeably. The API that each of these classes provides is the same (ideally, implemented using an interface), but the underlying implementation changes. The Factory pattern provides us with an easy way to return a different data store class depending on either the
user’s preference, or a set of environmental factors:
```php
class Configuration {
  const STORE_INI = 1;
  const STORE_DB = 2;
  const STORE_XML = 3;
  
  public static function getStore($type = self::STORE_XML) {
    switch ($type) {
      case self::STORE_INI:
        return new Configuration_Ini();
      case self::STORE_DB:
        return new Configuration_DB();
      case self::STORE_XML:
        return new Configuration_XML();
      default:
        throw new Exception("Unknown Datastore Specified.");
    }
  }
}


class Configuration_Ini {
// ...
}


class Configuration_DB {
// ...
}


class Configuration_XML {
// ...
}


$config = Configuration::getStore(Configuration::STORE_XML);
```
