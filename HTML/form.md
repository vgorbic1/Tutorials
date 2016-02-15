## Form

#### Text Field
Text fields are one line areas that allow the user to input text.
```html
<input type="text" />
```

**Settings**

|HTML|EXPLANATION|
|---|---|
|size=|Defines the width of the field. That is how many visible characters it can contain.|
|maxlength=|Defines the maximum length of the field. That is how many characters can be entered in the field. If you do not specify a maxlength, the visitor can easily enter more characters than are visible in the field at one time.|
|name=|Adds an internal name to the field so the program that handles the form can identify the fields.|
|value=|Defines what will appear in the box as the default value.
|align=|Setting defines how the field is aligned. Valid entries are: TOP, MIDDLE, BOTTOM, RIGHT, LEFT, TEXTTOP, BASELINE, ABSMIDDLE, ABSBOTTOM.|
|tabindex=|defines in which order the different fields should be activated when the visitor clicks the tab key.|
```html
<input type="text" size="25" value="Enter your name here!" />
```

#### Password Field
Password fields are similar to text fields. The difference is that what is entered into a password field shows up as dots on the screen. This is, of course, to prevent others from reading the password on the screen.
```html
<input type="password" />
```

**Settings**

|HTML|EXPLANATION|
|---|---|
|size=|Defines the width of the field. That is how many visible characters it can contain.|
|maxlength=|Defines the maximum length of the field. That is how many characters can be entered in the field. If you do not specify a maxlength, the visitor can easily enter more characters than are visible in the field at one time.|
|name=|Adds an internal name to the field so the program that handles the form can identify the fields.|
|value=|Defines what will appear in the box as the default value.
|align=|Setting defines how the field is aligned. Valid entries are: TOP, MIDDLE, BOTTOM, RIGHT, LEFT, TEXTTOP, BASELINE, ABSMIDDLE, ABSBOTTOM.|
|tabindex=|defines in which order the different fields should be activated when the visitor clicks the tab key.|
```html
<input type="password" size="25" value="Enter password" />
```

#### Hidden Field
The hidden field does not show on the page. Therefore the visitor can't type anything into a hidden field, which leads to the purpose of the field to submit information that is not entered by the visitor.
```html
<input type="hidden" />
```

**Settings**

|HTML|EXPLANATION|
|---|---|
|name=|Adds an internal name to the field so the program that handles the form can identify the fields.|
|value=|Defines what will appear in the box as the default value.|
```html
<input type="hidden" name="Language" value="English" />
```


#### Check Box
Check boxes are used when you want to let the visitor select one or more options from a set of alternatives.
```html
<input type="checkbox" />
```

**Settings**

|HTML|EXPLANATION|
|---|---|
|name=|Adds an internal name to the field so the program that handles the form can identify the fields.|
|value=|Defines what will be submitted if checked.|
|align=|Defines how the field is aligned. Valid entries are: TOP, MIDDLE, BOTTOM, RIGHT, LEFT, TEXTTOP, BASELINE, ABSMIDDLE, ABSBOTTOM.|
|tabindex=|defines in which order the different fields should be activated when the visitor clicks the tab key.|
|checked|Default check this field.|
```html
<div align="center"><br />
<input type="checkbox" name="option1" value="Milk" /> Milk<br />
<input type="checkbox" name="option2" value="Butter" checked /> Butter<br />
<input type="checkbox" name="option3" value="Cheese" /> Cheese<br />
<br />
</div>
```

#### Radio Button
Radio buttons are used when you want to let the visitor select one - and just one - option from a set of alternatives.
```html
<input type="radio" />
```

**Settings**

|HTML|EXPLANATION|
|---|---|
|name=|tells which group of radio buttons the field belongs to. When you select one button, all other buttons in the same group are unselected. If you couldn't define which group the current button belongs to, you could only have one group of radio buttons on each page.|
|value=|Value that is submitted if checked.|
|align=|Alignment of the field. Valid entries are: TOP, MIDDLE, BOTTOM, RIGHT, LEFT, TEXTTOP, BASELINE, ABSMIDDLE, ABSBOTTOM.|
|tabindex=|defines in which order the different fields should be activated when the visitor clicks the tab key.|
|checked|Default check this field|
```html
<div><br />
  <input type="radio" name="group1" value="Milk" /> Milk<br />
  <input type="radio" name="group1" value="Butter" checked /> Butter<br />
  <input type="radio" name="group1" value="Cheese" /> Cheese
  <hr />
  <input type="radio" name="group2" value="Water" /> Water<br />
  <input type="radio" name="group2" value="Beer" /> Beer<br />
  <input type="radio" name="group2" value="Wine" checked /> Wine<br />
</div>
```

#### Drop-down Menu
Drop-down menus can serve the same purpose as radio buttons (one selection only) or check boxes (multiple selections allowed). The advantage of a drop-down menu, compared to radio buttons or check boxes, is that it takes up less space. But that is also a disadvantage, because people can't see all options in the menu right away.
```html
<select>
  <option>Milk</option>
  <option>Coffee</option>
  <option>Tea</option>
</select>
```
**Settings**

|HTML|EXPLANATION|
|---|---|
|**select**|
|name=|Adds an internal name to the field so the program that handles the form can identify the fields.|
|size=|Defines how many items should be visible at a time. Default is one item.|
|multiple=|Allow for multiple selections if present.|
|**option**|
|selected|Forces an item to be default selected.|
|value=|Defines what will be submitted if the item is selected. This is not always the same as what it says in the menu.|
```html
<div>
  <select name="mydropdown">
    <option value="Milk">Fresh Milk</option>
    <option value="Cheese">Old Cheese</option>
    <option value="Bread">Hot Bread</option>
  </select>
</div>
```

#### Text Area
Text areas are text fields that can span several lines.
```html
<textarea></textarea>
```
**Settings**

|HTML|EXPLANATION|
|---|---|
|rows=|Rows in the field.|
|cols=|Columns in the field.|
|name=|Adds an internal name to the field so the program that handles the form can identify the fields.|
|tabindex=|Defines in which order the different fields should be activated when the visitor clicks the tab key.|
|wrap=off|The text will handled as one long sequence of text without linebreaks.|
|wrap=virtual|The text will appear as if it recognized linebreaks - but when the form is submitted the linebreaks are turned off.|
|wrap=physical|The text will be submitted exactly as it appears on the screen - linebreaks included.|
```html
<div align="center">
  <textarea cols="40" rows="5" name="myname"></textarea>
</div>
```
