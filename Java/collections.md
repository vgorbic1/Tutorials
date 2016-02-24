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

