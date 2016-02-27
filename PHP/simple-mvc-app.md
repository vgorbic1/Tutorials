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
Create `connection.php` to provide database connection credentials. It is going to be a singleton class. This allows us to return an instance of the connection and always the same as we only need one to execute all our queries. As the class is a singleton, we make `__construct()` and `__clone()` private so that no one can call `new Db()`. It has an `$instance` variable that retains the connection object (PDO here). In the end, we have access to our connection object through `Db::getInstance()`.
```php
<?php
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












[SOURCE](http://requiremind.com/a-most-simple-php-mvc-beginners-tutorial/)

Application Github [repo](https://github.com/Raindal/php_mvc)
