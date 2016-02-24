## Collections
The Java Collections API's provide Java developers with a set of classes and interfaces that makes it easier to handle collections of objects. In a sense, Collection's works a bit as arrays, except their size can change dynamically, and they have more advanced behavior than arrays. Most of the Java collections are located in the java.util package.
In order to understand and use the Java Collections API effectively it is useful to have an overview of the interfaces it contains. There are two "groups" of interfaces:

**Collections**

![collections](https://cloud.githubusercontent.com/assets/13823751/13294665/ab63f030-daea-11e5-9f54-92856156b287.png)

**Maps**

![maps](https://cloud.githubusercontent.com/assets/13823751/13294700/d86fdee0-daea-11e5-9287-b356b0dd3e08.png)

#### History
Prior to Java 2, Java provided ad hoc classes such as Dictionary, Vector, Stack, and Properties to store and manipulate groups of objects. Although these classes were quite useful, they lacked a central, unifying theme. Thus, the way that you used Vector was different from the way that you used Properties. The collections framework was designed to meet several goals:
- The framework had to be high-performance. The implementations for the fundamental collections (dynamic arrays, linked lists, trees, and hashtables) are highly efficient.
- The framework had to allow different types of collections to work in a similar manner and with a high degree of interoperability.
- Extending and/or adapting a collection had to be easy.

Towards this end, the entire collections framework is designed around a set of standard interfaces. Several standard implementations such as LinkedList, HashSet, and TreeSet, of these interfaces are provided that you may use as-is and you may also implement your own collection, if you choose.

#### Collection
Collection interface enables you to work with groups of objects; it is at the top of the collections hierarchy.
Regardless of what Collection subtype you are using there are a few standard methods to add and remove elements from a Collection:
```java
String anElement = "an element";
Collection collection = new HashSet();
boolean didCollectionChange = collection.add(anElement);
boolean wasElementRemoved = collection.remove(anElement);   
```
Check if a collection contains a certain element:
```java
Collection collection = new HashSet();
boolean containsElement = collection.contains("an element");
Collection elements = new HashSet();
boolean containsAll = collection.containsAll(elements);
```
To get a collection size:
```java
int numberOfElements = collection.size();
```
Iterating a Collection:
```java
Collection collection = new HashSet();
//... add elements to the collection
```
Using iterator:
```java
Iterator iterator = collection.iterator();
while (iterator.hasNext()){
  Object object = iterator.next();
    //do something to object;    
}
```
Using for-loop:
```java
for (Object object : collection) {
    //do something to object;
}
```
The Collection interface can be generified:
```java
Collection<String> stringCollection = new HashSet<String>();
```
This stringCollection can now only contain String instances. If you try to add anything else, or cast the elements in the collection to any other type than String, the compiler will complain.

#### Extensions of Collection interface
- **LIST** stores an ordered collection of elements.
- **SET** must contain unique elements.
- **MAP** maps unique keys to values.
- **ENUMERATION** is legacy interface and defines the methods by which you can enumerate (obtain one at a time) the elements in a collection of objects. This legacy interface has been superseded by Iterator.

![collection-extensions](https://cloud.githubusercontent.com/assets/13823751/13295709/bbaf68a2-daef-11e5-99d8-b8ad0b832799.jpg)

#### List
The `java.util.List` interface is a subtype of the java.util.Collection interface. It represents an ordered list of objects, meaning you can access the elements of a List in a specific order, and by an index too. You can also add the same element more than once to a List. You can choose between the following List implementations in the Java Collections API: `java.util.ArrayList`, `java.util.LinkedList`, `java.util.Vector`, `java.util.Stack`.

Do not forget to import the interface collections you are about to use!

In the List:
- Elements can be inserted or accessed by their position in the list, using a zero-based index.
- A list may contain duplicate elements.
- In addition to the methods defined by Collection, List defines some of its own. 
- Several of the list methods will throw an `UnsupportedOperationException` if the collection cannot be modified, and a `ClassCastException` is generated when one object is incompatible with another.

Create a List instance:
```java
List listA = new ArrayList();
List listB = new LinkedList();
List listC = new Vector();
List listD = new Stack();
```
Here all elements are untyped (have type Object);

Add and an element:
```java
List listA = new ArrayList();
listA.add("element 1");
listA.add("element 2");
listA.add("element 3");

listA.add(0, "element 0");
```
Access the elements:
```java
List listA = new ArrayList();
listA.add("element 0");
listA.add("element 1");
listA.add("element 2");
String element0 = listA.get(0);
String element1 = listA.get(1);
String element3 = listA.get(2);
```
Remove elements:

`remove(Object element)` removes that element in the list, if it is present. All subsequent elements in the list are then moved up in the list. Their index thus decreases by 1.
`remove(int index)` removes the element at the given index. All subsequent elements in the list are then moved up in the list. Their index thus decreases by 1.
```java
Clearing a List:
List list = new ArrayList();
list.add("object 1");
list.add("object 2");
list.clear();
```
List Size:
```java
List list = new ArrayList();
list.add("object 1");
list.add("object 2");
int size = list.size();
```
Generic Lists:

By default you can put any Object into a List, but from Java 5, Java Generics makes it possible to limit the types of object you can insert into a List:
```java
List<MyObject> list = new ArrayList<MyObject>();
```
This List can now only have MyObject instances inserted into it. You can then access and iterate its elements without casting them:
```java
MyObject myObject = list.get(0);
for (MyObject anObject : list){
   //do someting to anObject...
}
```
Iterating a List:

The nice thing about Collections and Iterator is that each Collection object knows how to create its own Iterator. Calling iterator() on an ArrayList returns a concrete Iterator made for ArrayLists, but you never need to see or worry about the concrete class it uses. You just use the Iterator interface.
Use an Iterator:
```java
List list = new ArrayList();
  //add elements to list
Iterator iterator = list.iterator();
while(iterator.hasNext()) {
    Object next = iterator.next();
}

 // or for generic list:
List<String> mylistStr = new ArrayList<>();
Iterator<String> iterator = mylistStr.iterator();
while(iterator.hasNext()){
    String obj = iterator.next();
}
```
Use for loop:
```java
List list = new ArrayList();
  //add elements to list
for (int i=0; i < list.size(); i++) {
    Object obj = list.get(i);
}

  // or for generic list:
List<String> list = new ArrayList<String>();
  // add elements to list
for (int i=0; i<list.size(); i++){
    String next = list.get(i);
}
```

Use for-each (a.k.a for/in) loop:
```java
List list = new ArrayList();
  // add elements to list
for(Object obj : list) {  }
```
Example:
```java
ArrayList items = new ArrayList();
items.add(new MenuItem("Pancakes", 1.59);
items.add(new MenuItem("Toast", 0.59);
for (MenuItem item: items) {
    System.out.prntln("Breakfast item: " + item);
}
  // or for generic list:
List<String> list = new ArrayList<String>();
  // add elements to list
for(String obj : list) {  }
```
**Linked List** 

In linkedList you can walk the list forwards or backwards, but finding a position in the list takes time proportional to the size of the list. Each element of a LinkedList has more memory overhead since pointers to the next and previous elements are also stored.

LinkedList Example:
```java
import java.util.*;
public class LinkedListDemo {
   public static void main(String args[]) {
      // create a linked list
      LinkedList ll = new LinkedList();
      // add elements to the linked list
      ll.add("F");
      ll.add("B");
      ll.add("D");
      ll.add("E");
      ll.add("C");
      ll.addLast("Z");
      ll.addFirst("A");
      ll.add(1, "A2");
      System.out.println("Original contents of ll: " + ll);
      // remove elements from the linked list
      ll.remove("F");
      ll.remove(2);
      System.out.println("Contents of ll after deletion: "
       + ll);      
      // remove first and last elements
      ll.removeFirst();
      ll.removeLast();
      System.out.println("ll after deleting first and last: "
       + ll);
      // get and set a value
      Object val = ll.get(2);
      ll.set(2, (String) val + " Changed");
      System.out.println("ll after change: " + ll);
   }
}
```
**Array List** 

ArrayList allow fast random read access, so you can grab any element in constant time. But adding or removing from anywhere but the end requires shifting all the latter elements over, either to make an opening or fill the gap. ArrayLists take up as much memory as is allocated for the capacity, regardless of whether elements have actually been added.

ArrayList Example:
```java
import java.util.*;
public class ArrayListDemo {
   public static void main(String args[]) {
      // create an array list
      ArrayList al = new ArrayList();
      System.out.println("Initial size of al: " + al.size());
      // add elements to the array list
      al.add("C");
      al.add("A");
      al.add("E");
      al.add("B");
      al.add("D");
      al.add("F");
      al.add(1, "A2");
      System.out.println("Size of al after additions: " + al.size());
      // display the array list
      System.out.println("Contents of al: " + al);
      // Remove elements from the array list
      al.remove("F");
      al.remove(2);
      System.out.println("Size of al after deletions: " + al.size());
      System.out.println("Contents of al: " + al);
   }
}
```

**Vector**

A Vector is a resizable-array, ordered implementation of the List<E> interface that permits all elements including null. Vector allows random access to elements and is similar to ArrayList apart from being synchronized. In fact Vector is one of the two original collections shipped with Java, the other being Hashtable. Vector was retrofitted to implement List<E> interface, so that it became a part of The Collections Framework when the framework was introduced in version 1.2. There is no sound reason since the introduction of the ArrayList<E> class to use the Vector<E> class. If you need an ArrayList to be synchronized this can be achieved using methods of the Collections class without all the overheads of using Vector<E> synchronized methods.

#### Set
The java.util.Set interface is a subtype of the java.util.Collection interface. It represents set of objects, meaning each element can only exists once in a Set. You can choose between the following Set implementations in the Java Collections API: `java.util.EnumSet`, `java.util.HashSet`, `java.util.LinkedHashSet`, `java.util.TreeSet`.

Create a set:
```java
Set setA = new EnumSet();
Set setB = new HashSet();
Set setC = new LinkedHashSet();
Set setD = new TreeSet();
```
Adding an element to a set:
```java
Set setA = new HashSet();
setA.add("element 1");
setA.add("element 2");
setA.add("element 3");
```
Iterate through a set:
```java
Set setA = new HashSet();
setA.add("element 0");
setA.add("element 1");
setA.add("element 2");
```
Access via Iterator:
```java
Iterator iterator = setA.iterator();
while(iterator.hasNext(){
  String element = (String) iterator.next();
}
```
Access via new for-loop:
```java
for(Object object : setA) {
    String element = (String) object;
}
```
Removing an element:
```java
You remove elements by calling the remove(Object o) method. There is no way to remove an object based on index in a Set, since the order of the elements depends on the Set implementation.
```
Sets can be generic:
```java
Set<MyObject> set = new HashSet<MyObject>();
for(MyObject anObject : set){
   //do someting to anObject...
}
```
**HashSet**

A hash table stores information by using a mechanism called hashing. In hashing, the informational content of a key is used to determine a unique value, called its hash code. The hash code is then used as the index at which the data associated with the key is stored. The transformation of the key into its hash code is performed automatically.
```java
import java.util.*;
public class HashSetDemo {
   public static void main(String args[]) {
      // create a hash set
      HashSet hs = new HashSet();
      // add elements to the hash set
      hs.add("B");
      hs.add("A");
      hs.add("D");
      hs.add("E");
      hs.add("C");
      hs.add("F");
      System.out.println(hs);
   }
}
```
This would produce the following result: [D, E, F, A, B, C]

**LinkedHashSet**

LinkedHashSet maintains a linked list of the entries in the set, in the order in which they were inserted. This allows insertion-order iteration over the set. That is, when cycling through a LinkedHashSet using an iterator, the elements will be returned in the order in which they were inserted. The hash code is then used as the index at which the data associated with the key is stored. The transformation of the key into its hash code is performed automatically.

LinkedHashSet Example:
```java
import java.util.*;
public class HashSetDemo {
   public static void main(String args[]) {
      // create a hash set
      LinkedHashSet hs = new LinkedHashSet();
      // add elements to the hash set
      hs.add("B");
      hs.add("A");
      hs.add("D");
      hs.add("E");
      hs.add("C");
      hs.add("F");
      System.out.println(hs);
   }
}
```
This would produce the following result: [B, A, D, E, C, F]

**TreeSet**

Objects are stored in sorted, ascending order. Access and retrieval times are quite fast, which makes TreeSet an excellent choice when storing large amounts of sorted information that must be found quickly.

Tree Set Example:
```java
import java.util.*;
public class TreeSetDemo {
   public static void main(String args[]) {
      // Create a tree set
      TreeSet ts = new TreeSet();
      // Add elements to the tree set
      ts.add("C");
      ts.add("A");
      ts.add("B");
      ts.add("E");
      ts.add("F");
      ts.add("D");
      System.out.println(ts);
   }
}
```
This would produce the following result: [A, B, C, D, E, F]

![list-set](https://cloud.githubusercontent.com/assets/13823751/13297812/d30341ae-daf9-11e5-86a7-de8e55160d10.jpg)

#### Map
