## CAV Application
CAV (Controller Action View) "blures" the line between the Model and Controller in standard MVC approach.
The frameworks needs a single point of entry - `index.php`. This is where all access to the site must be controlled from. To ensure that a single point of entry is maintained, htaccess can be utilized. The `.htaccess` file itself looks like this:
```
RewriteEngine on

RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d

RewriteRule ^(.*)$ index.php?rt=$1 [L,QSA]
```
The `.htaccess` file will permit access to the site via urls such as `http://www.example.com/news/show`. If you do not have mod_rewrite available, the entry to the site will be the same, except that the URL will contain the values needed such as:
`http://www.example.com/index.php?rt=news/show`.

#### Site Structure
```
 html
      -application
      -controller
      -includes
      -model
      -views
 .htaccess
 index.php
 ```

#### index.php
The `index.ph`p file is our single point of access. As such, it provides the ideal space for declaring variables and site wide configurations. It is in this file that we will also call a helper file to initialize a few values. This file will be called `init.php` and it will be placed in `includes` directory as shown in the direcory structure. The index.php file therefore, will begin like this:
```php
<?php # index.php

 /*** error reporting on ***/
 error_reporting(E_ALL);

 /*** define the site path constant ***/
 $site_path = realpath(dirname(__FILE__));
 define ('__SITE_PATH', $site_path);

 /*** include the init.php file ***/
 include 'includes/init.php';

?>
```
With this file in place, and the .htaccess file we can begin to build the registry.

In this MVC framework, the registry object is passed to other objects and contains site wide variables without the use globals. To create a new registry object, we use the `init.php` file in the includes directory. To create new object we need to include the registry class definition file. During the building of the MVC framework we will be including the application class files directly. Any PHP class definition files which are used by the model will be autoloaded as they can become quite cumbersome with larger applications. After the application includes, the `__autoload` function will immediately follow to load class definition when the `new` keyword is used. The class definitions will be stored in a directory called model. The `includes/init.php` file should now look like this:
```php
<?php # includes/init.php
 
 /*** include the controller class ***/
 include __SITE_PATH . '/application/' . 'controller_base.class.php';

 /*** include the registry class ***/
 include __SITE_PATH . '/application/' . 'registry.class.php';

 /*** include the router class ***/
 include __SITE_PATH . '/application/' . 'router.class.php';

 /*** include the template class ***/
 include __SITE_PATH . '/application/' . 'template.class.php';

 /*** auto load model classes ***/
    function __autoload($class_name) {
    $filename = strtolower($class_name) . '.class.php';
    $file = __SITE_PATH . '/model/' . $filename;

    if (file_exists($file) == false)
    {
        return false;
    }
  include ($file);
}

 /*** a new registry object ***/
 $registry = new registry;

?>
```
The autoload function uses a naming convention for the class definition files to be included. They must all follow the convention of ending in .class.php and the class name must be that of the .class.php file name. So that to create a new "news" object the class definition file name must be news.class.php and the class must be named "news".

Create blank `<?php  ?>` files and put them in application directory:
* controller_base.class.php
* registry.class.php
* router.class.php
* template.class.php

#### The Registry
The registry is an object where site wide variables can be stored without the use of globals. By passing the registry object to the controllers that need them, we avoid pollution of the global namespace and render our variables safe. We need to be able to set registry variables and to get them. The php magic functions __set() and __get() are ideal for this purpose. 
```php
<?php # application/registry.class.php
Class Registry {

 /*
 * @the vars array
 * @access private
 */
 private $vars = array();

 /**
 * @set undefined vars
 * @param string $index
 * @param mixed $value
 * @return void
 */
 public function __set($index, $value)
 {
    $this->vars[$index] = $value;
 }

 /**
 * @get variables
 * @param mixed $index
 * @return mixed
 */
 public function __get($index)
 {
    return $this->vars[$index];
 }

}
?>
```
With the registry in place, our system is working. It does not do anything or display anything, but we have a functional system. The `__set()` and `__get()` magic function now allow us to set variables within the registry and store them there.

#### The Model
The model is where business logic is stored. Business logic is loosely defined as database connections or connections to data sources, and provides the data to the controller. Our database connection is a simple singleton and resides in the classes directory and can be called statically from the controller and set in the registry. Add this code to the `init.php` file we created earlier:
```php
<?php
 /*** create the database registry object ***/
 $registry->db = db::getInstance();
?>
```
Like all registry members, the database is now globally availabe to our scripts. As the class is a singleton we always get the same instance back.

#### The Router
The router class is responsible for loading up the correct controller. It does nothing else. The value of the controller comes from the URL. The url will look a like this:
```
http://www.example.com/index.php?rt=news
```
Or if you have htaccess amd mod_rewrite working like this:
```
http://www.example.com/news
```
To begin the router class a few things need to be set. Now add this code to the `router.class.php` file in the application directory:
```php
<?php # application/router.class.php

class router {
 /*
 * @the registry
 */
 private $registry;

 /*
 * @the controller path
 */
 private $path;
 private $args = array();
 public $file;
 public $controller;
 public $action;

 function __construct($registry) {
        $this->registry = $registry;
 }
```
We can load the router into the registry also. Add this code to the `index.php` file:
```php
/*** load the router ***/
$registry->router = new router($registry);
```
Add a method to set the controller directory path. Add this block of code to the `router.class.php` file:
```php
<?php
 /**
 * @set controller directory path
 * @param string $path
 * @return void
 */
 function setPath($path) {

   /*** check if path is a directory ***/
   if (is_dir($path) == false)
   {
     throw new Exception ('Invalid controller path: `' . $path . '`');
   }
   /*** set the path ***/
   $this->path = $path;
}
```
And to set the controller path in the registry is a simple matter of adding this line to the `index.php` file:
```php
/*** set the path to the controllers directory ***/
 $router->setPath (__SITE_PATH . 'controller');
```
With the controller path set we can load the controller. We will create a method called `loader()` to get the controller and load it. This method will call a `getController()` method that will decide which controller to load. If a controller is not found then it will default back to the index. The loader method looks like this:
```php
<?php

 /**
 * @load the controller
 * @access public
 * @return void
 */
 public function loader()
 {
        /*** check the route ***/
        $this->getController();

        /*** if the file is not there diaf ***/
        if (is_readable($this->file) == false)
        {
                echo $this->file;
                die ('404 Not Found');
        }

        /*** include the controller ***/
        include $this->file;

        /*** a new controller class instance ***/
        $class = $this->controller . 'Controller_';
        $controller = new $class($this->registry);

        /*** check if the action is callable ***/
        if (is_callable(array($controller, $this->action)) == false)
        {
                $action = 'index';
        }
        else
        {
                $action = $this->action;
        }
        /*** run the action ***/
        $controller->$action();
 }
 ```
