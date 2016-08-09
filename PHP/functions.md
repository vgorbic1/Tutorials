## Functions

#### Handling variable-length argument lists. (Similar to overloading in Java)
PHP provides three built-in functions to handle variable-length argument lists:
- ```func_num_args()``` -  Returns the number of arguments passed to the function.
- ```func_get_arg()``` - Returns an item from the argument list.
- ```func_get_args()``` - Returns an array comprising a function's argument list.

```php
function hello() {
  if (Func_num_args() > 0) {
    $arg = func_get_arg(0);
    echo "Hello $arg";
  } else {
    echo "Hello World";
  }
}

hello("Reader"); // displays "Hello Reader"
hello(); // displays "Hello World"
```
**Variadics (PHP 5.6)**

Variadics allow you to explicitly denote a function as accepting a variable length argument list. The variadic argument must be the last argument in the argument list.

Syntax:
```
... $args
```
The same function from abouve will look like this:
```php
function f($arg1, ...$args) {
  $count = strlen($arg1);
  
  foreach ($args as $arg) {
    $count += strlen($arg);
  }
  
  return $count;
}
```
**Splat or Argument Unpacking (PHP 5.6)**
Argument unpacking works the opposite way variadics does, allowing you to unpack an array-like data structure into an argument list when calling a function or method.
```php
$args = ["World", "Universe", "Hello World"];
echo str_replace(...$args); // Returns "Hello Universe";
```
