## Form Validation Demo
This form validation consists of four different functions:

- `emailvalidation(this, text)` will check to see if a value lives up to the general syntax of an email.
- `valuevalidation(this, min, max, text ,type)` will check to see if a value is within a certain interval.
- `digitvalidation(this, min, max, text, type)` will check to see if a value consits of a certain number of digits. 
- `emptyvalidation(this, text)` will check to see if a field is empty or not.

The validation can take place as the visitor enters values, or all at once upon clicking the submit button after entering the values. Each validation function can easily be customized to fit the needs of the fields they are checking. 

#### Functions
`emailvalidation(this, text)`

This function has an optional parameter `text` which will be displayed in an alertbox if content is illegal.
```javascript
function emailvalidation(entered, message) {
  with (entered) {
    atposition = value.indexOf('@'); 
    dotposition = value.lastIndexOf('.');
    lastposition = value.length-1;
    if (atposition < 1 || dotposition-atposition < 2 || lastposition-dotposition > 3 || lastposition-dotposition < 2) {
      if (message) {
        alert(message);
      }
      return false;
    } else {
      return true;
    }
  }
}
```
`valuevalidation(this, min, max, text, type)`

Optional parameters are:
- min - minimum value allowed in the field.
- max - maximum value allowed in the field.
- text - text that will show in an alertbox if content is illegal.
- type - enter "i" if only integers are allowed.
```javascript
function valuevalidation(entered, min, max, message, datatype) {
  with (entered) {
    var checkvalue = parseFloat(value);
    if (datatype) {
      var smalldatatype = datatype.toLowerCase();
      if (smalldatatype.charAt(0) == 'i') {
        checkvalue = parseInt(value)
      };
    }
    if ((parseFloat(min) == min && checkvalue < min) || (parseFloat(max) == max && checkvalue > max) || value != checkvalue) {
      if (message != '') {
        alert(message);
      } 
      return false;
    } else {
      return true;
    }
  }
} 
```

`digitvalidation(this, min, max, text, type)`

Optional parameters are:
- min -minimum number of digits allowed in the field.
- max -maximum number of digits allowed in the field.
- text -text that will show in an alertbox if content is illegal.
- type -enter "i" if only integers are allowed.
```javascript
function digitvalidation(entered, min, max, message, datatype) {
  with (entered) {
    var checkvalue = parseFloat(value);
    if (datatype) {
      var smalldatatype = datatype.toLowerCase();
      if (smalldatatype.charAt(0) == "i") {
        checkvalue = parseInt(value); 
        if (value.indexOf(".") != -1) {
          checkvalue = checkvalue+1
        }
      };
    }
    if ((parseFloat(min) == min && value.length < min) || (parseFloat(max) == max && value.length  >max) || value != checkvalue) {
      if (message != '') {
        alert(message);
      } 
      return false;
    } else {
      return true;
    }
  }
} 
```
`emptyvalidation(this, text)`

Optional parameters are:
- text -text that will show in an alertbox if content is illegal.
```javascript
function emptyvalidation(entered, message) {
  with (entered) {
    if (value == null || value == '') {
      if (message != '') {
        alert(message);
      }
      return false;
    } else {
    return true;
  }
}
```
There are two different ways to call these functions. One is used when you want to check the field immediately after an input is made to it. The other is when you want to check all fields at one time, when the user clicks the submit button.

To force the browser to check each field immediately, we add an onChange to each of the <input> tags in the form:
```html
<input type="text" name="Email" size="20" onChange="emailvalidation(this,'The E-mail is not valid');"> 
```

You might prefer to check all fields at one time when the user hits the submit button. To do this you should add an onSubmit event handler to the <form> tag. 
```html
<form onsubmit="return formvalidation(this)"> 
```
The function that checks the entire form will either return a value of false or true. If it's true the form will be submitted - if it's false the submission will be cancelled. A script that checks all fields in a form could look like this:
```javascript
function formvalidation(thisform) {
  with (thisform) {
    if (emailvalidation(Email, "Illegal E-mail") == false) {
      Email.focus(); 
      return false;
    };
    if (valuevalidation(Value, 0, 5, "Value MUST be in the range 0-5") == false) {
      Value.focus(); 
      return false;
    };
    if (digitvalidation(Digits, 3, 4, "You MUST enter 3 or 4 integer digits", "I") == false) {
      Digits.focus(); 
      return false;
    };
    if (emptyvalidation(Whatever, "The textfield is empty") == false) {
      Whatever.focus(); 
      return false;
    };
  }
} 
```
The above function works in addition to the four functions listed at the top of this page. The function needs to be customized to fit your form. You will need to enter the appropriate form field names used on your own form. (Instead of "E-mail", "Value", "Digits" and "Whatever" in this example). Furthermore, you would need to call the appropriate functions depending on which check you would like to perform on each form field. In the example each field is checked by a different function. You could as well have each field checked by the same function. If for example the form had 4 fields that should all contain an e-mail address you would add an emailvalidation to each.

[**SOURCE**](http://echoecho.com/jsforms01.htm)
