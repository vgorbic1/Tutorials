## Object-Oriented Programming Languages
Here is the definition of object-oriented programming that I will be using for the rest 
of the article: assume we have a ‘classic’ OOP language, i.e., one that supports classes
with fields, methods, and single inheritance. No interfaces, no mixins, no aspects, no
multiple inheritance, no delegates, no closures, no lambdas, nothing but the basics:
- **Class**: a named concept in the domain space, with an optional superclass, defined as a set of fields and methods.
- **Field**: a named property of some type, which may reference another object (see composition)
- **Method**: a named function or procedure, with or without parameters, that implements some behavior for a class.
- **Inheritance**: a class may inherit - use by default - the fields and methods of its superclass. Inheritance is 
transitive, so a class may inherit from another class which inherits from another class, and so on, up to a base class 
(typically Object, possibly implicit/absent). Subclasses may override some methods and/or fields to alter the default 
behavior.
- **Composition**: when a Field’s type is a class, the field will hold a reference to another object, thus creating 
an association relationship between them. Without getting into the nuances of the difference between simple 
association, aggregation, and composition, let’s intuitively define composition as when the class uses 
another object to provide some or all of its functionality.
- **Encapsulation**: by interacting with objects instead of directly with the implementation of methods and fields, 
we hide and protect the implementation of a class. If a consumer does not know anything about an object other 
than its public interface, then it cannot rely on any internal implementation details.

Inheritance is fundamental to object-oriented programming. A programming language may have objects and messages, 
but without inheritance it is not object-oriented (merely “object-based”, but still polymorphic). 

Composition is also fundamental to every language. Even if the language does not support composition (rare these days!), 
humans still think in terms of parts and components. It would be impossible to break down complex problems into modular 
solutions without composition.

Composition is fairly easy to understand - we can see composition in everyday life: a chair has legs, a wall is composed 
of bricks and mortar, and so on. While the definition of inheritance is simple, it can become a complicated, tangled 
thing when used unwisely. Inheritance is more of an abstraction that we can only talk about, not touch directly. 
Though it is possible to mimic inheritance using composition in many situations, it is often unwieldy to do so. 
The purpose of composition is obvious: make wholes out of parts. The purpose of inheritance is a bit more complex 
because inheritance serves two purposes, semantics and mechanics. 

[SOURCE](https://www.thoughtworks.com/insights/blog/composition-vs-inheritance-how-choose)
