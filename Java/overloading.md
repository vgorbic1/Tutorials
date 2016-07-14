## Method Overloading
An overloaded method is just a different method that happens to have the same method name. It has nothing to do with inheritance and polymorphism.
When you have two methods with the same name in one class, but one has a passing variable and another is empty:
```java
public class MyMethods {
  int total() {
    int aValue = 10 + 10;
    return aValue;
  }

  int total(int aNumber) {
    int aValue = aNumber + 20;
    return aValue;
  }
}
```
Use as many ```total()``` methods as you want, as long as they all of a different types (int, double, float);
