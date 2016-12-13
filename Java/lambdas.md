##Lambda Expressions
A lambda expression is a special construct of the Java language used for defining custom methods outside of any class.

In reality, the lambda expression automatically declares a “hidden” class, creates an instance of that class, and attaches the specified method to it.

Create a method converting any text to uppercase **traditional** way:
```java
class myClass {
  String transform(String s) { 
    return s.toUpperCase();
  }
}

myClass c = new myClass();
System.out.println( c.transform("text") ); // prints: "TEXT"
```
The same transform method declared using **lambda expression**:
```java
interface myInterface {  // We need to create an interface that must declare only one method. This is called a "functional interface"
  String transform(String s);
}

myInterface upper = (txt) -> {return txt.toUpperCase();}; // "txt" substitutes the input parameter, 
      // followed by the body of the transform method
System.out.println( upper.transform("text") ); // prints: "TEXT"
      // "upper" is an object of a hidden class that implements myInterface

myInterface lower = txt -> txt.toLowerCase();
System.out.println( lower.transform("TEXT") ); // prints: "text"
```
Lambda expressions are used when it is not practical to create a new class for just one or for a rarely used method. Also, the same interface can be used for creating of many different methods. 
To fully explore this capability, the package java.util.function provides several predefined functional interfaces to be used in lambda expressions. One of these functional interfaces – Function<T,R>, applies its method apply() to object of type T and returns the result as an object of type R. The [partial] declaration of the Function interface looks as follows:
```java
public interface Function <T, R> {
  R apply(T t);
  . . .
}
```
Let’s use this interface and a lambda expression to create a method that transforms digits into words:
```java
import java.util.function.*;
. . .
Function<Integer, String> spell = N ->    // "spell" is an object of a hidden class that implements the Function interface
       // "N" will be the input parameter to apply()
{  // This block will become the body of the apply() method
  String digits [] = {"zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"};
  return digits[N.intValue()]; // Returns N’th element of array digits
};

Integer N = Integer.valueOf(4); // Creates object of type Integer with the value of 4
System.out.println(spell.apply(N)); // Calls the apply() method of the object spell and prints: "four"
```
In general, it is not necessary to explicitly declare functional interface object references. A lambda expression itself can be viewed (and used) as an object of the corresponding functional interface. For example, we can pass a lambda expression as a parameter to a method if that parameter is declared as a functional interface.
