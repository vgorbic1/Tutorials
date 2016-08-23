##Coding Standards
WordPress maintains a set of coding standards for all core code. View the offi cial WordPress coding standards at http://codex.wordpress.org/WordPress_Coding_Standards.

####Document Code
Commenting your
Plugin’s source code is a quick and easy way to document exactly how your plugin works. Nearly all functions in WordPress core contain inline documentation in PHPDoc form. PHPDoc is a standardized method of describing a function’s usage in PHP comment form. These comments are also used by more visual tools such as PHPDocumentor and PHPXref.
```php
/**
* Short description
*
* Longer more detailed description
*
* @param type $varname1 Description
* @param type $varname2 Description
* @return type Description
*/
function boj_super_function( $varname1, $varname2 ) {
  //do function stuff
}
```

####Naming Variables, Functions, and Files
Variable and function names should always be written in lowercase. Words should also be separated using underscores:
```php
function boj_myplugin_function_name( $boj_myplugin_variable ) {
  //do something
}
```
Files should also be named using only lowercase letters; however, fi lenames should use hyphens to separate words and not underscores:
```
boj-plugin-name.php
```

####Single and Double Quotes
In WordPress it’s recommended to use single quotes whenever possible. One of the benefi ts of using single quotes is you rarely need
to escape HTML quotes in a string:
```php
echo '<a href="http://example.com/">Visit Example.com</a>';
```

####SQL Statements
SQL statements can be broke into multiple lines if the complexity of the statement warrants it. Even though SQL is not case - sensitive, it’s good practice to capitalize the SQL commands in the statement:
```sql
SELECT username FROM table1 WHERE status = 'active'
```
