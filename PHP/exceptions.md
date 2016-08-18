## Exceptions

Procedural code creates errors, while OOP has exceptions. Handle exceptions using "try" and "catch" blocks.

There are several key differences between “regular” PHP errors and exceptions:
- Exceptions are objects, created (or “thrown”) when an error occurs.
- Exceptions can be handled at different points in a script’s execution, and different types of exceptions can be handled by separate portions of a script’s code.
- All unhandled exceptions are fatal.
- Exceptions can be thrown from the __construct method on failure.
- Exceptions change the flow of the application.

####Basic Exception Class
Almost all of the properties of an ```\Exception``` are automatically filled in by the interpreter. You only need to provide a
message and a code, and all the remaining information will be taken care of.
```php
class Exception {
// The error message associated with this exception
protected $message = 'Unknown Exception';
// The error code associated with this exception
protected $code = 0;
// The pathname of the file where the exception occurred
protected $file;
// The line of the file where the exception occurred
protected $line;
// Constructor
function __construct ($message = null, $code = 0);
// Returns the message
final function getMessage();
// Returns the error code
final function getCode();
// Returns the file name
final function getFile();
// Returns the file line
final function getLine();
// Returns an execution backtrace as an array
final function getTrace();
// Returns a backtrace as a string
final function getTraceAsString();
// Returns a string representation of the exception
function __toString();
}
```
Since ```\Exception``` is a normal (if built-in) class, you can extend it and effectively create your own exceptions, thus providing your error handlers with any additional information that your application requires.

#### Throwing Exceptions
Exceptions are usually created and thrown when an error occurs by using the ```throw``` construct. Although it is common practice to do so, you don’t need to create the Exception object directly in the throw expression. You may instantiate the exception object at any time and assign it to a variable to throw later.
```php
if ($error) {
  throw new Exception("This is my error");
}
```
Exceptions then “bubble up” until they are either handled by the script or cause a fatal exception. Any exception that is thrown inside the ```try{}``` block is going to be caught and passed on to the code inside the ```catch{}``` block, where it can be handled as you see fit:
```php
try {
  if ($error) {
    throw new \Exception("This is my error");
  }
} catch (\Exception $e) {
  // Handle exception
}
```
One of the best features of exceptions is the fact that you can decide which kind of exception to trap.

Since you are free to extend the base \Exception class, this means that different nested try..catch blocks can be used to trap and deal with different types of errors.
```php
namespace myCode;
class Exception extends \Exception { }

try {
  try {
    try {
      new PDO("mysql:dbname=zce");
      throw new myException("An unknown error occurred.");
    } catch (\PDOException $e) {
      echo $e->getMessage();
    }
  } catch(\myCode\Exception $e) {
    echo $e->getMessage();
  }
} catch (\Exception $e) {
  echo $e->getMessage();
}
```
In this example, we have three nested try... catch blocks; the innermost
one will only catch \PDOException objects, while the next will catch the
custom \myCode\Exception objects, and the outermost will catch any other
exceptions that we might have missed. Rather than nesting the try...catch
blocks like we did above, you can also chain just the catch blocks:
```php
try {
  new PDO("mysql:dbname=zce");
  throw new myException("An unknown error occurred.");
} catch (\PDOException $e) {
  echo $e->getMessage();
} catch (\myCode\Exception $e) {
  echo $e->getMessage();
} catch (\Exception $e) {
  echo $e->getMessage();
}
```
Once an exception has been caught, execution of the script will follow from directly after the last catch block.

PHP allows us to define a “catch-all” function that is automatically called whenever an exception is not handled.
This function is set up by calling ```set_exception_handler()```:
```php
function handleUncaughtException($e) {
  echo $e->getMessage();
}

set_exception_handler("handleUncaughtException");
throw new Exception("You caught me!");
echo "This is never displayed";
```

#### Finally
With PHP 5.5, a finally block was added. Code within the ```finally``` block will be executed regardless of whether an exception has been thrown or not, making it useful for things like cleanup.
```php
try {
  // Try something
} catch (\Exception $exception) {
  // Handle exception
} finally {
  // Whatever happened, do this
}
```
