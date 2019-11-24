## call(), apply() and bind()
*call()* and *apply()* are useful when you need to borrow a method from another object:
```js
const wizard = {
  name: 'Merlin',
  health: 100,
  heal: function(num1, num2) {
    this.health += num1 + num2;
  }
}

const archer = {
  name: 'Robin Hood',
  health: 50
  // we want to borrow heal method from wizard!
}

wizard.heal.call(archer, 50, 60)
wizard.heal.apply(archer, [20, 30])
```
- *call()* takes the first argument as the object two which the borrowed method needs to be applied and executes right away. The other
arguments can be any arguments to pass with the method.
- *apply()* does the same, except the second argument is an array of the method arguments.

*call()* and *apply()* executes right away:
```js
myFunc() is the same as myFunc.call()
```

- *bind()* creates a function that can be used later with the proper *this* keyword:
```js
const wizard = {
  name: 'Merlin',
  health: 100,
  heal: function(num1, num2) {
    this.health += num1 + num2;
  }
}

const archer = {
  name: 'Robin Hood',
  health: 50
}

const healArcher = wizard.heal.bind(archer, 50, 60);
console.log(archer)
healArcher()
console.log(archer)
```
*bind()* takes other arguments after the first, which is the object that borrows the method.
