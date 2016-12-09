##Autoboxing / Auto-unboxing
Autoboxing automatically creates a type wrapper object and encapsulates a primitive type into it when an object of that type is needed. Auto-unboxing is the reverse process; it retrieves a primitive type from a type wrapper object when it is needed.
```java
class testWrapper {
  public static double test(Integer N) {
    return N; // Integer object N will be auto-unboxed to the primitive data type double
  }
  public static void main (String args[]) {
    int n = 123;
    double d = test(n); // Variable n of type int will be autoboxed into an Integer object
    System.out.println("d=" + d); // prints: d=123.0
  }
}
```
