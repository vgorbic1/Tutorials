# AJAX
To use ajax on the webserver first create a JavaScript object with ```CreateAjaxObject()``` function:
```javascript
function CreateAjaxObject(callback) {
    try {
        var ajax = new XMLHttpRequest();
    } catch(e1) {
	try {
	    ajax = new ActiveXObject("Msxml2.XMLHTTP");
	} catch(e2) {
	    try {
	        ajax = new ActiveXObject("Microsoft.XMLHTTP");
	    } catch(e3) {
	        ajax = false;
	    }
	}
    }
    
    if (ajax) ajax.onreadystatechange = function() {
	if (this.readyState == 4 && this.status == 200 && this.responseText != null) {
	    callback.call(this.responseText);
	} else {
           return false;
        }
    return ajax;
    }
}
```
Create functions that will call CreateAjaxObject function to complete the Ajax process. This function takes three arguments: the name of your callback function to receive data from the server, the url with which to communicate with the server, and string with arguments to post to the server. It sends the data using Post request.
```javascript
function PostAjaxRequest(callback, url, args) {
	var contenttype = 'application/x-www-form-urlencoded';
	var ajax        = new CreateAjaxObject(callback);
	if (!ajax) return false;
	ajax.open('POST', url, true);
	ajax.setRequestHeader('Content-type', contenttype);
	ajax.setRequestHeader('Content-length', args.length);
	ajax.setRequestHeader('Connection', 'close');
	ajax.send(args);
	return true;
}
```
Similar function, but sends Get request. Always have both functions in one document to allow for proper server interaction:
```javascript
function GetAjaxRequest(callback, url, args) {
	var nocache = '&nocache=' + Math.random() * 1000000; // prevent caching
	var ajax    = new CreateAjaxObject(callback);
	if (!ajax) return false;
	ajax.open('GET', url + '?' + args + nocache, true);
	ajax.send(null);
	return true;
}
```
Create a ```callback()``` function that will receive the data sent back to PHP via Ajax:
```javascript
function callback() {
    document.getElementById('mydiv').inner = this;
}
```
Supply HTML:
<div id='mydiv'></div>

Now we are ready to call either the ```PostAjaxRequest()``` or ```GetAjaxRequest()```:
```javascript
<script>
   PostAjaxRequest(function() {
      document.getElementById('mydiv').innerHTML = this
      }, 'ajax.php', 'url=http://wikipedia.org/wiki/AJAX')
</script>
````
In either instance, a program in the same folder as the calling code (called ajax.php) is chosen for communication, and the URL is sent to the program as the value of the key url.

Write the ajax.php program that will reside on server and communicate with the web browser. It tests whether the key url has been sent to it, either in a Post request (as $_POST['url']) or Get request (as $_GET['url']). This fetches the web page referred to and returned to the calling Ajax function using the PHP echo keyword:
```php
  echo isset($_POST['url']) ? file_get_contents($_POST['url']) : file_get_contents($_GET['url']);
```
