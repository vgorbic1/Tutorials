## CLASSES and OBJECTS

Declaring a class:
```php
class UserClass {
  public $firstName, $lastName;
  function getName() {
    return $this -> firstName . ' ' . $this -> lastName;
  }
}
```
"$this" refers to the current object and "->" is called object operator. It defines access to the property of the object, its method or the object itself. Use "$this" within the class to call instance variable of that class. No need to write "$" before the instance variable name, if it preceded by "->":
```php
$this -> firstName;
```
If function within a class has no visibility keyword – it is considered being public.

Creating an object:
```php
$User = new UserClass;
```
Accessing properties, methods, and objects:
```php
$User -> firstName = 'John';
```
Do not use "$" with a property name here!
```php
echo $User -> getName();
$User -> myMethod('John', 'Doe', 32);
```
Delete an object:
```php
unset($object);
```
Using constructor:
```php
class UserClass {
  public $firstName, $lastName;
  function __construct($firstName, $lastName) {
    $this -> firstName = $firstName;
    $this -> lastName = $lastName;
  }
}
```
Now simply create an instance (object):
```php
$User = new UserClass('John', 'Doe');
```
This method is preferable than just using function within the class declaration:
```php
UserClass($firstName, $lastName); 
```
Constructor cannot have return statement! Constructor can be used to connect to a database, set cookies, or establish initial values.

To provide default values to the properties; this is called a "default constructor":
```php
function __construct($firstName = 'anonymous', $lastName = 'user') { 
   … 
}
```
In PHP5 a constructor has "__construct" keyword. In PHP4 a constructor has the name of the class instead. If in PHP5 the class cannot find its constructor with a keyword, it looks for a function with the name of the class.

Using destructor:
```php
function __destruct() { 
    … destructor code … 
}
```
Destructors cannot take any arguments!

#### Using autoloads
The ```__autoload()``` function is invoked when code attempts to instantiate an object of a class that hasn't yet been defined.
```php
function __autoload($class) {
    require($class . '.php');
}
```
Now, if we call ```$obj =  new Class();``` the autoload function will automatically include Class.php script into the main script. Autoload function is defined outside of any class, but placed in a script that instantiates objects.

#### Object Cloning
When assigning a new object based on existing one, you don’t copy the old object to the new one, but create a reference to the existing one. This just creates a reference to $OldObject:
```php
$NewObject = $OldObject;
```
To create a brand new copy of an old object with its own methods and properties use clone keyword:
```php
$NewObject = clone $OldObject;
```

#### Static methods and properties
To apply a method to entire class, not an individual object, use the key word static before the function:
```php
static function enterName() { 
    … display the form … 
}
```

To call a static method outside a class use scope resolution operator: 
```php
UserClass::enterName;
```
To call a static method from another method of the same class:
```php
self::enterName();
```
To create a static property (to track a number of user for example):
```php
static $UserCount;
```
From outside the class access the property using scope resolution operator:
```php
echo UserClass::$UserCount;
```
From within the method of the same class access the property like this:
```php
self::$UserCount = 123;
```
#### Declaring Constants
Within a class use keyword const to define a constant variable:
```php
class UserClass {
  const VERSION = 1.1; 
  function dispVersion() {
    echo self::VERSION;
  }
}
```
No "$" needed before the constant name!

To access the constant directly:
```php
echo UserClass::VERSION;
```

#### VISIBILITY
- Public (default) visible from the scope of the program
- Protected – visible form the scope of the class (accessed by the object’s class methods and subclasses)
- Private – referenced by methods within the same class, but not subclasses.

As the rule use private or protected for object property or method variables. Use private if this is absolutely necessary.

#### INHERITANCE
```php
class Subscriber extends UserClass {
  public $username, $password;
  function showDetails() {
  echo $this -> firstName . ' ' . $this -> lastName . ' ' .$this -> username . ' ' . $this -> password;
 }
 ```
Now, to access the subclass:
```php
$User = new Subscriber('John', 'Doe');
$User -> username = 'jdoe';
$User -> password = 123;
echo $User -> showDetails();
```
To directly access a parent method from its subclass, use parent keyword:
```php
$object = new Child;
$object->output1();
$object->output2();
class Father {
  function output1() { … }
}
class Child extends Father {
  function output1(){ … }
  function output2(){ 
    parent::output1();
  }
}
```
You always have to create a constructor for the superclass when creating a subclass constructor, since it is not created automatically:
```php
$object = new ChocChip();
echo $object -> chewy;
echo $object -> chocolate;
class Cookie {
  public $chewy;
  function __construct() {
    $this->chewy = 'Turtle';
  }
}
class ChopChip extends Cookie {
  public $chocolate;
  function __construct() {
    parent::__construct();
    $this->chocolate = 'TURTLE';
  }
}
```
To prevent a method from being overridden by a subclass use final keyword, but it does not work for properties and classes, only functions!
```php
final public function author() {
     … 
} 
```
To check the type of certain class type use instanceof keyword:
```php
if ($obj instanceof SomeClass) {
    …
}
```

#### ABSTRACT CLASSES
Abstract class is a template version of a parent class.
```php
abstract class ClassName {
    protected $_name;
    abstract public function getName();
}
```
Extend abstract class in a child class:
```php
class Cat extends Pet {
    function getName() {
        return $this->_name;
    }
}
```
Abstract method cannot be private! Abstract classes can have non-abstract methods, as well as attributes, all of which would also be inhereted by the derived class.

