## C# Language
C# was created specifically for .NET. The language is sutable to develop:
- Console applications, which display no graphics.
- Windows applications, which use standard Windows interface.
- Web applications, which can be accessed with a browser.

The language is simple, but is highly expressive when it comes to implementing modern programming concepts. Developed by Anders Hejlsberg (also created Turbo Pascal) and Scott Wiltamuth.

#### Enumerations
Enums are strongly typed constants. They are essentially unique types that allow you to assign symbolic names to integral values. In the C# tradition, they are strongly typed, meaning that an enum of one type may not be implicitly assigned to an enum of another type even though the underlying value of their members are the same. Along the same lines, integral types and enums are not implicitly interchangable. All assignments between different enum types and integral types require an explicit cast.

**Declare enum:**
```c#
enum Temperatures {
  Wicked cold = 0,
  FreezingPoint = 32
}
```
**Declare enum with specific type:**
```c#
enum ServingSizes : unit {
  Small = 1,
  Regular = 2,
  Large = 3
}
```
Example of use:
```c#
class Values {

  enum Temperatures {
    WickedCold = 0,
    FreezingPoint = 32
  }
  
  static void Main() {
    System.Console.WriteLine("Wicked cold: {0}", (int) Temperatures.WickedCold);
    System.Console.WriteLine("Freezing point: {0}", (int) Temperatures.FreezingPoint);
  }
}
```
Another example with a switch statement:
```c#
using System;

// declares the enum
public enum Volume {
   Low,
   Medium,
   High
}

// demonstrates how to use the enum
class EnumSwitch {
   static void Main() {
      // create and initialize 
      // instance of enum type
      Volume myVolume = Volume.Medium;

      // make decision based
      // on enum value
      switch (myVolume) {
         case Volume.Low:
            Console.WriteLine("The volume has been turned Down.");
            break;
         case Volume.Medium:
            Console.WriteLine("The volume is in the middle.");
            break;
         case Volume.High:
            Console.WriteLine("The volume has been turned up.");
            break;
      }
      Console.ReadLine();
   }
}
```
