##Lazy Loading
We can use the require/include methods to load our classes, or we can use another method PHP gives us: the
```spl_autoload_register()``` function. This built-in function allows us to provide our own code, to use as a means
of loading a class based on the name of the class requested.
The pattern we will use to find class files will be the title-case class name with a directory separator between
each word and .php at the end. So if we need to load the ```Framework\Database\Driver\Mysql``` class, we will look
for the file ```framework/database/driver/mysql.php``` (assuming our framework folder is in the PHP include path):
```php
function autoload($class) {
  $paths = explode(PATH_SEPARATOR, get_include_path());
  $flags = PREG_SPLIT_NO_EMPTY | PREG_SPLIT_DELIM_CAPTURE;
  $file = strtolower(str_replace("\\", DIRECTORY_SEPARATOR, trim($class, "\\"))).".php";
  foreach ($paths as $path) {
    $combined = $path.DIRECTORY_SEPARATOR.$file;
    if (file_exists($combined)) {
      include($combined);
      return;
    }
  }
  throw new Exception("{$class} not found");
}

class Autoloader {
  public static function autoload($class) {
    autoload($class);
  }
}

spl_autoload_register('autoload');  // use the autoload() method to load a class file by name.
spl_autoload_register(array('autoloader', 'autoload'));  // use the Autoloader::autoload() method to load a class file by name.
// these can only be called within a class context:
// spl_autoload_register(array($this, 'autoload'));
// spl_autoload_register(__CLASS__.'::load');
```
The third and fourth calls to ```spl_autoload_register()``` tell PHP to use the ```autoload()``` method, belonging to the class in which these ```spl_autoload_register()``` calls occur, to load a class file by name.

The ```autoload()``` function first splits the returned string of PHP’s ```get_include_path()``` function into separate directories. It then constructs the target file name by splitting the requested class name on the second, third, fourth, and so on, uppercase letters and joining the words together using the ```PATH_SEPARATOR``` constant. If it finds the target file within any of the ```$paths``` directories, it will include the file and end function execution with a return statement. If the file is not found by the end of the loop, through ```$paths```, an Exception will be thrown. If no exception is thrown, you can assume that a file matching the class name was found (in one of the directories in the include path) and was included successfully.
