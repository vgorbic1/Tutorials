## Java
Object-oriented programming (OOP) is a programming paradigm that uses “objects” and their interactions to design applications and computer programs. Instead of thinking of our program as a bunch of functions, we need to think of our program as a bunch of objects that interact. A class definition includes everything that an object knows, and everything that it does all in the same file. Things an object knows about itself are called instance variables (state) Different objects of the same type (class) can have different states. Things an object can do are called methods.

#### Datatypes
Primitive data types hold the actual data and have different sizes:
    boolean
    byte (8 bits)
    char (16 bits)
    short (16 bits)
    int (32 bits)
    float (32 bits)
    long (64 bits)
    double (64 bits)
   
Object references only hold something that points to an object. References are all the same size and allow us to access and control objects. 

Access Levels and Access Modifiers
Public – least restrictive. Anyone anywhere can access it. Use for classes, constants (static final variables), and methods that you are exposing to other code (for example getters and setters) and most constructors.
Protected – allows subclasses outside the package to inherit the protected item.
Default – only code within the same package as the class with default can access it.
Private – only code within the same class can access it. It is private to a class, not private to an object! One Dog can see another Dog privates, but not Cat privates. Use privates for all instance variables and methods that you don’t want to call from outside. 

Array
An array is just a special object that holds more than one of something.
int[] nums = new int[7];
Now set numbers into the items in an array:
nums[0] = 6;
nums[1] = 19;
nums[2] = 44;
nums[3] = 42;
nums[4] = 10;
nums[5] = 20;
nums[6] = 1;

Arrays of objects are really arrays of object references.
Dog[] pets = new Dog[7];
pets[0] = new Dog();
pets[1] = new Dog();

Call methods on the first two elements like this:
pets[0].bark();
pets[1].bark();

MULTIDIMENSIONAL ARRAY
In Java it is just an array of arrays:
int[][] a2d = new int [4][2];
JVM creates an array with 4 elements. Each of these four elements is a reference variable to a newly created int array with two integer elements.
To access the secod element in the third array: int x = a2b[2][1];

Enumerations
Ennum is a special kind of class that extends java.lang. 
public enum Members {JERRY, BOBBY, PHIL};
public Members selectedBandMember;
If (selectedBandMember == Members.JERRY) {
   // do Jerry stuff
}

Encapsulation
Also called hiding data. Make your instance variables private.
private int size;
Create public accessor (getter) methods for the instance variable:
public int getSize() {
    return size;
}
 And public mutator (setter) method for the instance variable:
public void setSize(int x) {
    size = x;
}

Cast
The issue with math in Java is that computers have two ways of doing calculations. Integer math is much faster for most computers. Because of this most programming languages try to use integer math whenever possible. However, integer math can only use integers so when we want to have floating point answers sometimes we need to tell the compiler to use floating point math. When we have only one type of primitive, either all integers or all floating point, then the computer just uses the correct functions. It is when a calculation has mixed types of primitives or when the results needs to be floating point that we sometimes need to tell the compiler what to do. When we mix primitives we usually have to convert the integers to a floating points type. This is called a cast. We only had to cast one of the ints to a double to force the computer to use its floating point operation.
int x = 5;
int y = 7;
double v = (double)x / y;

Converting Strings to primitives
Everything that is entered from the keyboard is a String. To convert them to numbers use:
int num = Integer.parseInt("123");
double num = Double.parseDouble("123.99");
float num = Float.parseFloat("123.99");

ArrayList
Connect Java API:
import java.util.*;
Create an ArrayList:
ArrayList<Type> myList = new ArrayList<Type>();
Put something in it:
Egg eggOne = new Egg();
myList.add(eggOne);
Put another thing in it:
Egg eggTwo = new Egg();
myList.add(eggTwo);
Find out how many things are in it:
int theSize= myList.size();
Find out if it contains something:
boolean isIn = myList.contains(eggTwo);
Find out where something is (i.e. its index)
int index = myList.indexOf(eggOne);
Find out if it’s empty
boolean empty = myList.isEmpty();
Remove something from it
myList.remove(eggTwo);
Get an item from it
Egg anEgg = (Egg)myList.get(1);  // will get the second item in the ArrayList

