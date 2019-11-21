## Object Oriented JavaScript

#### Creating an object
There are two ways to create a JavaScript object: they are 'Constructor functions' and 'Literal notation'.
```javascript
//Constructor notation
function myObject(){
 ...
};

//Literal notation
var myObject = {
 ...
};
```
Literal is a preferred option if you are using this object as a single object and not requiring more than one instance of the object, whereas Constructor function type notation is preferred if you need to do some initial work before the object is created or require multiple instances of the object where each instance can be changed during the lifetime of the script.

#### Defining Methods and Properties
```javascript
// Constructor version
function myObject(){
    this.iAm = 'an object';
    this.whatAmI = function(){
        alert('I am ' + this.iAm);
    };
};

//Literal version:
var myObject = {
    iAm : 'an object',
    whatAmI : function(){
        alert('I am ' + this.iAm);
    }
}
```
For each of the objects we have created a property 'iAm' which contains a string value that is used in our objects method 'whatAmI' which alerts a message. To execute the method, as with any function, you must put parenthesis after it; otherwise you will just be returning a reference to the function and not what the function actually returns.

#### Using an object
To use a literally notated object, you simply use it by referencing its variable name, so wherever it is required you call it by typing:
```javascript
myObject.whatAmI();
```
With constructor functions you need to instantiate (create a new instance of) the object first; you do this by typing:
```javascript
var myNewObject = new myObject();
myNewObject.whatAmI();
```

#### Using a Constructor Function
Let's use our previous constructor function and build upon it so it performs some basic (but dynamic) operations when we instantiate it.
```javascript
function myObject(){
    this.iAm = 'an object';
    this.whatAmI = function(){
        alert('I am ' + this.iAm);
    };
};
```
Just like any JavaScript function, we can use arguments with our constructor function:
```javascript
function myObject(what){
    this.iAm = what;
    this.whatAmI = function(language){
        alert('I am ' + this.iAm + ' of the ' + language + ' language');
    };
};
```
Now let's instantiate our object and call its whatAmI method, filling in the required fields as we do so.
```javascript
var myNewObject = new myObject('an object');
myNewObject.whatAmI('JavaScript');  // This will alert 'I am an object of the JavaScript language.'
```
When a change is made to an Object Literal it affects that object across the entire script, whereas when a Constructor function is instantiated and then a change is made to that instance, it won't affect any other instances of that object.
```javascript
//LITERAL
var myObjectLiteral = {
    myProperty : 'this is a property'
}
 
//alert current myProperty
alert(myObjectLiteral.myProperty); //this will alert 'this is a property'
 
//change myProperty
myObjectLiteral.myProperty = 'this is a new property';
 
//alert current myProperty
alert(myObjectLiteral.myProperty); //this will alert 'this is a new property', as expected


// CONSTRUCTOR
var myObjectConstructor = function(){
    this.myProperty = 'this is a property'
}
 
//instantiate our Constructor
var constructorOne = new myObjectConstructor();
 
//change myProperty of the first instance
constructorOne.myProperty = 'this is a new property';
 
//instantiate a second instance of our Constructor
var constructorTwo = new myObjectConstructor();
 
//alert current myProperty of constructorOne instance
alert(constructorOne.myProperty); //this will alert 'this is a new property'
  
 //alert current myProperty of constructorTwo instance
alert(constructorTwo.myProperty); //this will still alert 'this is a property'
```

#### Scope
Scope in JavaScript is function/object based, so that means if you're outside of a function, you can't use a variable that is defined inside a function (unless you use a closure). There is however a scope chain, which means that a function inside another function can access a variable defined in its parent function.

In a browser, 'this' references the `window` object, so technically the `window` is our global object. If we're inside an object, `this` will refer to the object itself however if you're inside a function, `this` will still refer to the window object and likewise if you're inside a method that is within an object, `this` will refer to the object.

Due to our scope chain, if we're inside a sub-object (an object inside an object), `this` will refer to the sub-object and not the parent object.

When using functions like `setInterval`, `setTimeout` and `eval`, when you execute a function or method via one of these, `this` refers to the `window` object as these are methods of `window`, so `setInterval()` and `window.setInterval()` are the same.

#### Real World Example
Create a form validation object. Create a new function with three arguments, to being the DOM object we are attaching the event to, type being the type of event and fn being the function run when the event is triggered.
```javascript
function addEvent(to, type, fn){
    if(document.addEventListener){
        to.addEventListener(type, fn, false);
    } else if(document.attachEvent){
        to.attachEvent('on'+type, fn);
    } else {
        to['on'+type] = fn;
    }   
};
```
Create a jQuery launcher:
```javascript
$(document).ready(function(){
    //all our code that runs after the page is ready goes here
});
```
Using our addEvent function we have:
```javascript
addEvent(window, 'load', function(){
    //all our code that runs after the page is ready goes here
});
```
Form object.
```javascript
var Form = {
    validClass : 'valid',
     
    fname : {
        minLength : 1,      
        maxLength : 15, 
        fieldName : 'First Name'
    },
     
    lname : {
        minLength : 1,      
        maxLength : 25,
        fieldName : 'Last Name'
    },
     
    validateLength : function(formEl, type){
        if(formEl.value.length > type.maxLength || formEl.value.length < type.minLength ){    
            formEl.className = formEl.className.replace(' '+Form.validClass, '');
            return false;
        } else {
            if(formEl.className.indexOf(' '+Form.validClass) == -1)
            formEl.className += ' '+Form.validClass;
            return true;
        }
    },
     
    validateEmail : function(formEl){
        var regEx = /^([0-9a-zA-Z]([-.\w]*[0-9a-zA-Z])*@([0-9a-zA-Z][-\w]*[0-9a-zA-Z]\.)+[a-zA-Z]{2,9})$/;
        var emailTest = regEx.test(formEl.value);        
        if (emailTest) {
            if(formEl.className.indexOf(' '+Form.validClass) == -1)         
            formEl.className += ' '+Form.validClass;            
            return true;
        } else {
            formEl.className = formEl.className.replace(' '+Form.validClass, '');
            return false;
        }           
    },      
     
    getSubmit : function(formID){    
        var inputs = document.getElementById(formID).getElementsByTagName('input');
        for(var i = 0; i < inputs.length; i++){
            if(inputs[i].type == 'submit'){
                return inputs[i];
            }       
        }       
        return false;
    }           
         
};
```
HTML form
```html
<form id="ourForm">
    <label>First Name</label><input type="text" /><br />
    <label>Last Name</label><input type="text" /><br />
    <label>Email</label><input type="text" /><br />
    <input type="submit" value="submit" />
</form>
```
Access these input objects using JavaScript and validate them when the form submits:
```javascript
addEvent(window, 'load', function(){
     
    var ourForm = document.getElementById('ourForm');   
    var submit_button = Form.getSubmit('ourForm');
    submit_button.disabled = 'disabled';
     
    function checkForm(){
        var inputs = ourForm.getElementsByTagName('input');
        if(Form.validateLength(inputs[0], Form.fname)){
            if(Form.validateLength(inputs[1], Form.lname)){
                if(Form.validateEmail(inputs[2])){                   
                        submit_button.disabled = false;
                        return true;
                }
            }
        }
             
        submit_button.disabled = 'disabled';
        return false;
         
    };
     
    checkForm();        
    addEvent(ourForm, 'keyup', checkForm);
    addEvent(ourForm, 'submit', checkForm);
       
});
```
