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
Example:
```
<?xml version="1.0"?>
<library>
  <book isbn="03456789">
    <title>Frankenstein</title>
    <author>M. Shelley</author>
    <publisher>Bedford</publisher>
  </book>
  <book>
    <title>The Silmarillion</title>
    <author>J.R.R. Tolkien</author>
    <publisher>G. Allen &amp; Unwin</publisher>
  </book>  
</library>
```
```php
$dom = new DomDocument();
$dom->load('library.xml');
  // do something with the XML here

// save to file
if ($use_xhtml) {
  $dom->save('library.xml');
} else {
  $dom->saveHTMLFile('library.xml);
}

// output data
if ($use_xhtml) {
  echo $dom->saveXML();
} else {
  echo $dom->saveHTML();
}
```
#### XPath Queries
```DomXPath``` is far more powerful than its SimpleXML equivalent:
```php
$dom = new DomDocument();
$dom->load("library.xml");

// instantiate DomXpath object:
$xpath = new DomXPath($dom);

// register only namespaces we need to work with:
$xpath->registerNamespace("lib", "http://example.org/library");

// execute xpath query
$result = $xpath->query("//lib:title/text()");
foreach ($result as $book) {
  echo $book->data;
}
```
Displaying some query results with DOM:
```
$result = $xpath->query("//lib:title/text()");
if ($result->length > 0) {
  
  // Random Access
  $book = $result->item (0);
  echo $book->data;
  
  // Sequential Access
  foreach ($result as $book) {
    echo $book->data;
  }
}
```
#### Modifying XML Documents
To add new data to a loaded document, you need to create new DomElement objects. Let's add a new book to our library.xml document:
```php
$dom = new DomDocument();
$dom->load("library.xml");

$book = $dom->createElement("book");
$book->setAttribute("meta:isbn", "99849837948");

$title = $dom->createElement("title");
$text = $dom->createTextNode("Mastering the SPL Library");

$title->appendChild($text);
$book->appendChild($title);

$author = $dom->createElement("author", "J. Thijssen");
$book->appendChild($author);

$publisher = $dom->createElement("pub:publisher", "Musketeers");
$book->appendChild($publisher);

$dom->documentElement->appendChild($book);
```