Inheritance
Place the common code in a common class. This common class in known as a superclass. Next, we create a class that uses the common code in the superclass. A class that does this is called a subclass. Subclasses inherit instance variables and methods from their superclasses. A subclass can add its own variables and methods. When a subclass has a method with the same header as the superclass then it is called an override. The subclass overrides the method in the superclass.
To invoke the superclass version of a method from a subclass that’s overridden the method, use the super keyword.

Polymorphism
Polymorphism – Determining object behavior based on the actual type instead of the calling type.
Animal myDog = new Dog();
In Java we can force programmers to not instantiate certain classes by using the new keyword abstract. An abstract class has only one purpose, to be subclassed. This allows us to have some common code that only makes sense in a subclass. 
public abstract class Animal { }
Abstract methods are declared without a body and without any curly braces. Abstract methods have only one purpose, to force subclasses to have this method.
public abstract void eat();

Interfaces
An interface is like a contract, you are telling the compiler that you will have certain methods. The compiler will then enforce the contract! An interface is like a class. You create a file with a .java extension. You add code that looks a lot like a class. And you add methods that are just abstract methods like in an abstract class.
public interface Pet { 
    public abstract void beFriendly();    
    public abstract void play();
A class can implement an interface. In fact, it can implement as many interfaces as you want.
public class Dog extends Canine implements Pet {
    public void beFriendly() {...} 
    public void play() {...}
}  
Now we can do the following:
Canine myDog = new Dog();
Pet myDog = new Dog();

Code Release
The entire library is in a directory structure for clarity and organization. This is called packaging in Java and each individual directory in the hierarchy is called a package. Add the package statement to the top of a .java file:
package java111.project5;
The src directory will be where all the .java files are kept. The classes directory will get the .class files.
To automate this we will use the -d flag on the compiler. This compiler flag tells the compiler where to put the .class files that it is about to create. It goes right after the javac statement. After those arguments we have to add the path to the files we want to compile and the files themselves:
	javac -classpath classes -d classes src/java111/project5/*.java
Here’s the full script to run a packaged class:
	java -classpath classes java111.project5.PackageExercise

Constructors
Constructors are similar to methods but they aren’t methods. All classes have at least one constructor and if you don’t write one the compiler does. 
public class Duck {  
    public Duck() {
        System.out.println("Quack");
    }
}
Colling a constructor:
Duck duck = new Duck();
If we make a constructor with a parameter then the compiler does not make one for us without any parameters!
Having more than one constructor in a class means you have overloaded constructor.

Static Methods
Static methods can’t access anything that is not also static. They are like global methods that are used without objects. To make a static method you add the word static to the method declaration:
public static void myStaticMethod() {...}

Static Variables
Static variables are like instance variables that all objects of that class share.
int static duckCount;

Constants
Constants have keyword final that can be added to classes, methods, and instance variables.
public static final int WEEKS_IN_SEASON = 20;
If you add final to a method it means that the method can’t be overridden.
public final void doMyCoolThing() {...}
If you add final to a class then you can’t subclass the class. There are lots of classes in Java like this. Just try to subclass the String class!

Generating Javadoc
The Javadoc utility comes with Java. It is a command line tool that is run like java or javac. To generate your Javadoc use these steps: Use the cd command to navigate to your projects directory. Copy and paste this command to the command line and run it:
javadoc -d docs -private -sourcepath src java111.project5 java111.project5.labs

Timestamp and Calendar
For a time-stamp of current time, use import java.util.Date:
   Date today = new Date();
   String s = String.format("%tA, %<tB %<td", today);
For everything else, use import java.util.Calendar:
   Calendar c = Calendar.getInstance();
   c.set(2004,0,7,15,40);
   System.out.println(c.getTime());
Here we are getting an instance of the abstract class Calendar that is represented by GeorgianCalendar concrete class. Then, we set time to January (0) 7th of 2004, 15:40, and displaying the result. There are many different methods to operate with Calendar objects. Check API.

Wrapping a primitive
Wrap primitive to treat it as an object. A wrapper class is named after each primitive type it wraps, but with first letter capitalized: Boolean, Character (not Char as you would think!), Byte, Short, Integer (not Int!), Long, Float, Double. 
wrapping value:
int i = 288;
Integer iWrap = new Integer(i);   <- send the primitive to the wrapper constructor
unwrapping a value:
int unWrapped = iWrap.intValue();   <- boolean has booleanValue(), Character has a charValue(), etc.
After Java 5.0 autoboxing is converts primitive to objects automatically!
Now you can do:
ArrayList<Integer> listOfNumbers = new ArrayList<Integer>();
listOfNumbers.add(3);  <- you can add ints or Intergers 
int = listOfNumbers.get(0);  

Exception Handling
An exception is an object of type Exception.
The simplest block:
try {
…
} catch(Exception ex){   <- ex is an argument of type “Exception”
…
}
 
Exception throwing code:
public void takeRisk() throws BadException {
  if (abandonAllHope) {
    throw new BadException();   <-creates a new BadException object and throws it.
  }
}

Call that risky method:
public void crossFingers() {
  try {
    anObject.takeRisk();
  } catch(BadException ex) {
    System.ou.println(“Ah!”);
    ex.printStackTrace();    <- all exceptions inherit this method
  }
}
The compile checks for everything except RuntimeException. They are called “Unchecked Expressions”. Most of them comes from your code logic, so the compiler does not check for them!

The block with part that runs no-matter what:
try {
  turnOvenOn();
  x.bake();
} catch (BakingException ex) {
  Ex.printStackTrace();
} finally {
  turnOvenOff();   <- do this even if we caught an exception.
}
Throw multiple exceptions:
public class Laundry {
  public void doLaundry() throws PantsExcseption, LingerieException {
    // code that could throw either exception
  }
}
Catching multiple exceptions:
public class Foo {
  puplic void go() {
    Laundry laundry = new Laundry();
    try {
      Laundry.doLaundry();
    } catch (PantsException pex) {
      // recovery code
    } catch (LingerieException lex) {
      // recovery code
    }
  }
}
Multiple catch blocks must be ordered from smallest to biggest.
When you don’t want to handle an exception, just duck it by declaring it again:
void foo() throws ClothingException {
  laundty.doLaundry();
}   <-Now who ever calls foo() will have to handle the exception


GUI
Use javax.swing package to apply GUI. 
This is a simplest code that engages GUI:
import javax.swing.*; // Swing package for creating GUI
import java.awt.event.*; // This package has ActionListener and ActionEvent
// Make a class
public class SimpleGui1 implements ActionListener { 
  // Declare a global variable "button"
  JButton button;
  public static void main(String[] args) {
    // Create an object SimpleGui1
	SimpleGui1 gui = new SimpleGui1();	
	// Run the program
	gui.go();
  }
  // The program lives here:
  public void go() { 
	// Make a frame
	JFrame frame = new JFrame();	
	// Make a button
	button = new JButton("click me");	
	// Add the interface to the button's list of listeners
	// Pass the argument that is an object from a class that implements ActionListener.
	button.addActionListener(this);
	// Make the program quit as soon as we close the window
	frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	// Add the button to the frame's content pane
	frame.getContentPane().add(button);
	// Give the frame a size in pixels
	frame.setSize(300,300);
	// Make the frame visible
	frame.setVisible(true);	
  } 
  // Implement the ActionListener interface's actionPerformed() method.
  // This is the actual event-handling method.
  // The button calls this method to let us know an event happened.
  // It sends us an ActionEvent object as the argument, but we don't need it here.
  public void actionPerformed(ActionEvent event) {
    button.setText("I've been clicked!");
  }
}

Event listener implements the interface, registers with the button, and provide the event-handling.
Event source accepts registrations from listeners, gets events from the user and calls the listener’s event-handling method when the user clicks the button.
Event object holds data about the event.

Three ways to put things on GUI:
Put widgets on a frame. (Use javax.swing API)
Frame.getContentPane().add(myButton); 
Draw 2D graphics on a widget using graphics objects to paint shapes. (Use Java2D API)
Graphics. fillOval(70,70,100,100);
Put a JPEG on a widget:
Graphics.drawImage(myPic,10,10,this);

Use of paintComponent() to display a shape:
import java.awt.*;
import javax.swing.*;
// Creating graphics for GUI
// This is a subclass of JPanel to make a customize widget
class MyDrawPanel extends JPanel {
  // This is the important Graphic method.
  // The system calls it.
  public void paintComponent(Graphics g) { 
    // "g" is like a painting machine. Tell it what ot paint with coordinates and size
    g.setColor(Color.orange);
	g.fillRect(20,50,100,100);
  }
}

Use paintComponent() to display an image:
public void paintComponent(Graphics g) {
  image image = new ImageIcon(“cat.jpg”).getImage();
  d.drawImage(image,3,4,this); // 3pix from the left and 4 pix from the top
}

Inner Class
Inner class is nested within another class:
class MyOuterClass {
  class MyInnerClass {
      Void go() { }
  }
}
An instance of an Inner class can use all variables and methods of the outer class, even private ones, but an inner object must be tied to a specific outer object on the heap. They are linked.
class MyOuter {
  private int x;
  MyInner = new MyInner();
  public void doSuff() {
    inner.go();
  }
  class MyInner {
    void go() {
      x = 42;
    }
  }
}
It is also possible to call an inner class from outside of outer class.

STATIC INNER CLASS
Static means tied to the class, not to a particular instance. 
Public class FooOuter {
  Static class BarInner {
    Void sayIt() {
      System.out.println(‘method of a static inner class”);
    }
  }
}
You call it like this:
Public Test {
  Public static void main (String[] args) {
    FooOuter.BarInner foo = new FooOuter.BarInner(); // Don’t use instance of the outer class
    Foo.sayIt();
  }
}
Inner static class can get access to any static members of outer class.

ANONYMOUS INNER CLASS
Create an instance on the fly:
  Public static void main (String[] args) {
    JFrame frame = new JFrame();
    JButton = new JButton(“click”);
    Frame.getContentPane().add(button);
      // button.addActionListener(quitListener); //normally we would use an instance of an inner class, but…
    Button.addActionListener(new ActionListener() { // We create an anonymous class
      Public void actionPerformed(ActionEvent ev) {
        System.exit(0);
      }
     });
   }
  
Saving Objects
If your data will be used by only the Java program that generated it, use serialization.
If your data will be used by other programs, write a plain text file. 
Writing a serialized object to a file (p.432/Head First Java):
FileOutputStream fileStream = new FileOutputStream(“MyGame.ser”); 
ObjectOutputStream os = new ObjectOutputStream(fileStream);
os.writeObject(characterOne);
os.close();

SERIALIZATION
Serialization saves the entire object graph. All objects referenced by instance variables, starting with the object serialized. If you want your class to be serializable, implement Serializable.
import java.io.* // need to implement Serializable
public class Box implements Serializable {…
Mark and instance as transient if it cannot be saved:
Class Chat implements Serializable {
  transient String currentID; // this will be skipped during serialization

DESERIALIZATION
Deserialize an object (p.441/Head First Java):
FileInputStream fileStream = new FileInputStream(“MyGame.ser”);
ObjectInputStream os = new ObjectInputStream(fileStream);
Object one = os.readObject();
GameCharacter elf = (GameCharacter) one;
os.close();

LINKED INVOCATIONS
StringBuffer sb = new StringBuffer(“spring”);
sb = sb.delete(3,6).insert(2,”umme”).deleteCharAt(1);
System.out.println(“sb = “ +sb);
// result is sb = summer
First, find the result in the leftmost call sb.delete(3,6) which will give the result as “spr”, and so on.
Same as:
sb = sb.delete(3,6);
sb = sb.insert(2,”umme”);
sb = sb.deleteCharAt(1);
Another option:
Class Foo {
  public static void main(String[] args) {
    new Foo().go(); // We do not care about instantiating Foo!
  }
  void go() {
    // do something
  }
}


