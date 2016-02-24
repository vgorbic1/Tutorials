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
- 
![collection-extensions](https://cloud.githubusercontent.com/assets/13823751/13295709/bbaf68a2-daef-11e5-99d8-b8ad0b832799.jpg)

#### List

