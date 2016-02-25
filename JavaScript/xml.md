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

} else { // xmlParser will be an instance of ActiveXObject

}
```

