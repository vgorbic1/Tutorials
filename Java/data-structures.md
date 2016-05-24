##Data Structures (Legacy!)

The data structures provided by the Java utility package are very powerful and perform a wide range of functions. These data structures consist of the following interface and classes:
-	Enumeration
-	BitSet
-	Vector
-	Stack
-	Dictionary
-	Hashtable
-	Properties

All these classes are now legacy and Java-2 has introduced a new framework called Collections Framework.

#### Enumeration
The Enumeration interface isn't itself a data structure, but it is very important within the context of other data structures. The Enumeration interface defines the methods by which you can enumerate (obtain one at a time) the elements in a collection of objects. This legacy interface has been superseded by Iterator. Although not deprecated, Enumeration is considered obsolete for new code. However, it is used by several methods defined by the legacy classes such as Vector and Properties, is used by several other API classes, and is currently in widespread use in application code.

Enumeration has the following methods:

```boolean hasMoreElements( )```

When implemented, it must return true while there are still more elements to extract, and false when all the elements have been enumerated.

```Object nextElement( )```

This returns the next object in the enumeration as a generic Object reference.
```java
import java.util.Vector;
import java.util.Enumeration;

public class EnumerationTester {

   public static void main(String args[]) {
      Enumeration days;
      Vector dayNames = new Vector();
      dayNames.add("Sunday");
      dayNames.add("Monday");
      dayNames.add("Tuesday");
      dayNames.add("Wednesday");
      dayNames.add("Thursday");
      dayNames.add("Friday");
      dayNames.add("Saturday");
      days = dayNames.elements();
      while (days.hasMoreElements()){
         System.out.println(days.nextElement()); 
      }
   }
}
```
This would produce the following result:
```
Sunday
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
```
#### BitSet
A BitSet class creates a special type of array that holds bit values. The BitSet array can increase in size as needed. This makes it similar to a vector of bits. This is a legacy class but it has been completely re-engineered in Java 2, version 1.4.
[More here](http://www.tutorialspoint.com/java/java_bitset_class.htm)

#### Vector
Vector implements a dynamic array. It is similar to ArrayList, but with two differences:

-	Vector is synchronized.
-	Vector contains many legacy methods that are not part of the collections framework.

The Vector class is similar to a traditional Java array, except that it can grow as necessary to accommodate new elements. Like an array, elements of a Vector object can be accessed via an index into the vector.
The nice thing about using the Vector class is that you don't have to worry about setting it to a specific size upon creation; it shrinks and grows automatically when necessary.
[More here](http://www.tutorialspoint.com/java/java_vector_class.htm)

#### Stack
Stack is a subclass of Vector that implements a standard last-in, first-out stack. Stack only defines the default constructor, which creates an empty stack. Stack includes all the methods defined by Vector, and adds several of its own. You can think of a stack literally as a vertical stack of objects; when you add a new element, it gets stacked on top of the others. When you pull an element off the stack, it comes off the top. In other words, the last element you added to the stack is the first one to come back off.
[More here](http://www.tutorialspoint.com/java/java_stack_class.htm)

#### Dictionary
The Dictionary class is an abstract class that defines a data structure for mapping keys to values. This is useful in cases where you want to be able to access data via a particular key rather than an integer index. Since the Dictionary class is abstract, it provides only the framework for a key-mapped data structure rather than a specific implementation. Dictionary is an abstract class that represents a key/value storage repository and operates much like Map. Given a key and value, you can store the value in a Dictionary object. Once the value is stored, you can retrieve it by using its key. Thus, like a map, a dictionary can be thought of as a list of key/value pairs. The Dictionary class is obsolete. You should implement the Map interface to obtain key/value storage functionality.

#### Hashtable
Hashtable was part of the original java.util and is a concrete implementation of a Dictionary. However, Java 2 re-engineered Hashtable so that it also implements the Map interface. Thus, Hashtable is now integrated into the collections framework. It is similar to HashMap, but is synchronized. Like HashMap, Hashtable stores key/value pairs in a hash table. When using a Hashtable, you specify an object that is used as a key, and the value that you want linked to that key. The key is then hashed, and the resulting hash code is used as the index at which the value is stored within the table.
[More here](http://www.tutorialspoint.com/java/java_hashtable_class.htm)

#### Properties
Properties is a subclass of Hashtable. It is used to maintain lists of values in which the key is a String and the value is also a String. The Properties class is used by many other Java classes. For example, it is the type of object returned by System.getProperties( ) when obtaining environmental values.
[More here](http://www.tutorialspoint.com/java/java_properties_class.htm)
