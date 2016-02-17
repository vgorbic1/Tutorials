## Form. Get Values

#### Get Values from Radio element
HTML file:
```html
<label for="rice">Select a rice:</label>
  <input name="rice" type="radio" value="White Rice" checked /> White Rice
  <input name="rice" type="radio" value="Brown Rice" /> Brown Rice
```
JavaScript file:
```javascript
var rice = getRadioValue(frm, 'rice');

function getRadioValue(form, name) {
    var value;
    var radios = form.elements[name];  // Use 'name` attribure
    for (var i = 0, len = radios.length; i < len; i++) {
        if ( radios[i].checked ) {
            value = radios[i].value;
            break;
        }
    }
    return value;
}
```
#### Get Value from one Checkbox
HTML file:
```html
<label for="">Guacamole</label>
  <input id="guacamole" type="checkbox" value="Guacamole" />
```
JavaScript file:
```javascript
var check = document.querySelector('#guacamole:checked').value;
```

#### Get Values from Grouped Checkboxes
HTML file:
```html
<label for="salsa">Choose Salsa(s):</label>
  <input name="salsa[]" type="checkbox" value="Pico De Gallo" /> Pico De Gallo 
  <input name="salsa[]" type="checkbox" value="Roasted Corn" /> Roasted Corn 
  <input name="salsa[]" type="checkbox" value="Tomatillo-Green" /> Tomatillo-Green 	
	<input name="salsa[]" type="checkbox" value="Tomatillo-Red" /> Tomatillo-Red
```
JavaScript file:
```javascript
// The array 'salsa' will contain values of all checked checkboxes 
var salsa = getCheckBoxValue(frm, 'salsa[]');  // the name attribute should have these '[]' to get through all checkboxes

function getCheckBoxValue(form, name) {
	var value = [];
	var checkboxes = form.elements[name];
	for (var i = 0, len = checkboxes.length; i < len; i++) {
        if ( checkboxes[i].checked ) {
            value.push(checkboxes[i].value);
        }
    }
	return value;
}
```
