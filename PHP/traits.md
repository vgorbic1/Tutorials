##Traits
Traits are intended to provide horizontal reuse, without the complexity of multiple inheritance. Traits are best described as compiler assisted copy and paste—the code within a trait can be injected into one or more classes.
```php
namespace Ds\Util;
trait SecureDebugInfo {
  public function __debugInfo() {
    $info = (array) $this;
    foreach ($info as $key => $value) {
      // Hide elements starting with '_'
      if ($key[0] == '_') {
        unset($info[$key]);
      }
    }
  }
}
```
We have defined the ```__debugInfo``` magic method, which can now be added to any class simply by using the trait. This is done by reusing the ```use``` keyword (which is also used for importing namespaces).
```php
namespace Ds;
class MyClass {
  use Util\SecureDebugInfo;
}
```
Traits can define properties and methods, including static variants. Also, because they are almost literally copy-and-paste, keywords such as ```$this```, ```parent```, ```self```, and ```static```, will work exactly as you would expect.
You can use multiple traits in the same way you import multiple namespaces, either by using multiple ```use``` statements, or using a comma-separated list.

#### Namespaces
While you can define a trait within a namespace, unless you are within the traits namespace hierarchy, you must always specify the fully-qualified name. So, with our ```Ds\Util\SecureDebugInfo``` trait, inside the ```Ds\Util`` namespace, you can simply use ```SecureDebugInfo```. Within the ```Ds``` namespace, you can use ```Util\SecureDebugInfo```. In any other namespace, you must always
specify the fully-qualified name.

#### Inheritance and Precedence
While traits do not support inheritance from other traits, you can simply ```use``` a trait within another:
```php
trait One {
  public function one() { }
}

trait Two {
  public function two() { }
}

trait Three {
  use One, Two; // Trait three now comprises of all three traits.
  public function Three() { }
}
```
Whenever a trait is used within a class, any method that is defined within the class will override any method with the same name in the trait.

Additionally, when using a trait within a child class, any methods within the trait will override others with the same name that would normally be inherited.

Methods defined in traits that are used in the parent class are inherited identically to any other method in the parent class, and will resolve for ```parent::method()``` calls.
```php
class Numbers {
  use One; // Adds One->one()
  public function two() { }
  public function three() { }
}

class MoreNumbers extends Numbers {
  use Two; // Two->two() overrides Numbers->two()
  public function one() { } // Overrides Numbers->one() (Trait One->one)
}

class EvenMoreNumbers extends MoreNumbers {
  use Three; // Three->one() overrides MoreNumbers->one()
      // Three->two() overrides MoreNumbers->two()
      // (Trait Two->two)
      // Three->three() overrides inherited
      // Numbers->three()
public function three() { } // Overrides Three->three()
}
```

#### Trait Requirements
It is also possible to specify methods that must be defined by the class that uses the trait, so that the trait’s methods can reliably call it. This is done using abstract methods.
**Abstract trait methods**
```php
namespace Ds\Util;
trait SecureDebugInfo {
  public function __debugInfo() {
    return $this->getData();
  }
  
  abstract public function getData();
}
```
Here we define an abstract method ```getData()``` which is used by our concrete method, ```__debugInfo()```.
####Conflict Resolution
When using a trait, you may end up with two traits that have a conflicting method. When you do this, PHP will emit a fatal error. To resolve this, we must use the ```insteadof``` keyword to explictly resolve this conflict.
```php
class MyClass {
  use Ds\Util\SecureDebugInfo, My\Framework\DebugHelper {
      Ds\Util\SecureDebugInfo::__debugInfo insteadof My\Framework\DebugHelper;
  }
}
```
Note that we always use the static method syntax, with ```::```—and that we only need to specify the method itself on the left operand.

####Aliases and Method Visibility
If we wish to still be able to access a conflicted method, we can use an alias, using the ```as``` keyword.
```php
class MyClass {
  use MyTrait {
    MyTrait::myMethod as protected;
    MyTrait::myOtherMethod as private NewMethodName;
  }
}
```
In the first case, we are changing the visibility of the method; in the second, we are adding a new alias with different visibility.

####Detecting Traits
Because traits are like copy-and-paste, the instanceof operator does not work for detecting whether a class utilizes a trait. To check whether a class utilizes a trait, we use the ```class_uses()``` function, which returns an array which has both its keys and
values set to each of the traits in use:
```php
class Numbers {
  use One, Two;
}

var_dump(class_uses('MoreNumbers'));
```
The code above will return:
```
array(2) {
  ["One"]=>
    string(3) "One"
  ["Two"]=>
    string(3) "Two"
}
```
