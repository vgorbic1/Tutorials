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