#### __toString()
PHP invokes ```__toString()``` automatically when an object of that type is used as a string. Just define it in your class. Used frequently as a debugging tool. The class variable will be shown as a string, and no error will be generated:
```php
$a = new SomeClass();
echo $a;
```

#### INTERFACE

An interface is provided so you can describe a set of functions and then hide the final implementation of those functions in an implementing class. This allows you to change the IMPLEMENTATION of those functions without changing how you use it. 
```php
interface iSomething {
    public function someFunction($var);
}
```
Associate a class with the interface:
```php
class SomeClass implements iSomething {
    …
}
```

#### Abstract Class vs. Interface
An abstract class has an "is a" relationship with the derived class. Intrface does not have "is a" relationship, rather having "has the same behaviors as" relationship with a derived class.

For example: I have a database. I want to write a class that accesses the data in my database. I define an interface like this:
```php
interface Database {
    function listOrders();
    function addOrder();
    function removeOrder();
...
}
```
Then let's say we start out using a MySQL database. So we write a class to access the MySQL database:
```php
class MySqlDatabase implements Database {
    function listOrders() {...
}
// We write these methods as needed to get to the MySQL database tables. Then // you can write your controller to use the interface as such:
    $database = new MySqlDatabase();
    foreach ($database->listOrders() as $order) {
// Then let's say we decide to migrate to an Oracle database. We could write // another class to get to the Oracle database as such:
    class OracleDatabase implements Database {
    public function listOrders() {...
}
```
Then - to switch our application to use the Oracle database instead of the MySQL database we only have to change ONE LINE of code:
```php
$database = new OracleDatabase();
```
all other lines of code, such as:
```php
foreach ($database->listOrders() as $order) {
```
will remain unchanged. The point is - the INTERFACE describes the methods that we need to access our database. It does NOT describe in any way HOW we achieve that. That's what the IMPLEMENTing class does. We can IMPLEMENT this interface as many times as we need in as many different ways as we need. We can then switch between implementations of the interface without impact to our code because the interface defines how we will use it regardless of how it actually works.

#### TRAITS
In PHP 5.4, traits solve the problem of single inheritance. Traits allow you to add functionality to a class without using inheritance. Traits cannot be instantiated. Traits may have abstract methods that must be implemented by any class that uses the trait.
```php
trait tSomeTrait {
    // Attributes
    function someFunction() {
        …
    }
}
```
Add a trait to a class with "use" keyword:
```php
class SomeClass {
    use tSomeTrait;
    // Rest of the class
}
```
Now, when object of the class is created, it has someFunction method:
```php
$obj = new SomeClass();
$obj->someFunction();
```

#### Traits vs. Interfaces:
An interface enforces stricter programming, ensuring that classes are designed to implement specific methods. The trait makes methods available to a class that the class itself does not define.

#### TYPE HINTING
The Type Hinting is indicting what type of value is expected. You can type hint with functions, interfaces, and arrays.
```php
class SomeClass {
    function doThis(OtherClass $var) {
        …
    }
}
```
If the calling code sends a wrong type $var, an error will be generated. They are exceptions that could be caught.

#### NAMESPACES
The namespaces are a way of encapsulating classes, interfaces, functions, and constants into separate directories to avoid name collision. You can use a namespace in multiple files.
To define a namespace use "namespace" keyword. It should be very first line of the code and content the name of the namespace (parent directory where this current script is sitting), except declare() statement can be first sometimes. 
```php
namespace SomeNamespace;
class SomeClass {
    …
}
```
Namespace can have subnamespaces:
```php
namespace MyUtilities\MyNamespace;
```
To use that class, you'd need to include the file that defines the namespace:
```php
require('SomeNamespace.php');
```
Then use backslashes to indicate a namespace is being used:
```php
$obj = new \SomeNamespace\SomeClass();
```
To represent current namespace use ```__NAMESPACE__``` constant.

PHP allows you to more quickly reference a namespace by bringing it into current scope via the "use" keyword:
```php
use MyNamespace\Company;
```
Now create an object by just referencing classes within the Company namespace:
```php
$obj = new Department();
```

#### DEPENDENCY INJECTION
Dependency Injection helps instantiate objects on the fly. It really decouples different code and helps easy maintenance, so you do not need to touch written code if you add more classes.

Simple way example:
```php
class Triangle extends Shape {
   public function draw() {
       echo "Triangle has been drawn";
   } 
}
class Circle extends Shape {
    public function draw() {
        echo "Circle has been drawn";
    }
}
class Shape {
    public function draw() {
        echo "Shape has been drawn";
    }
}
$Triangle =  new Triangle();
$Triangle->draw();
$Circle = new Circle();
$Circle->draw();
```
Slightly better with same classes, just adding a new function:
```php
function drawShape($shape) {
    $shape->draw();
}
$shape = new Circle();
drawShape($shape);
$shape2 = new Triangle();
drawShape($shape2);
```
Real Injection now. Make a class instead a function:
```php
class Drawing {    
    protected $shape;   
    public function setShape($shape) {     shape object is injected
        $this->shape = $shape;
    }    
    public function drawShape() {
        $this->shape->draw();
    }    
}
$Drawing = new Drawing();
$MyTriangle = new Triangle();
$Drawing->setShape($MyTriangle);
$Drawing->drawShape();
$MyCircle = new Circle();
$Drawing->setShape($MyCircle);
$Drawing->drawShape();
```
