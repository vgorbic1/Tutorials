##Packages
A package is a container for classes. All Java classes are spread across more than 200 packages. The fundamental classes reside in the **java.lang** package, which is always available to the Java compiler.
```java
import java.math.*;  // All classes from package java.math will be available
import java.io.FileReader; // Class FileReader from the package java.io will be available
class myClass { . . . }
```
User-defined classes are also placed into packages. For example, the myClass from the above example will be placed in a default, “no-name” package. To place it into a particular package, the first statement of the program (not counting comment lines) must be the package statement:
```java
package mypack.io;
import java.io.FileReader;
class myClass { . . . }
```
Here the myClass class will be placed into the mypack.io package. If mypack.io does not exist it will be created.

When a class is compiled without the package statement, it can be placed in any named package and be accessible by all classes in that package.
