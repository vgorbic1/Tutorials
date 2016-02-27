## Simple MVC Application
MVC is a design pattern that suggests you organize your code in a way concerns are properly separated, and yet interact with each other in a certain fashion. **Models** fetch and mold data which is in turn sent to the **View** and therefore displayed. The **Controller** is managing the process.

#### Database
Create a MySQL database `php_mvc` that contains a table `posts` with 3 columns `id`, `author` and `content`.
```sql
CREATE DATABASE php_mvc;

USE php_mvc;

CREATE TABLE posts (id INT NOT NULL AUTO_INCREMENT, author VARCHAR(255), content TEXT, PRIMARY KEY (id));
```

#### Utility Files
Create `index.php`, which is going to make sure we have something to query the database any time later in the execution.
As this is a pretty specific thing, we put it in a specific file that we’re going to require in our index.php:
```php
<?php # index.php
  require_once('connection.php');
?>
```
Create `connection.php` to provide database connection credentials. It is going to be a singleton class. This allows us to return an instance of the connection and always the same as we only need one to execute all our queries. As the class is a singleton, we make `__construct()` and `__clone()` private so that no one can call `new Db()`. It has an `$instance` variable that retains the connection object (PDO here). In the end, we have access to our connection object through `Db::getInstance()`. The singletons are not the only way to handle database connection, it’s just been a common way for years.
```php
<?php # connection.php
  class Db {
    private static $instance = NULL;
    private function __construct() {}
    private function __clone() {}
    
    public static function getInstance() {
      if (!isset(self::$instance)) {
        $pdo_options[PDO::ATTR_ERRMODE] = PDO::ERRMODE_EXCEPTION;
        self::$instance = new PDO('mysql:host=localhost;dbname=php_mvc', 'root', '', $pdo_options);
      }
      return self::$instance;
    }
  }
?>
```
Enhance the `index.php` file. This file is going to receive all the requests. This means that every link would have to point to `/?x=y` or `/index.php?x=y`. The `if` statement checks whether we have the parameters controller and action set and store them in variables. If we do not have such parameters we just make pages the default controller and home the default action. Every request when hiting our index file is going to be routed to a controller (just a file defining a class) and an action in that controller (just a method in that class).
```php
<?php
  require_once('connection.php');

  if (isset($_GET['controller']) && isset($_GET['action'])) {
    $controller = $_GET['controller'];
    $action     = $_GET['action'];
  } else {
    $controller = 'pages';
    $action     = 'home';
  }

  require_once('views/layout.php');
?>
```
Finally we require the only part of our application that does not change: the layout. Let’s create this 'layout.php' file and put it to `views` directory. Note, `php_mvc_blog` is the root of the whole application. In the middle we require another file: `routes.php`.
```php
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <header>
      <a href='/php_mvc_blog'>Home</a>
    </header>

    <?php require_once('routes.php'); ?>

    <footer>
      Copyright
    </footer>
  </body>
</html>
```
The only part we still need is the main area of our page. We can determine what view we need to put there depending on our previously set `$controller` and `$action` variables. The `routes.php` file is going to take care of that. This file is not in the views folder but at the root of our application.
```php

```









[SOURCE](http://requiremind.com/a-most-simple-php-mvc-beginners-tutorial/)

Application Github [repo](https://github.com/Raindal/php_mvc)
