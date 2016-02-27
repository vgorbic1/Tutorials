## Simple MVC Application
MVC is a design pattern that suggests you organize your code in a way concerns are properly separated, and yet interact with each other in a certain fashion. **Models** fetch and mold data which is in turn sent to the **View** and therefore displayed. The **Controller** is managing the process.

#### Database
Create a MySQL database `php_mvc` that contains a table `posts` with 3 columns `id`, `author` and `content`.
```sql
CREATE DATABASE php_mvc;

USE php_mvc;

CREATE TABLE posts (id INT NOT NULL AUTO_INCREMENT, author VARCHAR(255), content TEXT, PRIMARY KEY (id));
```
We need to have some data in the database so add some manually as we do not have a feature for this yet.
```sql
INSERT INTO posts VALUES (1, 'Jon Snow', 'The wall will Fall.');
INSERT INTO posts VALUES (2, 'Khal Drogo', 'I may be dead but I’m still the most awesome character.');
```

#### Views and Controllers
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
The only part we still need is the main area of our page. We can determine what view we need to put there depending on our previously set `$controller` and `$action` variables. The `routes.php` file is going to take care of that. This file is not in the views folder but at the root of our application. We want our `routes.php` to output the html that was requested one way or another. To fetch the right view (file containing the html we need) we have two things: a controller name and an action name. We can write a function call that will take those two arguments and call the action of the controller:
```php
<?php
  function call($controller, $action) {
    // require the file that matches the controller name
    require_once('controllers/' . $controller . '_controller.php');

    // create a new instance of the needed controller
    switch($controller) {
      case 'pages':
        $controller = new PagesController();
      break;
    }

    // call the action
    $controller->{ $action }();
  }

  // just a list of the controllers we have and their actions
  // we consider those "allowed" values
  $controllers = array('pages' => ['home', 'error']);

  // check that the requested controller and action are both allowed
  // if someone tries to access something else he will be redirected to the error action of the pages controller
  if (array_key_exists($controller, $controllers)) {
    if (in_array($action, $controllers[$controller])) {
      call($controller, $action);
    } else {
      call('pages', 'error');
    }
  } else {
    call('pages', 'error');
  }
?>
```
Let’s continue and write our first controller for the call function to find the file. This class has two public functions as expected: `home()` and `error()`. As you can see, the first one is also defining some variables. We’re doing this so we can later ouput their values in the view and not clutter our view with variables definition and other computation not related to anything visual. Separation of concerns.
```php
<?php # controllers/pages_controller.php
  class PagesController {
    public function home() {
      $first_name = 'Jon';
      $last_name  = 'Snow';
      require_once('views/pages/home.php');
    }

    public function error() {
      require_once('views/pages/error.php');
    }
  }
?>
```
To keep things simple, we usually name the view after the action name and we store it under the controller name. Let’s create both our views. Use those previously defined `$first_name` and `$last_name` where you see fit.

views/pages/home.php:
```php
<p>Hello there <?php echo $first_name . ' ' . $last_name; ?>!<p>
<p>You successfully landed on the home page. Congrats!</p>
```
views/pages/error.php
```php
<p>Oops, this is the error page.</p>
<p>Looks like something went wrong.</p>
```

#### Models
We want to be able to fetch a list of posts and display those, and same thing for one particular post. Modify the `routes.php` file to reflect that behaviour.
```php
<?php # routes.php
  function call($controller, $action) {
    require_once('controllers/' . $controller . '_controller.php');

    switch($controller) {
      case 'pages':
        $controller = new PagesController();
      break;
      case 'posts':
        // we need the model to query the database later in the controller
        require_once('models/post.php');
        $controller = new PostsController();
      break;
    }

    $controller->{ $action }();
  }

  // we're adding an entry for the new controller and its actions
  $controllers = array('pages' => ['home', 'error'],
                       'posts' => ['index', 'show']);

  if (array_key_exists($controller, $controllers)) {
    if (in_array($action, $controllers[$controller])) {
      call($controller, $action);
    } else {
      call('pages', 'error');
    }
  } else {
    call('pages', 'error');
  }
?>
```
We can create the posts controller now. The pages controller is managing static pages of our application whereas the posts controller is managing what we call a resource. The resource here is a post. A resource can usually be listed (index action), showed (show action), created, updated and destroyed. `Post::all()` and `Post::find()` refer to the model.
```php 
<?php # controllers/posts_controller.php
  class PostsController {
    public function index() {
      // we store all the posts in a variable
      $posts = Post::all();
      require_once('views/posts/index.php');
    }

    public function show() {
      // we expect a url of form ?controller=posts&action=show&id=x
      // without an id we just redirect to the error page as we need the post id to find it in the database
      if (!isset($_GET['id']))
        return call('pages', 'error');

      // we use the given id to get the right post
      $post = Post::find($_GET['id']);
      require_once('views/posts/show.php');
    }
  }
?>
```
Now we can move on to writing the model. Our model is a class with three attributes. It has a constructor so we can call `$post = new Post('Neil', 'A Most Simple PHP MVC')` if need be. Put the `post.php` file in `models` directory
```php
<?php # models/post.php
  class Post {
    // we define 3 attributes
    // they are public so that we can access them using $post->author directly
    public $id;
    public $author;
    public $content;

    public function __construct($id, $author, $content) {
      $this->id      = $id;
      $this->author  = $author;
      $this->content = $content;
    }

    public static function all() {
      $list = [];
      $db = Db::getInstance();
      $req = $db->query('SELECT * FROM posts');

      // we create a list of Post objects from the database results
      foreach($req->fetchAll() as $post) {
        $list[] = new Post($post['id'], $post['author'], $post['content']);
      }

      return $list;
    }

    public static function find($id) {
      $db = Db::getInstance();
      // we make sure $id is an integer
      $id = intval($id);
      $req = $db->prepare('SELECT * FROM posts WHERE id = :id');
      // the query was prepared, now we replace :id with our actual $id value
      $req->execute(array('id' => $id));
      $post = $req->fetch();

      return new Post($post['id'], $post['author'], $post['content']);
    }
  }
?>
```
Let’s modify our layout to add a link to the posts in the header. The `layout.php` file looks like this:
```php
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <header>
      <a href='/php_mvc_blog'>Home</a>
      <a href='?controller=posts&action=index'>Posts</a>
    </header>

    <?php require_once('routes.php'); ?>

    <footer>
      Copyright
    </footer>
  </body>
</html>
```
We have to create the views we require in the posts controller:

views/posts/index.php
```php
<p>Here is a list of all posts:</p>
<?php foreach($posts as $post) { ?>
  <p>
    <?php echo $post->author; ?>
    <a href='?controller=posts&action=show&id=<?php echo $post->id; ?>'>See content</a>
  </p>
<?php } ?>
```
views/posts/show.php
```php
<p>This is the requested post:</p>
<p><?php echo $post->author; ?></p>
<p><?php echo $post->content; ?></p>
```

Check the result!

[SOURCE](http://requiremind.com/a-most-simple-php-mvc-beginners-tutorial/)

Application Github [repo](https://github.com/Raindal/php_mvc)
