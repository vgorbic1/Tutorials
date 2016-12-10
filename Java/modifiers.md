## Modifiers
Modifiers control behavior and/or accessibility of classes, interfaces, variables, and methods.

### Class Modifiers
There is a limited set of modifiers that can be applied to classes:
- ```public``` modifier makes the class accessible from any package. If this modifier is not specified, the class will be accessible from the package it was declared.
- ```abstract``` modifier defines a class in which one or more methods are declared as skeletons - with the return type and the list of input parameters, but without the body. Abstract classes will further be explained in the “Abstract Classes” section.
- ```final``` modifier prohibits the class from being extended by other classes.

### Access Level Modifiers
Access level modifiers control the visibility of variables and methods of a class from other classes in the same or different packages. There are four access level modifiers (in order from less to more restrictive):

**public -> protected -> [no modifier] -> private**



