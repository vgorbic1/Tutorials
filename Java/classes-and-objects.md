##Classes and Objects
Java is an Object-Oriented language, meaning that its primary purpose is to manipulate objects. An Object is a logical entity 
consisting of data and code. All objects are built from templates called classes, which makes them central to the Java language. 
Any functionality you wish to implement in Java, must be constructed as a class.
![classes-objects](https://cloud.githubusercontent.com/assets/13823751/21015511/e0b9f228-bd27-11e6-8303-152cdf3cfe3c.jpg)
Classes are declared using the class statement:
```java
//Class Temperature provides functionality to convert
// temperatures from Celsius to Fahrenheit and vice versa
class Temperature {

  // Class variables and methods:
  static double t; // temperature value
  static double FtoC() // method for converting °F to °C
    {return (temp - 32 ) / 1.8;}
  static double CtoF() // method for converting °C to °F
    {return temp * 1.8 + 32;}
    
  // Instance variables and methods:
  double temp; // temperature value
  double toCelsius() // method for converting °F to °C
    {return (temp - 32 ) / 1.8;}
  double toFahrenheit () // method for converting °C to °F
    {return temp * 1.8 + 32;}
}
```
All variables and methods declared as static are called class variables and class methods, and can be used without creating any objects. Other variables and methods are called instance variables and instance methods, and can be used only through object instances.
```java
// Class variables and methods can be referenced via class name
Temperature.t = 77.0;
temp = Temperature.FtoC();
System.out.println(Temperature.t + "F=" + temp +"C");

// Class variables and methods can be referenced
// by their names directly (if the names are unique in the program)
t = 25.0;
temp = CtoF();
System.out.println(t + "C=" + temp +"F");
```
###Initializing Class Variables
During program execution, when a class is first used, i.e. when it is loaded into the Java Virtual Machine (JVM), its class variables are assigned default values. For numeric variables, the default value is zero. If there is a need to initialize a class variable to a non-default value, it can be done in the declaration statement itself, or in a statement block declared as static.
```java
// When the Temperature class is loaded into JVM
// the class variable tF will be assigned the value 77.0
// and the tC=FtoC(); code will run to calculate the tC value.
class Temperature {
  static double tF = 77.0; // class variable tF = 77.0
  static double tC; // class variable tC = 0.0
  static { 
    tC = FtoC(); 
  } // static statement block will convert tF to °C and put it into tC
  // method FtoC converts °F to °C
  static double FtoC() {
    return (tF - 32 ) / 1.8;
  }
}
```
- Declaration Rule: Class variables, methods, and statement blocks must be declared using the static modifier.
- Accessibility Rule: Class variables and methods can be referenced by their names directly if the name is unique, or via the class name in all cases.
- Execution Rule: All static declarations and statement blocks {…} of a class will be processed (i.e. executed) one time only, when the class is first used in the program.

##Instance Variables and Methods
The variables, methods, and statement blocks in a class declaration, that do not have the static modifier, are called instance variables, instance methods, and instance statement blocks. Their usage is subject to the following rules:
- Declaration Rule: Instance variables, methods, and statement blocks must be declared without the static modifier.
- Accessibility Rule: Instance variables and methods can be used only after an object (instance) of the class is created, and must be referenced via the object name
- Execution Rule: All instance declarations and statement blocks {…} of a class are processed (i.e. executed) each time an object (i.e. instance) of the class is created.

###Creating Objects
The process of creating a new object is called instantiation, and is performed using the **new** statement:
```java
myClass object1 = new myClass();
```
This is what happens during execution of the above statement:
- **myClass object1** declares the variable object1 of type myClass. This variable can be used to reference any object of class myClass, that’s why such variables are also called object references.
- The new operator creates a new object; all instance declarations of variables, statement blocks, and methods are processed.
- The myClass() method is invoked to optionally initialize the instance variables of the newly created object.
- The reference between the variable object1 and the new object is established.

####Constructors
