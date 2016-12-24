## Dependency Injection
Many people use the terms dependency injection and Inversion of Control (IoC) interchangeably.

You have two compolnents, A and B, and A depends on B:
```java
public class A {
  public void method() {
    B b = new B();
    b.method();
}
```
A must obtain an instance of B before it can use B. It can be problematic if B is an interface with many implementations.
You will have to choose an implementation of B and by doing so you reduce the reusability of A because you cannot
use A with the implementations of B that you did not choose.

Dependency injection takes over object creation and injects dipendencies to an object that needs them. Framework would create
an instance of A and instance of B and inject the latter to the former. For this you need to create a **set** method or a special constructor in the target class:
```java
public class A {
  private B b;
  public void method() {
    b.method();
  }
  public void setB(B b) {
    this.b = b;
  }
}
```
or
```java
public class A {
  private B b;
  public A(B b) {
    this.b = b;
  }
  public void method() {
    b.method();
  }
}
````
