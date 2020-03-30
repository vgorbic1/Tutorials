## Namespaces
One particularly useful new addition to PHP 5.3.0 is namespaces. Namespaces allow developers to sandbox their code, outside of the global namespace, to avoid class name conflicts and help organize their code better.
```php
namespace Framework {
  class Hello {
    public function world() {
      echo "Hello world!";
    }
  }
}

namespace Foo {
  // allows us to refer to the Hello class
  // without specifying its namespace each time
  use Framework\Hello as Hello;
  class Bar {
    function __construct() {
      // here we can refer to Framework\Hello as simply Hello
      // due to the preceding "use" statement
      $hello = new Hello();
      $hello->world();
    }
  }
}

namespace {
  $hello = new Framework\Hello();
  $hello->world(); // prints "Hello world!"
  $foo = new Foo\Bar();
  $foo->bar(); // prints "Hello world!"
}
```
The namespace itself remains within the global namespace, so it must remain unique; however, it can contain any number of classes, which can reuse class names that are in the global namespace, or within other namespaces.

Namespaces are not a requirement of the MVC design pattern, but they certainly do help to avoid class and function name collisions. Some popular MVC frameworks (such as Symphony) already organize their classes in namespaces.
