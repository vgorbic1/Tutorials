## Design Principles

#### The Open-Closed Principle (OCP)
Classes should be open for extension, and closed for modification.
Opening classes means allowing them to be subclassed and extended. The base class is closed for modification, but subclasses may have their own modifications. It is a combination or encapsulation and abstraction.

#### The Don't Repeat Yourself Principle (DRY)
Avoid duplicate code by abstracting out things that are common and placing those things in a single location.
Abstract out the common code and put it in one place. Remove the code from other locations and reference the code that was just abstracted. Make one requirement in one place.

#### The Single Responsibility Principle (SRP)
Every object in your system should have a single responsibility, and all the object's services should be focused on carrying out that single responsibility.
Make sure that a class does only one thing, and that it does it well. No other classes should share that behavior. It is the same as cohesion. The SRP will make your classes bigger, but overall application will be a lot simpler to manage and maintain. 
If you can say "itself" in use case, it should stay in the class, if not,  move that functionality somewhere else:
Automobile starts itself. -> OK
Automobile stops itself -> OK
Automobile drives itself. -> Not OK. Move it somewhere.

#### The Liskov Substitution Principle (LSP)
Subtypes must be substitutable for their base types.
It is all about well-designed inheritance. When you inherit from a base class, you must be able to substitute your subclass for that base class without things going terribly wrong. Otherwise, you've used inheritance incorrectly.

#### Delegate functionality to another class.
Delegation is when you hand over the responsibility for a particular task to another class or method.
Delegation is best used when you want to use another class's functionality, as is, without changing that behavior at all.

#### Composition
Use composition to assemble behaviors from other classes.  Use it when delegation isn't quite what you want, for example when you need to have more than one single behavior to choose from.
Composition is most powerful when you want to use behavior defined in an interface, and then choose from a variety of implementations of that interface, at both compile time and run time. Composition allows you to use behavior from a family of other classes, and to change that behavior at runtime.  Think of pizza. It's composed of different ingredients, but you can swap out different ingredients without affecting the overall pizza slice.
When an object is composed of other objects, and the owning object is destroyed, the objects that are part of the composition go away, too. Composition is really about ownership.

#### Aggregation
Aggregation is a composition without the abrupt ending. Aggregation is when one class is used as part of another class, but still exists outside of that other class. If the object does make sense existing on its own, then you should use aggregation; if not, then go with composition.

#### Inheritance
A class may inherit - use by default - the fields and methods of its superclass. Inheritance is transitive, so a class may inherit from another class which inherits from another class, and so on, up to a base class (typically Object, possibly implicit/absent). Subclasses may override some methods and/or fields to alter the default behavior.

#### Encapsulation
By interacting with objects instead of directly with the implementation of methods and fields, we hide and protect the implementation of a class. If a consumer does not know anything about an object other than its public interface, then it cannot rely on any internal implementation details.
