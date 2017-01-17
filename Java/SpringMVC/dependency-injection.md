## Dependency Injection
Many people use the terms dependency injection and Inversion of Control (IoC) interchangeably.

You have two compolnents, A and B, and A depends on B:
```java
public class A {
  public void method() {
    B b = new B();
    b.method();
}
```
A must obtain an instance of B before it can use B. It can be problematic if B is an interface with many implementations.
You will have to choose an implementation of B and by doing so you reduce the reusability of A because you cannot
use A with the implementations of B that you did not choose.

Dependency injection takes over object creation and injects dipendencies to an object that needs them. Framework would create
an instance of A and instance of B and inject the latter to the former. For this you need to create a **set** method or a special constructor in the target class:
```java
public class A {
  private B b;
  public void method() {
    b.method();
  }
  public void setB(B b) {
    this.b = b;
  }
}
```
or
```java
public class A {
  private B b;
  public A(B b) {
    this.b = b;
  }
  public void method() {
    b.method();
  }
}
````

#### Setter-based Dependency Injection in Spring
Employee class
```java
package app01a.bean;

public class Employee {
	private String firstName;
	private String lastName;
	private Address homeAddress;

	public Employee() {
	}

	public Employee(String firstName, String lastName, Address homeAddress) {
		super();
		this.firstName = firstName;
		this.lastName = lastName;
		this.homeAddress = homeAddress;
	}

	public String getFirstName() {
		return firstName;
	}

	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}

	public String getLastName() {
		return lastName;
	}

	public void setLastName(String lastName) {
		this.lastName = lastName;
	}

	public Address getHomeAddress() {
		return homeAddress;
	}

	public void setHomeAddress(Address homeAddress) {
		this.homeAddress = homeAddress;
	}

	@Override
	public String toString() {
		return firstName + " " + lastName + "\n" + homeAddress;
	}

}
```
The Address class
```java
package app01a.bean;

public class Address {
	private String line1;
	private String line2;
	private String city;
	private String state;
	private String zipCode;
	private String country;

	public Address(String line1, String line2, String city, String state,
			String zipCode, String country) {
		super();
		this.line1 = line1;
		this.line2 = line2;
		this.city = city;
		this.state = state;
		this.zipCode = zipCode;
		this.country = country;
	}

	public String getLine1() {
		return line1;
	}

	public void setLine1(String line1) {
		this.line1 = line1;
	}

	public String getLine2() {
		return line2;
	}

	public void setLine2(String line2) {
		this.line2 = line2;
	}

	public String getCity() {
		return city;
	}

	public void setCity(String city) {
		this.city = city;
	}

	public String getState() {
		return state;
	}

	public void setState(String state) {
		this.state = state;
	}

	public String getZipCode() {
		return zipCode;
	}

	public void setZipCode(String zipCode) {
		this.zipCode = zipCode;
	}

	public String getCountry() {
		return country;
	}

	public void setCountry(String country) {
		this.country = country;
	}

	@Override
	public String toString() {
		return line1 + "\n" + line2 + "\n"
				+ city + "\n" + state + "\n" + zipCode
				+ "\n" + country;
	}

	
}
```
Employee depends on Address. To make sure that every Employee instance contains an instance of Address, you can configure
Spring  with these two bean elements:
```xml
    <bean name="simpleAddress" class="app01a.bean.Address" >
      <constructor-arg name="line1" value="151 Corner Street" />
      <constructor-arg name="line2" value="" />
      <constructor-arg name="city" value="Albany" />
      <constructor-arg name="state" value="NY" />
      <constructor-arg name="zipCode" value="12345" />
      <constructor-arg name="country" value="US" />
    </bean>
    
    <bean name="employee1" class="app01a.bean.Employee">
      <property name="homeAddress" ref="simpleAddress" />
      <property name="firstName" value="Junior" />
      <property name="lastName" value="Moore" />
    </bean>
 ```
 The simpleAddress bean instantiates Address and passes values to its constructor. The employee1 bean uses property
 elements to inject values to its setter methods. The homeAddress property is given the reference of simpleAddress.
 The order of bean declarations is not important.
 
 #### Constructor-based Dependency Injection
 Since the Employee class above provides a constructor that can take values, we can inject Address to an instance
 of Employee through its constructor:
 ```xml
     <bean name="simpleAddress" class="app01a.bean.Address" >
      <constructor-arg name="line1" value="151 Corner Street" />
      <constructor-arg name="line2" value="" />
      <constructor-arg name="city" value="Albany" />
      <constructor-arg name="state" value="NY" />
      <constructor-arg name="zipCode" value="12345" />
      <constructor-arg name="country" value="US" />
    </bean>
    
    <bean name="employee2" class="app01a.bean.Employee">
      <constructor-arg name="homeAddress" ref="simpleAddress" />
      <constructor-arg name="firstName" value="Junior" />
      <constructor-arg name="lastName" value="Moore" />
    </bean>
 ```
