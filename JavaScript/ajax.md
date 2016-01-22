# AJAX

AJAX stands for Asynchronous JavaScript and XML. AJAX is a new technique for creating better, faster, and more 
interactive web applications with the help of XML, HTML, CSS, and Java Script. Ajax uses XHTML for content, CSS for presentation, 
along with Document Object Model and JavaScript for dynamic content display.

Conventional web applications transmit information to and from the server using synchronous requests. It means you fill out a form, 
hit submit, and get directed to a new page with new information from the server.
With AJAX, when you hit submit, JavaScript will make a request to the server, interpret the results, and update the current screen. 
In the purest sense, the user would never know that anything was even transmitted to the server.

XML is commonly used as the format for receiving server data, although any format, including plain text, can be used. AJAX is a web 
browser technology independent of web server software. A user can continue to use the application while the client program requests 
information from the server in the background.

AJAX is the most viable Rich Internet Application (RIA) technology so far. It is getting tremendous industry momentum and several 
tool kit and frameworks are emerging. But at the same time, AJAX has browser incompatibility and it is supported by JavaScript, 
which is hard to maintain and debug.

#### STEPS OF AJAX OPERATION
A JavaScript function is called as the result of an event. Example: ```validateUserId()``` JavaScript function is mapped as an event 
handler to an onkeyup event on input form field whose id is set to "userid":
```<input type="text" size="20" id="userid" name="id" onkeyup="validateUserId();">```
The XMLHttpRequest Object is Created.
```javascript
var ajaxRequest;  // The variable that makes Ajax possible!
function ajaxFunction(){
   try {      
      // Opera 8.0+, Firefox, Safari
      ajaxRequest = new XMLHttpRequest();
   } catch (e) {   
      // Internet Explorer Browsers
      try {
         ajaxRequest = new ActiveXObject("Msxml2.XMLHTTP");
      } catch (e) {   
         try {
            ajaxRequest = new ActiveXObject("Microsoft.XMLHTTP");
         } catch (e) {      
            // Something went wrong
            alert("Your browser broke!");
            return false;
         }
      }
   }
}
```
The XMLHttpRequest Object is configured and making asynchronous request. In this step, we will write a function that will be 
triggered by the client event and a callback function ```processRequest()``` will be registered.
```javascript
function validateUserId() {
   ajaxFunction(); 
   // Here processRequest() is the callback function.
   ajaxRequest.onreadystatechange = processRequest;
   if (!target) target = document.getElementById("userid");
   var url = "validate?id=" + escape(target.value);
   ajaxRequest.open("GET", url, true);
   ajaxRequest.send(null);
}
```
Webserver returns the result containing XML document. You can implement your server-side script in any language, however its logic should be as follows:
* Get a request from the client.
* Parse the input from the client.
* Do required processing.
* Send the output to the client.

If we assume that you are going to write a Java servlet, then here is the piece of code:
```java
public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException {
   String targetId = request.getParameter("id");
   if ((targetId != null) && !accounts.containsKey(targetId.trim())) {
      response.setContentType("text/xml");
      response.setHeader("Cache-Control", "no-cache");
      response.getWriter().write("true");
   } else {
      response.setContentType("text/xml");
      response.setHeader("Cache-Control", "no-cache");
      response.getWriter().write("false");
   }
}
```
Callback function ```processRequest()``` is called next. The XMLHttpRequest object was configured to call the ```processRequest()``` function when there is a state change to the readyState of the XMLHttpRequest object. Now this function will receive the result from the server and will do the required processing. As in the following example, it sets a variable message on true or false based on the returned value from the Webserver.
```javascript
function processRequest() {
   if (req.readyState == 4) {
      if (req.status == 200) {
         var message = ...;
...
}
```
The HTML DOM is updated. This is the final step and in this step, your HTML page will be updated. It happens in the following way:
*JavaScript gets a reference to any element in a page using DOM API. The recommended way to gain a reference to an element is to call. *JavaScript may now be used to modify the element's attributes; modify the element's style properties; or add, remove, or modify the child elements:
```javascript
<script type="text/javascript">
<!--
function setMessageUsingDOM(message) {
   var userMessageElement = document.getElementById("userIdMessage");
   var messageText;  
   if (message == "false") {
      userMessageElement.style.color = "red";
      messageText = "Invalid User Id";
   } else {
      userMessageElement.style.color = "green";
      messageText = "Valid User Id";
   }
   var messageBody = document.createTextNode(messageText);
   // if the messageBody element has been created simple 
   // replace it otherwise append the new element
   if (userMessageElement.childNodes[0]) {
      userMessageElement.replaceChild(messageBody, userMessageElement.childNodes[0]);
   } else {
      userMessageElement.appendChild(messageBody);
   }
}
-->
</script>
<body>
<div id="userIdMessage"><div>
</body>
```
#### XMLHttpRequest
XMLHttpRequest (XHR) is an API that can be used by JavaScript, JScript, VBScript, and other web browser scripting languages to transfer and manipulate XML data to and from a webserver using HTTP, establishing an independent connection channel between a webpage's Client-Side and Server-Side. The data returned from XMLHttpRequest calls will often be provided by back-end databases. Besides XML, XMLHttpRequest can be used to fetch data in other formats, e.g. JSON or even plain text.

