## Design Patterns

A design pattern is a recommended best practice for solving a particular problem, or implement a certain functionality.

### Creational Patterns
The creational patterns used to generate one or more objects.

####The Singleton
The singleton pattern is a creational pattern that will restrict the application to create only one particular class style. Use for connection to a database.
```php
class SomeClass {
    static private $_instance = NULL;
    static function getInstance(){
        if (self::$_instance = NULL) {
            self::$_instance = new SomeClass();
        }
        return self::$_instance;
    }
}
```
To create an instance use this class:
```php
$obj1 = SomeClass::getInstance();
```
If a second object also calls that code, the same instance will be created.
```php
$obj2 = Someclass::getInstance();
```
Now both ```$obj1``` and ```$obj2``` refer to the same instance of ClassName.
The class constructor, that is empty, prevents a user from creating a new object of the class.

#### The Factory 
The factory pattern is used to manufacture potentially multiple objects of a specific type. The factory pattern become useful in situations where the type of object that needs to be generated isn’t known when the program is written but only once the program is running. Alternatively, abstract class and different derived subclasses will need to be created on the fly. Once you have created the object, regardless of its specific type, the use of that object will be consistent. The method takes at least one argument, which indicates the type of object to create. The method then returns an object of that type:
```php
static function Create($type) {
    // Valideate $type.
    return new SomeClassType();
} 
```
The Factory pattern is easily extendable. A variation on the Factory pattern is Abstract Factory, that outputs other facroies. 

###Structural Patterns
The structural patterns apply in situations where a nontraditional class structure, or a modification of an existing class structure, is required.

#### The Composite Pattern
The composite pattern applies in situations where you have an object that might represent a single entity or a composite entity, but still needs to be usable in the same manner. For example, you could show errors on the form or on a single element; you could validate the entire form at once or just a single element. Another sign that the composite pattern may apply is when you are working with tree-like structure.
Start with base abstract class:
```PHP
abstract class FormComponent {
    abstract function add(FormComponent $obj);
    abstract function remove(FormComponent $obj);
    abstract function display();
    abstract function validate();
    abstract function showError();
}
```
Each subclass now inherits from the derived class. The Form class implements a true add() method:
```PHP
class Form extends FormComponent {
    private $_elements = array();
    function add(FormComponent $job) {
       $this->_elements[] = $obj;
    }
    function display() {
    // Display the entire form
    }
}
```
The FormElement class has to define add() method, but the method should not do anything, because we do not have any subelements:
```php
class FormElement extends FormComponent {
    function add(FormComponent $obj) {
        return $obj; // or falce.
    }
    function display() {
        // Display the element.
    }
}
```
Finally, add elements to a form:
```php
$form = new Form();
$email = new FormElement();
$form->add($email);
```

###Behavioral Patterns
Behavioral patterns are used to address how an application runs. These patterns can change algorithm on the fly.

#### The Strategy Pattern
The strategy pattern is most useful in situations where you have classes that may be similar, but not related, and differ only in their specific behavior.
You have three behaviors that all apply to strings: stripping out HTML, crossing out swear words, catching insecure characters. These filters can be applied differently on the fly. This is a good candidate for the Strategy pattern.
Start with defining an interface with the needed functionality:
```php
interface Filter {
    function filter($str);
}
```
Next, create specific filter types:
```php
class HtmlFilter implements Filter {
    functrion filter($str) {
        // Strip out the HTML
        return $str;
    }
}
class SwearFilter implements Filter {
    function filter($string) {
        // Cross out swear words.
        return $str;
    }
}
```
Finally, another class would be written that could use any filter:
```php
class FormData {
    private $_data = NULL;
    function __construct($input) {
        $this->_data = $input;
    }
    function process(Filter $type) {
        $this->_data = $type->filter($this->_data);
    }
}
```
Now use it:
```php
$form = new FormData($someUserInput);
if (/* NO HTML ALLOWED */) {
    $form->process(new HtmlFilter());
}
if (/* NO SWEAR WORDS ALLOWED */) {
    $form->process(new SwearFilter());
}
```
