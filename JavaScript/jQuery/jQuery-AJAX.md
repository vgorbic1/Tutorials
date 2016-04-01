## jQuery AJAX
AJAX is about loading data in the background and display it on the webpage, without reloading the whole page. jQuery provides several methods for AJAX functionality. With the jQuery AJAX methods, you can request text, HTML, XML, or JSON from a remote server using both HTTP Get and HTTP Post - And you can load the external data directly into the selected HTML elements of your web page.

#### AJAX load() Method
The load() method loads data from a server and puts the returned data into the selected element.

Syntax:
```
$(selector).load(URL, data, callback);
```
* The required URL parameter specifies the URL you wish to load.
* The optional data parameter specifies a set of querystring key/value pairs to send along with the request.
* The optional callback parameter is the name of a function to be executed after the `load()` method is completed.

The following example loads the content of the element with id="p1", inside the file "demo_test.txt", into a specific <div> element:
```javascript
$("#div1").load("demo_test.txt #p1");
```

#### jQuery get() Method
The get() method requests data from the server with an HTTP GET request.

Syntax:
```
$.get(URL, callback);
```
* The required URL parameter specifies the URL you wish to request.
* The optional callback parameter is the name of a function to be executed if the request succeeds.

The following example uses the $.get() method to retrieve data from a file on the server:
```javascript
$("button").click(function(){
    $.get("demo_test.asp", function(data, status){
        alert("Data: " + data + "\nStatus: " + status);
    });
});
```

#### jQuery post() Method
The post() method requests data from the server using an HTTP POST request.

Syntax:
```
$.post(URL, data, callback);
```
* The required URL parameter specifies the URL you wish to request.
* The optional data parameter specifies some data to send along with the request.
* The optional callback parameter is the name of a function to be executed if the request succeeds.

The following example uses the $.post() method to send some data along with the request:
```javascript
Example
$("button").click(function(){
    $.post("demo_test_post.asp",
    {
        name: "Donald Duck",
        city: "Duckburg"
    },
    function(data, status){
        alert("Data: " + data + "\nStatus: " + status);
    });
});
```
