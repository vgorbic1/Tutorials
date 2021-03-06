##Abstract Classes
- Use an abstract class when you want to define a TEMPLATE for a group of subclasses. 
- Use intrface when you want to define a ROLE that other classes can play, regardless of where those classes are in the inheritance tree.

When you don't want a class to be instantiated (in other words, you don't want anyone to make a new object of that class type) mark the class with the ```abstract``` keyword.

Abstract classes are placeholders for actual implementation classes. The abstract class defines behavior, and the subclasses implement that behavior.
```java
public abstract class Instrument {
	private String serialNumber;
	private double price;

	// Constructor
	public Instrument(String serialNumber, double price) {
		this.serialNumber = serialNumber;
		this.price = price;
	}

	// Getters and Setters
	public getInstrumentPrice(Double price) {
		this.price = price;
	}

	public setInstrumentPrice() {
		return price;
	}

}
```
The subclass will get the common properties and define their own constructors with the right type of spec class:
```java
public class Guitar extends Instrument {

	// Constructor
	public Guitar(String serialNumber, double price) {
		super(serialNumber, price);
	}

}
```
If the subclass has its own property:
```java
public class Guitar extends Instrument {
	private int numOfStrings;

	// Constructor
	public Guitar(String serialNumber, double price, int numOfStrings) {
		super(serialNumber, price);
		this.numOfStrings = numOfStrings;	
	}

	public getNumOfStrings() {
		return numOfStrings;
	}

}
```
