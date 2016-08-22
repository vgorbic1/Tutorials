##Lazy Loading
We can use the require/include methods to load our classes, or we can use another method PHP gives us: the
```spl_autoload_register()``` function. This built-in function allows us to provide our own code, to use as a means
of loading a class based on the name of the class requested.
```php
function autoload($class)
{
$paths = explode(PATH_SEPARATOR, get_include_path());
$flags = PREG_SPLIT_NO_EMPTY | PREG_SPLIT_DELIM_CAPTURE;
$file = strtolower(str_replace("\\", DIRECTORY_SEPARATOR, trim($class, "\\"))).".php";
foreach ($paths as $path)
{
$combined = $path.DIRECTORY_SEPARATOR.$file;
if (file_exists($combined))
{
include($combined);
return;
}
}
throw new Exception("{$class} not found");
}
class Autoloader
{
public static function autoload($class)
