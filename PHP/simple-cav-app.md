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
The `getController` method that the `loader()` method calls does the work. By taking the route variables from the url via `$_GET['rt']` it is able to check if a contoller was loaded, and if not default to index. It also checks if an action was loaded. An action is a method within the specified controller. If no action has been declared, it defaults to index. Add the getController method to the `router.class.php` file.
```php
<?php
 /**
 * @get the controller
 * @access private
 * @return void
 */
private function getController() {

        /*** get the route from the url ***/
        $route = (empty($_GET['rt'])) ? '' : $_GET['rt'];

        if (empty($route))
        {
                $route = 'index';
        }
        else
        {
                /*** get the parts of the route ***/
                $parts = explode('/', $route);
                $this->controller = $parts[0];
                if(isset( $parts[1]))
                {
                        $this->action = $parts[1];
                }
        }

        if (empty($this->controller))
        {
                $this->controller = 'index';
        }

        /*** Get action ***/
        if (empty($this->action))
        {
                $this->action = 'index';
        }

        /*** set the file path ***/
        $this->file = $this->path .'/'. $this->controller . '.php';
}
?>
```

#### The Controller
The base controller is a simple abstract class that defines the structure of all controllers. By including the registry here, the registry is available to all class that extend from the base controller. An `index()` method has also been included in the base controller which means all controller classes that extend from it must have an `index()` method themselves. Add this code to the `controller.class.php` file in the application directory:
```php
<?php # application/controller.class.php

Abstract Class baseController {

/*
 * @registry object
 */
protected $registry;

function __construct($registry) {
        $this->registry = $registry;
}

/**
 * @all controllers must contain an index method
 */
abstract function index();
}

?>
```
create an index controller and a blog controller. The index controller is the sytem default and it is from here that the first page is loaded. The blog controller is for an imaginary blog module. When the blog module is specified in the URL
`http://www.example.com/blog`
then the index method in the blog controller is called. A view method will also be created in the blog controller and when specified in the URL `http://www.example.com/blog/view`
then the view method in the blog controller will be loaded. First lets see the index controller. This will reside in the controller directory:
```php
<?php # controller/indexcontroller.php
class indexController extends baseController {

  public function index() {
    /*** set a template variable ***/
        $this->registry->template->welcome = 'Welcome to PHPRO MVC';

    /*** load the index template ***/
        $this->registry->template->show('index');
  }

}
?>
```
The indexController class above shows that the indexController extends the baseController class, thereby making the registry available to it without the need for global variables. The indexController class also contains the mandatory `index()` method that ll controllers must have. Within its `index()` method a variable named "welcome" is set in the registry. This variable is available to the template when it is loaded via the `template->show()` method.

The blogController class follows the same format but has has one small addition, a `view(`) method. The `view()` method is an example of how a method other than the `index()` method may be called. The view method is loaded via the URL 
`http://www.example.com/blog/view`:
```php
<?php

Class blogController Extends baseController {

  public function index() {
        $this->registry->template->blog_heading = 'This is the blog Index';
        $this->registry->template->show('blog_index');
  }

  public function view(){
        /*** should not have to call this here.... FIX ME ***/
        $this->registry->template->blog_heading = 'This is the blog heading';
        $this->registry->template->blog_content = 'This is the blog content';
        $this->registry->template->show('blog_view');
  }

 }
?>
```
#### The View
The View contains code that relates to presentation and presentation logic such as templating and caching. In the controller above we saw the `show()` method. This is the method that calls the view. The major component in this app is the template class. The `template.class.php` file contains the class definition. Like the other classes, it has the registry available to it and also contains a `__set()` method in which template variables may be set and stored.

The show method is the engine room of the view. This is the method that loads up the template itself, and makes the template variables available. Some larger MVC's will implement a template language that adds a further layer of abstraction from PHP. Added layers mean added overhead. Here we stick with the speed of PHP within the template, yet all the logic stays outside. This makes it easy for HTML monkies to create websites without any need to learn PHP or a template language. The `template.class.php` file looks like this:
```php
<?php

Class Template {

/*
 * @the registry
 * @access private
 */
private $registry;

/*
 * @Variables array
 * @access private
 */
private $vars = array();

/**
 * @constructor
 * @access public
 * @return void
 */
function __construct($registry) {
   $this->registry = $registry;
}

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

 function show($name) {
        $path = __SITE_PATH . '/views' . '/' . $name . '.php';

        if (file_exists($path) == false)
        {
                throw new Exception('Template not found in '. $path);
                return false;
        }

        // Load variables
        foreach ($this->vars as $key => $value)
        {
                $$key = $value;
        }

        include ($path);
  }
}
?>
```
#### Templates
The templates themselves are basically HTML files with a little PHP embedded. Do not let the separation Nazi's try to tell you that you need to have full seperation of HTML and PHP. Remember, PHP is an embeddable scripting language. This is the sort of task it is designed for and makes an efficient templating language. The template files belong in the `views` directory. Here is the `index.php` file:
```php
<h1><?php echo $welcome; ?></h1>
```
The blog_index.php file:
```php
<h1><?php echo $blog_heading; ?></h1>
```
And finally the blog_view.php file:
```php
<h1><?php echo $blog_heading; ?></h1>
<p><?php echo $blog_content; ?></p>
```
In the above template files note that the variable names in the templates, match the template variables created in the controller.

[SOURCE](http://www.phpro.org/tutorials/Model-View-Controller-MVC.html#) by Kevin Waterson.
