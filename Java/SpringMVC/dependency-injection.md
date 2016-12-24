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
