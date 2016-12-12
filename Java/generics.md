## Generics
Generics is a feature of Java allowing the use of generic names when specifying the class type of object parameters in the declarations of classes, interfaces, methods, or constructors. For example, if two methods have same functionality but one receives an integer parameter, and another receives a double parameter, we can declare just one method and supply that method with a “generic” type of the parameter, which will be substituted with the proper type during compilation.

Let’s say that we want to create a method that acts on an object without knowing what its type is. One way of accomplishing that is by using the Object class – the superclass of all objects. We could accept an Object instance and then cast it to the desired type.

Generics is a compiler feature, not a run-time feature. All class type references are resolved at compile time.

####Generic Classes
Generic class is not much different from any regular Java class. What makes it "generic" is a small addition to the class declaration syntax:
```java
class G <T> {  //The < > notation identifies class G as generic
 ...
}
```
The <T> notation is a class type parameter in which T is a type-variable, i.e. parameter representing a class name. It indicates that an arbitrary (any) class name can be used in the declarations of variables and methods of the class:
```java
class myClass <T> {
  public T myValue;
  public void setValue(T obj) {
    myValue = obj;
  }

  public static void main (String args[]) {
    myClass<String> c = new myClass<String>();
    c.setValue(“test”);
    System.out.println(c.myValue); // prints: “test”

    myClass<Integer> n = new myClass<Integer>();
    n.setValue(123);
    System.out.println(n.myValue); // prints: “123”
  }
}
```
Note that we have to specify the class type parameter explicitly when creating objects of generic classes. This information is used by Java for type safety checking, making sure, for example, that an object reference of type myClass<String> does not point to an object of type myClass<Integer>.

The class declaration shown in the previous example (class myClass <T>) allows substitution of the type-variable T with any class name. In most cases, it is not desirable. Usually, we want to restrict the range of classes for which generic class objects can be built. We can achieve this by using another form of generic class declaration:
```
class G <T extends classname> { ... }
```
The classname parameter sets the upper boundary for class names that are allowed to be specified by the type-variable T and enforces that only the classname class or any class extending the classname can be specified by the T parameter. This is a part of the type safety mechanism provided by generics.
```java
abstract class AB { public abstract String myName(); }

class A extends AB { 
  public String myName() {
    return "A";
  }
}
  
class B extends AB { 
  public String myName() {
    return "B";
  }
}

class G <T extends AB> {  // The type-variable T can specify only class AB or its subclasses
  String name;
  G (T obj) { 
    name = obj.myName(); // class G constructor
  } 
}

public static void main (String args[]) {
  A a = new A();
  G g;
  g = new G(a); // Error! You have to specify explicitly the object type you are passing to the constructor of class G.
  g = new G<AB>(a); // Compiler will check if the reference "a" is of type AB or its subclasses
  G<B> b; // Ensures that "b" can reference only G objects created with the input parameter of type B.
  b = new G<B>(new B()); // Compiler will check that the input parameter new B() is of type B (and it is), and that b 
        //can reference a G object created with the input parameter of this type.
  g = b; // OK. The g and b are both of type G
  b = g; // "Unsafe conversion" error: b can only reference G objects created with input parameter of type B, 
        // but g could point to the G object created with input parameter of type AB, A, or B
  }
```
####Passing Generic Classes as Parameters
Objects of generic classes can be passed as parameters to methods, in the same way as other Java objects:
```java
class GenericClass <T> {…}
. . .
public void myMethod(GenericClass g) {…}
. . .
GenericClass<A> a = new GenericClass<A>( ); // The a variable references an object of type GenericClass<A>
GenericClass<B> b = new GenericClass<B>( ); // The b variable references an object of type GenericClass<B>
myMethod(a);
myMethod(b);
```
myMethod() can accept any object of type GenericClass regardless of the type-variable T used in creating those objects. We can add some type safety checking to the process by specifying restrictions for the input parameter of myMethod(). This is accomplished with the help of the wildcard parameter <?>:
```java
abstract class AB { ... }
class A extends AB { ... }
class B extends AB { ... }
. . .
class G <T extends AB> { // Objects of generic class G can be of types G, G<AB>, G<A>, or G<B>
. . .
  public void myMethod(G<?> g) {…} // Object g can be of any type allowed by the class G declaration
  public void myMethod(G<? extends AB> g) {…} // Object g can be of type G<AB> or its sub-classes (i.e. G<AB>, G<A>, G<B>)
  public void myMethod(G<? super B> g) {…} // Object g can be of type G<B> or its super-classes (i.e. G<B> or G<AB>)
```
In this example ```<? extends AB>``` sets the upper boundary for passing object references, and ```<? super B>``` sets the lower boundary.
