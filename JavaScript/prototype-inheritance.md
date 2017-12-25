## Prototypal Inheritance
Create a parent class:
```javascript
// Person constructor
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

// Create a prototype function Greeting for the parent class
Person.prototype.greeting = function(){
  return `Hello there ${this.firstName} ${this.lastName}`;
}

const person1 = new Person('John', 'Doe');
console.log(person1.greeting());
```
Create a child class:
```javascript
// Customer constructor
function Customer(firstName, lastName, phone, membership) {

  // Call a prototype properties from the parent class
  Person.call(this, firstName, lastName);

  this.phone = phone;
  this.membership = membership;
}
```
Inherit Person (parent) prototype methods:
```javascript
Customer.prototype = Object.create(Person.prototype);

// Make customer.prototype return Customer()
Customer.prototype.constructor = Customer;

// Create customer
const customer1 = new Customer('Tom', 'Smith', '555-555-5555', 'Standard');
console.log(customer1);
```
Create a prototype funcion for Customer (child) which is unique to the Customer:
```javascript
// Customer greeting
Customer.prototype.greeting = function(){
  return `Hello there ${this.firstName} ${this.lastName} welcome to our company`;
}
```
