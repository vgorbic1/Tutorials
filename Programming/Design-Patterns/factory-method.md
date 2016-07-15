##Factory Method 
The factory method Pattern defines an interface for creating an object, but lets subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses. 

![factory-method](https://cloud.githubusercontent.com/assets/13823751/16876937/9cc85764-4a6b-11e6-973a-dc08e9d90b40.jpg)

Depend upon abstractions. Do not depend upon concrete classes. High-level components should not depend on out low-level components; rather, they should both depend on abstractions. A high-level component I s a class with behavior defined in terms of other, low-level components.
These are the guidelines to follow the Dependency Inversion Principle:
-	No variables should hold a reference to a concrete class. If you use "new", you will be holding a reference to a concrete class. Use factory to get around that. 
-	No class should derive from a concrete class. If you derive from a concrete class, you're dependent on the concrete class. Derive from an abstraction, like an interface or an abstract class.
-	No method should override an implementation method of any of its base classes. If you override an implemented method, then your base class wasn't really an abstraction to start with. Those methods implemented in the base class are meant to be shared by all your subclasses.
Factory method creates objects through inheritance. Use your subclasses to create objects for you. Clients only need to know the abstract type they are using, the subclass worries about the concrete type.
