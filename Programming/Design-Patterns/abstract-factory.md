## Abstract Factory Pattern
The Abstract Factory Pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes.
The job of an Abstract Factory is to define an interface for creating a set of products. Each method in that interface is responsible for creating a concrete product, and we implement a subclass of the Abstract Factory to supply those implementations. So, factory methods are a natural way to implement your product methods in your abstract factories.
Abstract method creates objects through composition. It provides an abstract type for creating a family of products. Subclasses of this type define how those products are produced. To use the factory, you instantiate one and pass it into some code that is written against the abstract type.

![abstract-factory](https://cloud.githubusercontent.com/assets/13823751/16877025/f7a4b664-4a6b-11e6-9793-83e7c2364584.jpg)

