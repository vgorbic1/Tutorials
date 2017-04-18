## Builder Design Pattern
The Builder pattern is one of most popular Object Oriented Design Patterns.
It is used for creating object instances, when dealing with classes that have
large number of constructor arguments.

For example, you have an Employee class:
```java
public Employee {
	private String firstName;
	private String lastName;
	private String phone;
	private int age;
}
```
*Goal:* Create an object of Employee class with only firstName and lastName fields.

*Possible Solution*: Create a constructor and pass only firstName and lastName arguments:
```java
    public Employee(firstName, lastName) {
	    this.firstName = firstName;
		this.lastName = lastName;
    }
```
Now, the goal was changed to create an object of Employee class with firstName, lastName
and the employee's age.

*Possible Solution*: Create another constructor that overloads the initial one 
and accepts all three attributes:
```java
    public Employee(firstName, lastName) {
	    this.firstName = firstName;
		this.lastName = lastName;
    }
	
	public Employee(firstName, lastName, age) {
	    this.firstName = firstName;
		this.lastName = lastName;
		this.age = age;
    }
```
Now, how about to add all four attributes? A third construction has to be set, proving
that our approach is not effective. This is known as "Telescoping Constructor 
Anti-pattern".

*Another Possible Solution*: Create getters and setters for each attribute. All this
fields can be set when we create an object of the Employee class. But this is not
a thread safe solution. The state of this object is changing from one line to the
other.

*Best approach* is to use the Build Pattern:
```java
public class Employee {
	private String firstName;
	private String lastName;
	private String phone;
	private int age;

	// Define a private! constructor and provide a Builder object as a
	// parameter.
	// Set only those fields to Employee object, that were passed with the
	// builder object of inner Builder class.
	private Employee(Builder builder) {
		this.firstName = builder.firstName;
		this.lastName = builder.lastName;
		this.phone = builder.phone;
		this.age = builder.age;
	}

	@Override
	public String toString() {
		return "Employee [firstName=" + firstName + ", lastName=" + 
				lastName + ", phone=" + phone + ", age=" + age + "]";
	}

	// Create a nested class that has the same fields as the outer class.
	public static class Builder {
		private String firstName;
		private String lastName;
		private String phone;
		private int age;

		// This method returns an instance of this inner class.
		public Employee build() {
			return new Employee(this);
		}

		public Builder firstName(String value) {
			this.firstName = value;
			return this;
		}
		
		public Builder lastName(String value) {
			this.lastName = value;
			return this;
		}
		
		public Builder phone(String value) {
			this.phone = value;
			return this;
		}
		
		public Builder age(int value) {
			this.age = value;
			return this;
		}

	}
}
```
Create any instance of the Employee class:
```java
public static void main(String[] args) {
	Employee employee = new Employee.Builder()
		.firstName("James").build();
	System.out.println(employee);
}

// or

public static void main(String[] args) {
	Employee employee = new Employee.Builder()
		.firstName("James")
		.lastName("Bond").build();
	System.out.println(employee);
}

// or 

public static void main(String[] args) {
	Employee employee = new Employee.Builder()
		.firstName("James")
		.lastName("Bond")
		.phone("007").build();
	System.out.println(employee);
}
	
// or 

public static void main(String[] args) {
	Employee employee = new Employee.Builder()
		.firstName("James")
		.lastName("Bond")
		.phone("007")
		.age(55).build();
	System.out.println(employee);
}
```
Note, that the order of methods that set the fields is not important.
