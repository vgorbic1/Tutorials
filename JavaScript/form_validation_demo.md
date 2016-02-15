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
- min --minimum value allowed in the field.
- max --maximum value allowed in the field.
- text --text that will show in an alertbox if content is illegal.
- type --enter "I" if only integers are allowed.
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
      if (message != "") {
        alert(message);
      } 
      return false;
    } else {
      return true;
    }
  }
} 
```
