##Type Wrappers
The usage of primitive data types has its limitations. Many of the data structures operate on objects. For example, you cannot construct 
a set of integers. That’s why Java provides type wrappers – classes that encapsulate a primitive type within an object. 
There is one wrapper for each primitive type: Double, Float, Long, Integer, Short, Byte, Character, and Boolean.

Each of the above classes offers a wide range of methods (most of them static) allowing various manipulations over the underlying primitive type including the conversions between different 
primitive types.
```java
Integer N = Integer.valueOf(10); // N is an Integer object
int n = N.intValue();
double d = N.doubleValue();
String s = Integer.toBinaryString(n);
System.out.println("n="+ n + " d=" + d + " s=" + s);
// The output of this program is “n=10 d=10.0 s=1010”.
```
