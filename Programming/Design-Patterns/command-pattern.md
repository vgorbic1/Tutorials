##Command Pattern
The command pattern encapsulates a request as an object, thereby letting you parameterize other objects with different requests, queue or log requests, and support undoable operations.
Package the actions and the receiver up into an object that exposes just one method, execute(). When called, execute() causes the actions to be invoked on the receiver. 
The META COMMAND PATTERN allows you to create macros of commands so that you can execute multiple commands at once.

![command](https://cloud.githubusercontent.com/assets/13823751/16877284/fef40072-4a6c-11e6-851b-ddb645c06516.png)

#### Null Object.
A null object is useful when you don't have a meaningful object to return and yet you want to remove the responsibility for handling null form the client.
