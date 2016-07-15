Adapter Pattern
The adapter pattern converts the interface of a class into another interface the clients expect. Adopter lets classes work together that couldn’t otherwise because of incompatible interfaces.
-	The client makes a request to the adapter by calling a method on it using the target interface.
-	The adapter translates the request into one or more calls on the adaptee using the adaptee interface.
-	The client receives the results of the call and never knows there is an adapter doing the translation.
There are two kinds of adapters: object adapters and class adapters. Object adapter:

![adapter-1](https://cloud.githubusercontent.com/assets/13823751/16877388/658e8366-4a6d-11e6-8438-e6ca089107ad.png)

Class adapter works with multiple inheritance, so it is not possible with Java:

![adapter-2](https://cloud.githubusercontent.com/assets/13823751/16877400/78b62962-4a6d-11e6-8ca2-238863642017.png)

Example: 

![adapter-3](https://cloud.githubusercontent.com/assets/13823751/16877422/8dc0b110-4a6d-11e6-85f9-3a3c766ce2d2.png)
