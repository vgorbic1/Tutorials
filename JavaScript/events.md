## Events
Events are happen when:
- an element is clicked on
- the page is loaded
- input fields are changed

#### Inline Event Handling (one and old way)

This is a traditional way to handle events. You are writing JavaScript on HTML page, which is not always good. If it is already on the page, do not refactor.
```javascript
// HTML
iPhone <input type="button" value="add to cart" onclick="addToCart('iPhone');" />
iPad <input type="button" value="add to cart" onclick="addToCart('iPhone');" />

// JavaScript
function addToCart(product) {
    // We cannot use 'this' keyword. It is useless here.
    console.log(product + ' added to cart');
}
```
If you already have inline event and want to add extra functionality, you may do the following:
```javascript
// HTML
<input type="button" id="btn" value="click me" onclick="console.log('first event');" />
<script>init();</script>  // put after </html>

// JavaScript file
function init() {
    var btn = document.getElementById('btn');
    var inlineEvent = btn.onclick;  // assign inline event from HTML file
    btn.onclick = function() {
        inlineEvent();  // trigger the inline event from HTML file
        console.log('second event'); // trigger additional functionality with the same click
    }
}
```
#### Dot-notation Invent Handling (another way to do it)

Remove all JavaScript from your HTML and use *this* keyword as a point of reference.
```javascript
// HTML
<input type="button" id="iPhone" value="iPhone" />
<input type="button" id="iPad" value="iPad" />

// JavaScript
function init() {
    var btn1 = document.getElementById('iPhone');
    var btn2 = document.getElementById('iPad');
    btn1.onclick = addToShoppingCart;
    btn2.onclick = addToShoppingCart;
}

function addToShoppingCart() {
    // Now we can use 'this' keyword to access any element on the page  
    console.log(this.value);  // gets the button text
}
```

#### Using Event Listener (still another way)

Add another (custom) event and attache it with *addEventListener()* function. Old IE browsers do not have this function, so you need to use a feature detection with *if* statement:
```javascript
// HTML
<input type="button" id="iPhone" value="iPhone" />
<input type="button" id="iPad" value="iPad" />

// JavaScript
function init() {
    var btn1 = document.getElementById('iPhone');
    var btn2 = document.getElementById('iPad');
    btn1.onclick = addToShoppingCart;
    btn2.onclick = addToShoppingCart;
	
    // adding additional event to onclick event defined earlier
    if (window.addEventListener) {  // if browser recognizes this function
        btn1.addEventListener('click', eventListenerEvent, false);
        btn2.addEventListener('click', eventListenerEvent, false);
    } else {
        btn1.attachEvent('onclick', eventListenerEvent);  // old IEs use this attacheEvent() function!
        btn2.attachEvent('onclick', eventListenerEvent);
    }
}

function eventListenerEvent() {
    // standards compliant event handling
    var control;  // Create a var to handle control in both IE and other browsers
    if (window.event) {  // If this property exists, we are using old version of IE
        control = window.event.srcElement;  // we cannot use 'this' keyword 
    } else {  // if not, all other browsers
        control = this;  // we can use 'this' keyword
    }
    console.log('standards compliant event ' + this.value);
}
```

#### onclick
```javascript
<h1 id="header">Header</h1>
<input type="button" onclick="document.getElementById('header').style.color = 'red'" />
```
To call the function from a script:
```javascript
<h1 onclick="changeThisHeader(this)">Header</h1>

function changeThisHeader(id) {
  id.innerHTML = 'Another Header';
}
```
To assign an event using DOM:
```javascript
document.getElementById('button').onclick = function() { displayDate() };
```

#### onload
This event works when user eters the page. It is usually used to check user browser's type or version, as well as whether cookies are disabled.
```javascript
<body onload="checkCookie()">
```
#### onunload
This event works when user leaves the page.

#### onchange
This event is often used in combination with validation of input fields.
```javascript
<input type="text" onchange="upperCase()" />
```

