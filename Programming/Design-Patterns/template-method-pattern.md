## Template Method Pattern
The template method pattern defines the steps of an algorithm and allows subclasses to provide the implementation for one or more steps. The template method pattern defines the skeleton of an algorithm in a method, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm's structure. This pattern is all about creating pattern for algorithm.

![template](https://cloud.githubusercontent.com/assets/13823751/16895642/243d5c26-4b43-11e6-8f6b-6b1555a4c856.png)

Hollywood Principle:
Don't call us, we'll call you. With the Hollywood principle, we allow low-level components to hook themselves into a system, but the high-level components determine when they are needed, and how.
