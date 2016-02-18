##Abstract Classes
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

public class Guitar extends Instrument {

	// Constructor
public Guitar(String serialNumber, double price) {
	super(serialNumber, price);
}

}

If the subclass has its own property:

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
