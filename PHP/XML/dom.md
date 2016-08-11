## DOM
DOM is the PHP 5 extension. It is possible to combine SimpleXML and DOM in one document.
#### Loading and Saving XML Documents
Loading from a file:
```php
$dom = new DomDocument();
$din->load("library.xml");
```
Loading from a string. Usful for REST Web Services:
```php
$dom = new DomDocument();
$dom->loadXML($xml);
```
Import HTML files ans strings:
```php
DomDocument::loadHTMLFile()   // loading file
DomDocument::loadHTML()  // loading string
```
Save XML document:
```php
DomDocumnet::save()   // to a file
DomDocument::saveHTML()  // also to a string, but it saves an HTML document instead of an XML file
DomDocument::saveHTMLFile()  // to a file in HTML format
```

