## Instanceof
When working with objects, sometimes it might be not clear what class an object belongs to. For example, if class A is extended by classes B and C, an object reference of type A can reference objects of classes A, B, and C:
```java
A obj;
obj = new A(); // obj is a reference to an object of class A
obj = new B(); // obj is a reference to an object of class B
obj = new C(); // obj is now references an object of class C
```
An object reference of type Object can refer any object, of any class:
```java
Object obj;
obj = String(“text”);
obj = Integer(123);
obj = MyClass();
```
So, how can we determine the real type of an object referred by a variable? The answer is – with the help of the instanceof operator.
```java
Object obj;
obj = new String(“text”);
. . .
obj = new Date();
. . .
if (obj instanceof String) {
  System.out.println(“Object of type String”);
}
if (obj instanceof Date) {
  System.out.println(“Object of type Date”);
}
```
