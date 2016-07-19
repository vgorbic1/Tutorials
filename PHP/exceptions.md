## Exceptions

Procedural code creates errors, while OOP has exceptions. Handle exceptions using "try" and "catch" blocks.

To throw an exception:
```php
throw new Exception('error message');
```
To catch this exception:
```php
catch (Exception $e) { 
    …
}
```
Any code within a "try" block after an exception is thrown will never run. If no exception ever occurs, the code in the "catch" block will never be executed:
```php
try {
    // Do something
} catch (Exception $e) {
    echo $e->getMessage();
}
```

#### Exception class methods:
- getCode() returns the numeric exception code received, if any.
- getMessage() returns the string exception message received, if any.
- getFile() returns the name of the file where the exception occurred.
- getLine() returns the line number from which the exception was thrown.
- getTrace() returns an array of information, like the file name, line number, and so on.
- getTraceAsString() returns the same information as getTrace() but as a string.
- __toString() returns all of the preceding information as a string.

#### Extending the Exception class:
```php
class MyException extends Exception {
    …
}
```
Only the Exception constructor and ```__toString()``` methods can be overridden, because the others are all defined as final!

To throw this custom exception use:
```php
throw new MyException('error message');
```
Now, write "try" and "catch" exception blocks:
```php
try {
    // Some code
    throw new MyException1('error message');
    // Some more code
    throw new MyException2('error message');
} catch (MyException1 $e) {
} catch (MyException2 $e) {
}
```
If your extended Exception class has its own constructor, it should also call the Exception constructor using:
```php
parent::__construct();
```
