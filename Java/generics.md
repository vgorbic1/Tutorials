## Generics
Generics is a feature of Java allowing the use of generic names when specifying the class type of object parameters in the declarations of classes, interfaces, methods, or constructors. For example, if two methods have same functionality but one receives an integer parameter, and another receives a double parameter, we can declare just one method and supply that method with a “generic” type of the parameter, which will be substituted with the proper type during compilation.

Let’s say that we want to create a method that acts on an object without knowing what its type is. One way of accomplishing that is by using the Object class – the superclass of all objects. We could accept an Object instance and then cast it to the desired type.

Generics is a compiler feature, not a run-time feature. All class type references are resolved at compile time.

