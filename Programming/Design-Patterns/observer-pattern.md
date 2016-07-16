## Observer Pattern
The Observer Pattern defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.
If you understand newspaper subscriptions, you pretty much understand the Observer Pattern, only we call the publisher the SUBJECT and the subscribers the OBSERVERS.

![observer](https://cloud.githubusercontent.com/assets/13823751/16876774/e5586272-4a6a-11e6-940a-90f8b8b7177e.jpg)

Strive for loosely coupled designs between objects that interact. They minimize interdependency between objects.
With Java's built-in support, all you have to do is extend Observable in java.util.Observable and tell it when to notify the Observers. The API does the rest for you.
