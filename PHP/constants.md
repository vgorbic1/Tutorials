## Constants
Constants values remain the same once defined and cannot be changed.
```PHP
define('SITE_NAME', 'Product Store');
```
Refer to the constant:
```PHP
echo SITE_NAME;
```
Define a document root depending on the platform:
```PHP
switch($plaform) // Must be 'win', 'mac', or 'lin' 
{ case 'win': define('DOC_ROOT', 'C:/xampp/htdocs'); break;
  case 'mac': define('DOC_ROOT', '/Applications/XAMPP/htdocs'); break;
  case 'lin': define('DOC_ROOT', '/opt/lamp/htdocs'); break; }
```

#### Magic (Predefined) Constants
These are internal constants used by PHP engine:

```__LINE__``` The current line number of the file.

```__FILE__``` The full absolute path and filename of the current file. Symbolic links are resolved. If this is used inside an include, the name of the included file is returned. Example: ```dirname(__FILE__)``` gives the full path to the directory where the file sits.

```__DIR__``` The directory of the current file. If used inside an include, the directory of the included file is returned. This is equivalent to ```dirname(__FILE__)```. This directory name does not have a trailing slash unless it is the root directory. 

```__FUNCTION__``` Returns the function name as it was declared in a case-sensitive string.

```__CLASS__``` Returns the class name as it was declared. The class name includes the namespace it was declared in (e.g. Foo\Bar). Note that as of PHP 5.4 ```__CLASS__``` works also in traits. When used in a trait method, ```__CLASS__``` is the name of the class the trait is used in.

```__TRAIT__``` Returns the trait name. The trait name includes the namespace it was declared in (e.g. Foo\Bar).

```__METHOD__``` Returns the class method name as it was declared.

```__NAMESPACE__``` Returns the name of the current namespace as defined at compile time.

These magic constants help with debugging:
```PHP
echo "This is line " . __LINE__ . " of file " . __FILE__;
```
