## Modifiers
Modifiers control behavior and/or accessibility of classes, interfaces, variables, and methods.

### Class Modifiers
There is a limited set of modifiers that can be applied to classes:
- ```public``` modifier makes the class accessible from any package. If this modifier is not specified, the class will be accessible from the package it was declared.
- ```abstract``` modifier defines a class in which one or more methods are declared as skeletons - with the return type and the list of input parameters, but without the body. Abstract classes will further be explained in the “Abstract Classes” section.
- ```final``` modifier prohibits the class from being extended by other classes.

### Access Level Modifiers
Access level modifiers control the visibility of variables and methods of a class from other classes in the same or different packages. There are four access level modifiers (in order from less to more restrictive):

**public -> protected -> [no modifier] -> private**

![modifiers](https://cloud.githubusercontent.com/assets/13823751/21074104/9220b0e0-beb5-11e6-81bf-0df0b3835693.jpg)

### Static Modifier
The static modifier indicates that the variable or method can be accessed before any object of the class is created. A good example is the main method that starts execution of an application. It must be declared static because it is called before any object exists.

### Final Modifier
The final modifier can be applied to variables, methods, and classes to "finalize" their declaration.
A **final variable** cannot be modified after it is assigned an initial value. That effectively makes a final variable a constant:
```java
final double pi = 3.1415926;
```
A **final method** cannot be overridden. If a class declares some method as final, the sub-classes of that class cannot create a method with the same signature as the final method.

A **final class** cannot have sub-classes, i.e. it cannot be inherited.
