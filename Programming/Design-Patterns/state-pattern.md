## State Pattern
The State Pattern allows an object to alter its behavior when its internal state changes. The object will appear to change its class.

![state](https://cloud.githubusercontent.com/assets/13823751/16895678/0637a2d0-4b44-11e6-9ade-be2cc5e0832f.png)

This diagram is the same as Strategy pattern. In general, think of the Strategy Pattern as a flexible alternative to subclassing. With Strategy you can change the behavior by composing with a different object. The State Pattern is an alternative to putting lots of conditionals in your context; by encapsulating the behaviors within state objects, you can simply change the state object in context to change its behavior.
