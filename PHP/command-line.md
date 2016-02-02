## Command-Line Interface
Use PHP for shell scripting (command-line programming). On Windows – via DOS prompt (console or command window) on Unix and Mac OS X – via Terminal.
To see the current PHP version:
```
php –v
```
CLI uses a different configuration file (php.ini) than Web PHP, with different modules installed. Hence, PHP CLI may run differently than you are used to!

Test small sections of code right in CLI:
```
php –r 'echo "Hello, World!";' // Unix version
php –r "echo 'Hello, World!';" // Windows version
```
To invoke interactive shell on Unix use –a flag:
```
php –a
```
If you have interactive mode instead (Windows), that means you do not have interactive shell and readline installed. Use this mode to print entire script within <?php and ?> tags, and press Ctrl-Z to execute the code.

Creating Command-Line Script
To create a command-line script, do not use any HTML; the file may have .php extension, but it is not necessary; the very first line of the script should start with shebang (Unix and Mac OS X. Windows will ignore it):
#!/usr/bin/php
<?php … code …?>

To run command-line script:
If your PHP is in your PATH and you are in the same directory as the script:
php –f scriptname.php
If you have to write PHP path manually and you are in the same directory as the script:
/usr/bin/php scriptname.php    // for Unix or Mac
C:\php\php.exe scriptname.php    // for Windows 
If you need to write a path to the file:
php /path/to/scriptname.php
Or just run the file as an application:
scriptname.php    // Windows
(You may need to tell Windows what application to use for the script. Choose PHP as default program that ALWAYS will open .php scripts)
./scriptname.php    // Unix and Mac
(Make sure the file is executable first: chmod +x scriptname.php)

Using Command-Line Arguments
Access command-line arguments in PHP script:
$_SERVER['argv']   // stores every argument provided
$_SERVER['argc']   // stores number of items in $argv. 
(The name of the script is the first argument: $_SERVER['argv'][0])

Php Build Server
PHP has a build in server, but not production level. It allows to test PHP scripts.
If your PHP has flags –S and –t, then the built-in server is supported. (Check it with php –h )
By default the server will use the directory in which the server was started as the Web root directory, so you should navigate there first. Server will use PHP CLI configuration.
Start the server:
php –S localhost:8000
(Use port 8000 or 8080 to prevent conflicts if your 80 is taken by Apache)
Go to a browser and print URL:
localhost:8000/php.info
Stop the server:
Use Ctrl-C for command-line.

