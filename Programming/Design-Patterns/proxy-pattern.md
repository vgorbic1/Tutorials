## Proxy Pattern
The Proxy Pattern provides a surrogate or placeholder for another object to control access to it. The proxy is a "representative for another object. A virtual proxy controls access to a resource that is expensive to create. A protection proxy controls access to a resource based on access rights.

![proxy1](https://cloud.githubusercontent.com/assets/13823751/16895692/6429148c-4b44-11e6-825e-d3152f9e9500.png)

![proxy2](https://cloud.githubusercontent.com/assets/13823751/16895695/6f41cfc6-4b44-11e6-8f6d-456f0b5b4dd8.png)

This diagram is the same as Strategy pattern. In general, think of the Strategy Pattern as a flexible alternative to subclassing. With Strategy you can change the behavior by composing with a different object. The State Pattern is an alternative to putting lots of conditionals in your context; by encapsulating the behaviors within state objects, you can simply change the state object in context to change its behavior.

Sometimes Proxy and Decorator look very similar, but their purposes are different; a decorator adds behavior to a class, while a proxy controls access to it.
A Caching Proxy maintains a cache of previous created objects and when a request is made it returns cached object, if possible.
#### PROTECTION PROXY
Java has a proxy class in java.lang.reflect. It crates the proxy class at runtime, so it is called dynamic proxy.

![proxy3](https://cloud.githubusercontent.com/assets/13823751/16895703/9933db62-4b44-11e6-8706-81c21bec08ac.png)

Protect Proxy is a proxy that controls access to an object based on access rights.
The proxy class has a static method called isProxyClass(). There are some restrictions on the types of interfaces to pass into newProxyInstance(). Check the javadoc. Java 5 makes all this process easier.
