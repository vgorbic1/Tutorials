## Form

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
<div align="center"><br>
<input type="radio" name="group1" value="Milk"> Milk<br>
<input type="radio" name="group1" value="Butter" checked> Butter<br>
<input type="radio" name="group1" value="Cheese"> Cheese
<hr>
<input type="radio" name="group2" value="Water"> Water<br>
<input type="radio" name="group2" value="Beer"> Beer<br>
<input type="radio" name="group2" value="Wine" checked> Wine<br>
</div>
```
