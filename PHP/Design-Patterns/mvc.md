##The Model-View-Controller Pattern
Unlike the patterns we have seen this far, the Model-View-Controller (MVC)
pattern is actually quite complex. Its goal is to provide a methodology for
separating the business logic (model) from the display logic (view) and the
decisional controls (controller).

In a typical MVC setup, the user initiates an action (even a default one) by
calling the Controller. The Controller, in turn, interfaces with the Model,
causing it to perform some sort of action and, therefore, changing its state.
Finally, the View is called, thus causing the user interface to be refreshed to
reflect the changes in the Model and the action requested of the Controller,
and the cycle begins anew.

The clear advantage of the MVC pattern is its clear-cut approach to separating
each domain of an application into a separate container. This, in turn, makes
your applications easier to maintain and to extend, particularly because
you can easily modularize each element, minimizing the possibility of code
duplication.
