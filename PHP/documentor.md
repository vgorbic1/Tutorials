## Documentor
Use dock block syntax to create documentation comments in PHP:
```PHP
/**
 *  Some comments
 */
```
To documaent a variable definition use `@var`. Dock block does need to reference the variable name, just the type:
```PHP
/**
 * @var string
 */
```
To document a parameter for a certain function use `@param`

To document a return for a certain function use `@return`

Full usage can be found [here](http://phpdoc.org/docs/latest/index.html)

#### To download phpDocumentor
In command line:
```
pear channel-discover pear.phpdoc.org
```
#### To install phpDocumentor
In command line:
```
pear install phpdoc/phpDocumentor-alpha
```
#### To create PHP Document on your code
Go to the directory with your code. In command line:
```
phpdoc –f HelloWorld.php –t docs
```
#### To create documentation of entire project
```
phpdoc –d HelloWorld.php –t docs
```
The target `(-t)` directory for the documentation is "docs" which is located in the same directory as the code is.
