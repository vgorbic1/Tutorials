## Popup Windows
If you only want to open a new browser window you can add the *target="_blank"* attribute 
within the *<a>* element. JavaScript popup windows however, are more powerful.

Using JavaScript's *window.open()* method, you can determine what the window looks like 
(i.e. size, whether it has scrollbars, status bars etc).

### Basic JavaScript Popup Script
```js
<input type="button" 
       value="Open a Popup Window" 
       onclick="window.open('https://www.example.com/',
       'popUpWindow',
       'height=500,
        width=400,
        left=100,
        top=100,
        resizable=yes,
        scrollbars=yes,
        toolbar=yes,
        menubar=no,
        location=no,
        directories=no,
        status=yes');
">
```
The *window.open()* method takes three arguments: the URL of the new page, 
the name of the window, and the attributes of the window. The attributes 
are optional and should be quite self explanatory in the above example.

You can put the above code into a function, then call the function, passing 
the URL as a parameter, whenever you want to open a popup window:
```js
function basicPopup(url) {
  popupWindow = window.open(url,'popUpWindow','height=500,width=500,left=100,top=100');
}
```
```html
<a href="https://www.example.com" onclick="basicPopup(this.href);return false">Open a popup window</a>
```
The **return false** statement ensures our base page doesn't actually go to that address - only the popup window.

### Automatically Center Popup
```js
var popupWindow = null;
function centeredPopup(url,winName,w,h,scroll) {
  LeftPosition = (screen.width) ? (screen.width-w)/2 : 0;
  TopPosition = (screen.height) ? (screen.height-h)/2 : 0;
  settings = 'height='+h+',width='+w+',top='+TopPosition+',left='+LeftPosition+',scrollbars='+scroll+',resizable'
  popupWindow = window.open(url, winName, settings)
}
```
```html
<a href="https://www.example.com" 
   onclick="centeredPopup(this.href,'myWindow','700','300','yes');return false">
   Centered Popup
</a>
```
### Close the Popup Window
```js
<a href="JavaScript:window.close()">Close</a>
```