#### XMLHttpRequest Methods
```abort()``` Cancels the current request.

```getAllResponseHeaders()``` Returns the complete set of HTTP headers as a string.

```getResponseHeader( headerName )``` Returns the value of the specified HTTP header.

```open( method, URL )```

```open( method, URL, async )```

```open( method, URL, async, userName )```

```open( method, URL, async, userName, password )``` Specifies the method, URL, and other optional attributes of a request.
The method parameter can have a value of "GET", "POST", or "HEAD". Other HTTP methods, such as "PUT" and "DELETE" (primarily used in REST applications) may be possible. The "async" parameter specifies whether the request should be handled asynchronously or not. "true" means that the script processing carries on after the ```send()``` method without waiting for a response, and "false" means that the script waits for a response before continuing script processing.

```send( content )``` Sends the request.

```setRequestHeader( label, value )``` Adds a label/value pair to the HTTP header to be sent.

#### XMLHttpRequest Properties
```onreadystatechange``` An event handler for an event that fires at every state change.

```readyState``` Defines the current state of the XMLHttpRequest object.

Possible values for the readyState property:

```0```	The request is not initialized.

```1```	The request has been set up.

```2```	The request has been sent.

```3```	The request is in process.

```4```	The request is completed.

```readyState = 0``` After you have created the XMLHttpRequest object, but before you have called the ```open()``` method.

```readyState = 1``` After you have called the ```open()``` method, but before you have called ```send()```.

```readyState = 2``` After you have called ```send()```.

```readyState = 3``` After the browser has established a communication with the server, but before the server has completed the response.

```readyState = 4``` After the request has been completed, and the response data has been completely received from the server.

```responseText``` Returns the response as a string.

```responseXML``` Returns the response as XML. This property returns an XML document object, which can be examined and parsed using the W3C DOM node tree methods and properties.

```status``` Returns the status as a number (e.g., 404 for "Not Found" and 200 for "OK").

```statusText``` Returns the status as a string (e.g., "Not Found" or "OK").

