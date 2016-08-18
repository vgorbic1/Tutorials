## Errors and Error Management
By default, PHP reports any errors it encounters to the script’s output. Unless you happen to be in a debugging environment, you will probably not want to take advantage of this feature.

#### Error Types
- Compile-time errors - Errors detected by the parser while it is compiling a script. Cannot be trapped from within the script itself.
- Fatal errors - Errors that halt the execution of a script. Cannot be trapped.
- Recoverable errors - Errors that represent significant failures, but can still be handled in a safe way.
- Warnings - Recoverable errors that indicate a run-time fault. Do not halt the execution of the script.
- Notices - Indicate that an error condition occurred, but is not necessarily significant. Do not halt the execution of the script.
- Informational - Indicates a condition that you should check in your code, because it may indicate functionality that will change or be
removed in a future version.

Several configuration directives in the php.ini file allow you to fine-tune how—and which—errors are reported. The most important ones are ```error_reporting```, ```display_errors```, and ```log_errors```.

```error_reporting``` directive determines which errors are reported by PHP. A series of built-in constants allow you to prevent PHP from reporting errors beneath a certain pre-defined level. For example, the following allows for the reporting of all errors, except notices:
```
error_reporting=E_ALL & ~E_NOTICE
```
Error reporting can also be changed dynamically from within a script by calling the ```error_reporting()``` function.

The ```display_errors``` and ```log_errors``` directives can be used to determine how errors are reported. If ```display_errors``` is turned on, errors are added to the script’s output; generally speaking, this is not desirable in a production
environment, as everyone will be able to see your scripts’ errors. Under those circumstances, you will instead want to turn on ```log_errors```, which causes errors to be written to your web server’s error log. You can change the file used for logging with the ```error_log``` directive, which takes the name of a file. Make sure the file is writeable by your script.

#### Handling Errors
Your scripts should always be able to recover from a trappable error, even if it’s just to advise the user and to notify support staff that an error occurred. This way, your script won’t simply capitulate when something unexpected occurs, resulting in better communication with your users and the possible avoidance of some major problems.

Your scripts can declare a catch-all function that is called by PHP when an error condition occurs by calling the ```set_error_handler()``` function:
```php
$oldErrorHandler = '';
function myErrorHandler($no, $str, $file, $line, $context) {
  global $oldErrorHandler;
  logToFile("Error $str in $file at line $line");
  // Call the old error handler
  if ($oldErrorHandler) {
    $oldErrorHandler($no, $str, $file, $line, $context);
  }
}

$oldErrorHandler = set_error_handler('myErrorHandler');
```
