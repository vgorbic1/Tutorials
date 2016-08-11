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

#### Moving Data
Moving a node with DOM. Take the second book element and place it before the first.
```php
$dom = new DOMDocument();
$dom->load("library.xml");

$xpath = new DomXPath($dom);
$xpath->registerNamespace("lib", "http://example.org/library");

$result = $xpath->query("//lib:book");
$result->item(1)->parentNode->insertBefore($result->item(1), $result->item(0));
```
Take the first book element and place it at the end.
```php
$dom = new DOMDocument();
$dom->load("library.xml");

$xpath = new DomXPath($dom);
$xpath->registerNamespace("lib", "http://example.org/library");

$result = $xpath->query("//lib:book");
$result->item(1)->parentNode->appendChild($result->item(0));
```
To duplicate a node:
```php
$dom = new DOMDocument();
$dom->load("library.xml");

$xpath = new DomXPath($dom);
$xpath->registerNamespace("lib", "http://example.org/library");

$result = $xpath->query("//lib:book");
$clone = $result->item(0)->cloneNode();
$result->item(1)->parentNode->appendChild($clone);
```
#### Modifying Data
When modifyint data, you will typically want to edit the CDATA within a node.
```php
$xml = <<<XML
<xml>
  <text>some text here</text>
</xml>
XML;

$dom = new DOMDocument();
$dom->loadXML($xml);

$xpath = new DomXPath($dom);

$node = $xpath->query("//text/text()")->item(0);
$node->data = ucwords($node->data);

echo $dom->saveXML();
```
gives:
```
</xml version="1.0"?>
<xml>
  <text>Some Text Here</text>
</xml>
```
#### Removing Data
You can remove attributes, elements, and CDATA.
```php
$xml = <<<XML
<xml>
  <text>some text here</text>
  <text>some more text here</text>
  <text>yet more here</text>
</xml>
XML;

$dom = new DOMDocument();
$dom->loadXML($xml);

$xpath = new DomXPath($dom);

// retrieve all text nodes
$result = $xpath->query("//text");
$result->item(0)->parentNode->removeChild($result->item()0);
$result->item(1)->removeAttribute('type');

$result = $xpath->query('text()', $result->item(2));
$result->item(0)->deleteData(0, $result->time(0)->length);

echo $dom->saveXML();
```
#### Using Namespace prefixes
```php
$dom = new DomDocument()';

$node = $dom->createElement('ns1:somenode');

$node->setAttribute('ns2:someattribute', 'somevalue');
$node2 = $dom->createElement('ns3:anothernode');
$node->appendChild($node2);

// set xmlns:* attributes
$node->setAttribute('xmlns:hs1', 'http://exmple.org/ns1');
$node->setAttribute('xmlns:hs2', 'http://exmple.org/ns2');
$node->setAttribute('xmlns:hs3', 'http://exmple.org/ns3');

$dom->appendChild($node);

echo $dom->saveXML();
```
Or use methods:
```php
$dom = new DomDocument();

$node = $dom->createElementNS('http://example.org/ns1', 'ns1:somenode');
$node->setAttributeNS('http://example.org/ns2', 'ns2:someattribute', 'somevalue');
$node2 = $dom->createElementNS('http://example.org/ns3', 'ns3:anothernode');
$node3 = $dom->createElementNS('http://example.org/ns1', 'ns1:someothernode');

$node->appendChild($node2);
$node->appendChild($node3);
$dom->appendChild($node);

$dom->formatOutput = true;
echo $dom->saveXML();
```
will result in
```
<?xml version="1.0"?>
  <ns1:somenode xmlns:ns1="http://example.org/ns1"
    xmlns:ns2="http://example.org/ns2"
    xmlns:ns3="http://example.org/ns3"
    ns2:someattribute="somevalue">
  <ns3:anothernode xmlns:ns3="http://example.org/ns3"/>
  <ns1:someothernode/>
</ns1:somenode>
```
#### Interfacing with SimpleXML from DOM
```php
$sxml = simplexml_load_file('library.xml');

$node = dom_import_simplexml($sxml);
$dom = new DomDocument();
$dom->importNode($node, true);

$dom->appendChild($node);
```