### DATABASE OPERATIONS
Create a MySQL database with one table:
```
CREATE TABLE 'ajax_example' (
   'name' varchar(50) NOT NULL,
   'age' int(11) NOT NULL,
   'sex' varchar(1) NOT NULL,
   'wpm' int(11) NOT NULL,
   PRIMARY KEY  ('name')
)
````
Populate the table:
```
INSERT INTO 'ajax_example' VALUES ('Jerry', 120, 'm', 20);
INSERT INTO 'ajax_example' VALUES ('Regis', 75, 'm', 44);
INSERT INTO 'ajax_example' VALUES ('Frank', 45, 'm', 87);
INSERT INTO 'ajax_example' VALUES ('Jill', 22, 'f', 72);
INSERT INTO 'ajax_example' VALUES ('Tracy', 27, 'f', 0);
INSERT INTO 'ajax_example' VALUES ('Julie', 35, 'f', 90);
```
Create a client side HTML file, which is ajax.html:
```
<html>
<body>
<script language="javascript" type="text/javascript">
<!-- 
//Browser Support Code
function ajaxFunction(){
   var ajaxRequest;  // The variable that makes Ajax possible!
   try{
      // Opera 8.0+, Firefox, Safari
      ajaxRequest = new XMLHttpRequest();
   }catch (e){   
      // Internet Explorer Browsers
      try{
         ajaxRequest = new ActiveXObject("Msxml2.XMLHTTP");
      }catch (e) {     
         try{
            ajaxRequest = new ActiveXObject("Microsoft.XMLHTTP");
         }catch (e){        
            // Something went wrong
            alert("Your browser broke!");
            return false;
         }
      }
   }  
   // Create a function that will receive data
   // sent from the server and will update
   // div section in the same page.
   ajaxRequest.onreadystatechange = function(){ 
      if(ajaxRequest.readyState == 4){
         var ajaxDisplay = document.getElementById('ajaxDiv');
         ajaxDisplay.innerHTML = ajaxRequest.responseText;
      }
   }
   // Now get the value from user and pass it to server script.
   var age = document.getElementById('age').value;
   var wpm = document.getElementById('wpm').value;
   var sex = document.getElementById('sex').value;
   var queryString = "?age=" + age ;
   queryString +=  "&wpm=" + wpm + "&sex=" + sex;
   ajaxRequest.open("GET", "ajax-example.php" + queryString, true);
   ajaxRequest.send(null); 
}
//-->
</script>

<form name='myForm'>
   Max Age: <input type='text' id='age' /> <br />
   Max WPM: <input type='text' id='wpm' /> <br />
   Sex: 
   <select id='sex'>
      <option value="m">m</option>
      <option value="f">f</option>
   </select>
   <input type='button' onclick='ajaxFunction()' value='Query MySQL'/>
</form>
<div id='ajaxDiv'>Your result will display here</div>
</body>
</html>
```
Write the server-side script, which will fetch age, wpm, and sex from the database and will send it back to the client. Put the following code into the file "ajax-example.php".
```
<?php
$dbhost = "localhost";
$dbuser = "dbusername";
$dbpass = "dbpassword";
$dbname = "dbname";	
//Connect to MySQL Server
mysql_connect($dbhost, $dbuser, $dbpass);
//Select Database
mysql_select_db($dbname) or die(mysql_error());	
// Retrieve data from Query String
$age = $_GET['age'];
$sex = $_GET['sex'];
$wpm = $_GET['wpm'];	
// Escape User Input to help prevent SQL Injection
$age = mysql_real_escape_string($age);
$sex = mysql_real_escape_string($sex);
$wpm = mysql_real_escape_string($wpm);
//build query
$query = "SELECT * FROM ajax_example WHERE sex = '$sex'";
if(is_numeric($age))
   $query .= " AND age <= $age";
if(is_numeric($wpm))
   $query .= " AND wpm <= $wpm";	
//Execute query
$qry_result = mysql_query($query) or die(mysql_error());
//Build Result String
$display_string = "<table>";
$display_string .= "<tr>";
$display_string .= "<th>Name</th>";
$display_string .= "<th>Age</th>";
$display_string .= "<th>Sex</th>";
$display_string .= "<th>WPM</th>";
$display_string .= "</tr>";
// Insert a new row in the table for each person returned
while($row = mysql_fetch_array($qry_result)){
   $display_string .= "<tr>";
   $display_string .= "<td>$row[name]</td>";
   $display_string .= "<td>$row[age]</td>";
   $display_string .= "<td>$row[sex]</td>";
   $display_string .= "<td>$row[wpm]</td>";
   $display_string .= "</tr>";
}
echo "Query: " . $query . "<br />";
$display_string .= "</table>";
echo $display_string;
?>
```

### AJAX SECURITY
#### Server side
AJAX-based Web applications use the same server-side security schemes of regular Web applications. You specify authentication, authorization, and data protection requirements in your web.xml file (declarative) or in your program (programmatic). AJAX-based Web applications are subject to the same security threats as regular Web applications.

#### Client side 
JavaScript code is visible to a user/hacker. Hacker can use JavaScript code for inferring server-side weaknesses. JavaScript code is downloaded from the server and executed ("eval") at the client and can compromise the client by mal-intended code. Downloaded JavaScript code is constrained by the sand-box security model and can be relaxed for signed JavaScript.
