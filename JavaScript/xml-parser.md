## XML Data
We can deal with XML in two different ways:
- XML string of data. It is typical for legacy software or server applications, or web services.
- An XML file on the file system.

#### String of Data
Suppose we have a string of XML data:
```xml
<users>
  <user id='1'>
    <name>
      <first>aaron</first>
      <last>rodgers</last>
    </name>
  </user>
  <user id='2'>
    <name>
      <first>randall</first>
      <last>cobb</last>
    </name>
  </user>
  <user id='3'>
    <name>
      <first>clay</first>
      <last>mathews</last>
    </name>
  </user>
</users>
```
Convert the string to an XML parser (DOM Parser). The XML parser is not cross-browser solution, it does not exisit in IE.
```javascript
var xmlData = '<users><user id='1'><name><first>aaron</first><last>rodgers</last></name></user><user id='2'><name><first>randall</first> <last>cobb</last></name></user><user id='3'><name><first>clay</first><last>mathews</last></name></user></users>';
var xmlParser;
if (window.DOMParser) { // xmlParser will be an instance of DOMParser
  xmlParser = new DOMParser().parseFromString(xmlData, "application/xml");
} else { // xmlParser will be an instance of ActiveXObject
  xmlParser = new ActiveXObject("Microsoft.XMLDOM");
  xmlParser.loadXML(xmlData);
}
queryXML(xmlParser); // separate function that will deal with quering the XML document
```
To query the XML document:
```javascript
function queryXML(xmlParser) {  // Assume, that we already get the file content loaded from the previous example
	//Querying the XML
	var nameNodes = xmlParser.getElementsByTagName("name"); //returns an array
	//[0] = <name><first>bill</first><last>gates</last></name>
	//[1] = <name><first>steve</first><last>jobs</last></name>
	for (var i=0; i< nameNodes.length; i++) {
		var id = nameNodes[i].parentNode.id; // get the attribute of the element "user"
		var first = nameNodes[i].getElementsByTagName("first")[0].childNodes[0].nodeValue; // get the "first" element value 
		var last = nameNodes[i].getElementsByTagName("last")[0].childNodes[0].nodeValue; // get the "second" element value
		console.log("id: " + id);
		console.log(first + " " + last);
	}
}
```
#### XML File on Filesystem
Load the file contents (users.xml) into an xmlParser using AJAX
```javascript
var xhr = new XMLHttpRequest();
xhr.open("GET", "users.xml"); //server url (file on a filesystem)
//callback
xhr.onreadystatechange = function() {
//readyState = 0 .. 4
  if(xhr.readyState == 4) {
    //process the results asyncronously
    queryXML(xhr.responseXML);
  }
xhr.send(null); //go get the result from the url request
queryXML(xmlParser); // separate function that will deal with quering the XML document
```
To query the XML document (will be the same as in the example with the string data):
```javascript
function queryXML(xmlParser) {  // Assume, that we already get the string loaded from the previous example
	//Querying the XML
	var nameNodes = xmlParser.getElementsByTagName("name"); //returns an array
	//[0] = <name><first>bill</first><last>gates</last></name>
	//[1] = <name><first>steve</first><last>jobs</last></name>
	for (var i=0; i< nameNodes.length; i++) {
		var id = nameNodes[i].parentNode.id; // get the attribute of the element "user"
		var first = nameNodes[i].getElementsByTagName("first")[0].childNodes[0].nodeValue; // get the "first" element value 
		var last = nameNodes[i].getElementsByTagName("last")[0].childNodes[0].nodeValue; // get the "second" element value
		console.log("id: " + id);
		console.log(first + " " + last);
	}
}
```
