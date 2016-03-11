## Recursive Functions
Recursion is a programming concept. It is not unique to JavaScript, but is used in all languages. It is not a data type, like string or float. It is not a function, object, or method. It is not constrained by a single statement call like `if` or `while`.

Recursion is one of the most deceptively simple programming concepts. In programming, factorials are a perfect example of a case when a recursive function should be used. When you take the factorial of a number, you multiply that number by each number between itself and one. So the factorial of 5 is equal to 5 * 4 * 3 * 2 * 1, or 120.
```javascript
function factorial(n) {
  if (n === 0) {
    return 1;
  }
  // Recursion:
  return n * factorial(n - 1);
}

factorial(10);
```

There are a few key features of recursion that must be included in order for it to work properly.
* The first is a **base case**: this is a statement, usually within a conditional clause like `if`, that stops the recursion. If you don't have a base case, the recursion will go on infinitely and your program will crash.
* The second is a **recursive case**: this is the statement where the recursion actually happens: where the recursive function is called on itself:
```javascript
function factorial(n) {  
  // This is Base Case - when n is equal to 0, we stop the recursion
  if (n === 0) {
    return 1;
  }
  
  // This is Recursive Case
  // It will run for all other conditions except when n is equal to 0
  return n * factorial(n - 1);
}
```

#### Termination Condition
One other useful (and often necessary) feature of a recursive function is a termination condition. This is a specific statement that will explicitly stop the recursion. The base case is a form of termination condition. 
```javascript
function factorial(n) {
  // Termination condition to prevent infinite recursion:
  if (n < 0) {
    console.log("negative numbers are not allowed");
    return;
  }
  // Base case:
  if (n === 0) {
    return 1;
  }
  // Recursive case:
  return n * factorial(n -1);
}

factorial(-1);
factorial(5);
```
What would happen if we called it on a negative integer? Since the recursion will only stop when n is equal to 0, and that would never happen with a negative integer, our program would crash. In order to protect against this, we use a termination condition to ensure that the value passed to the function is valid, and will not crash our program.

When building your recursive case (the code that will be repeated), one of the rules of thumb is to ensure that the arguments you use for the recursion will lead to your base case. If the value we pass to the recursive function call is the same as the initial value, chances are our code will enter an infinite loop.

Many programming languages don't have loops like `for` or `while`, but use recursion for everything. In this example, each function does the same thing. One uses a loop, the other uses recursion:
```javascript
function loopFactorial(n) {
  var result = n;
  while (n > 1) {
    result = result * (n-1);
    n--;
  }
  return result;
}

function recursiveFactorial(n) {
  if (n < 0) {
    return console.log("Must be a positive integer.");
  }
  else if (n === 0) {
    return 1;
  }
  return n * recursiveFactorial(n - 1);
}

var loopResult = loopFactorial(3) // Call the function loopFactorial(n)
var recursiveResult = recursiveFactorial(3)// Call the function recursiveFactorial(n)

console.log("The loop function returned: " + loopResult);
console.log("The recursive function returned: " + recursiveResult);
```
Another example:
```javascript
function guessNumber(number) {
  // Prompt the user for a number
  guess = prompt("Guess a number between 1 and 100");
  // Convert their guess to a number using +
    guess = +guess;
  // Define base case
  if (guess === number) {
	return console.log("You got it! The number was " + number);
  }
  // Define recursive case with a function call
  guessNumber(number);
}

// Call the function guessNumber() with an integer for an argument
guessNumber(67);
```
An example with **Fibonacci sequence**. By definition, the first two numbers in the Fibonacci sequence are either 1 and 1, or 0 and 1, depending on the chosen starting point of the sequence, and each subsequent number is the sum of the previous two: (0,1,1,3,5,8,13,...)
```javascript
function growBeanstalk(years) {
  // Base case
  if (years <= 2) {
    return 1;
  }	
  // Recursive case
  return growBeanstalk(years - 1) + growBeanstalk(years - 2);	
}
// Set the height of the beanstalk using your function
var height = growBeanstalk(10);
console.log(height);
```
