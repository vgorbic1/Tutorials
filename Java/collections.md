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

