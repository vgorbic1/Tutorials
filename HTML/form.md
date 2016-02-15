## Form

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
