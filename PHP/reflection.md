##Reflection
With the introduction of PHP’s new object model in PHP 5.0 also came the Reflection API, a collection of functions and objects that allows you to examine the contents of a script’s code, such as functions and objects, at runtime. Reflection can be very handy in a number of circumstances. For example, it can be used to generate simple documentation, or to determine whether certain functionality is available to a script, and so on.
```php
<?php
/**
  * Say Hello
  *
  * @param string $to
*/
function hello($to = "World") {
  echo "Hello $to";
}
$funcs = get_defined_functions();
?>

<h1>Documentation</h1>

<?php
/**
  * Do Foo
  *
  * @param string $bar Some Bar
  * @param array $baz An Array of Baz
  */
function foo($bar, $baz = array()) { }
$funcs = get_defined_functions();
foreach ($funcs['user'] as $func) {
  try {
    $func = new ReflectionFunction($func);
  } catch (ReflectionException $e) {
  // ...
}
$prototype = $func->name . ' ( ';
$args = array();
foreach ($func->getParameters() as $param) {
  $arg = "";
  if ($param->isPassedByReference()) {
    $arg = '&';
  }
  if ($param->isOptional()) {
    $arg = '[' . $param->getName() . ' = '. $param->getDefaultValue() . ']';
  } else {
    $arg = $param->getName();
  }
  $args[] = $arg;
}
$prototype .= implode(", ", $args) . ' )';
echo "<h2>$prototype</h2>
<p> Comment: </p>
<pre>" . $func->getDocComment() . "</pre>
<p>
  File: " . $func->getFileName() . "<br />
  Lines: " . $func->getStartLine() . " - " . $func->getEndLine() . "
</p>";
}
```
with classes
```php
/**
  * Greeting Class
  *
  * Extends a greeting to someone/thing
  */
  
class Greeting {
  /**
    * Say Hello
    *
    * @param string $to
    */
  function hello($to = "World") {
    echo "Hello $to";
  }
}

$class = new ReflectionClass("Greeting");
?>

<h1>Documentation</h1>
<h2><?php echo $class->getName(); ?></h2>
<p>Comment:</p>
<pre><?php echo $class->getDocComment(); ?></pre>
<p>
  File: <?php echo $class->getFileName(); ?><br />
  Lines: <?php echo $class->getStartLine(); ?> - <?php echo $class->getEndLine(); ?>
</p>

<?php
foreach ($class->getMethods() as $method) {
  $prototype = $method->name . ' ( ';
  $args = array();
  foreach ($method->getParameters() as $param) {
    $arg = "";
    if ($param->isPassedByReference()) {
      $arg = '&';
    }
    if ($param->isOptional()) {
      $arg = '[' . $param->getName() . ' = ' . $param->getDefaultValue() . ']';
    } else {
      $arg = $param->getName();
    }
    $args[] = $arg;
  }
  $prototype .= implode(", ", $args) . ' )';
  echo "<h3>$prototype</h3>";
  echo "<p>Comment:</p>
  <pre>" . $method->getDocComment() . "</pre>
  <p>
    File: " . $method->getFileName() . "<br />
    Lines: " . $method->getStartLine() . " - " . $method->getEndLine() . "
  </p>";
}
```
The Reflection API is extremely powerful, since it allows you to inspect userdefined and internal functions, classes and objects, and extensions. In addition to inspecting them, you can also call functions and methods directly through the API.
