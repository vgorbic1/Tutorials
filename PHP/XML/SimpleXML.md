## PARSING XML WITH SimpleXML
Added in PHP5 the SimpleXML is an easy to use DOM parser. PHP treats elements and attributes as objects, so you need to cast them to strings in order to use them for comparison or in any standard string functions. 

SimpleXML also supports XPath, a language used to perform queries (search for data) within XML documents.
DOM parsers require more memory on the server than SAX parsers because they load the entire XML data into a variable.

To use SimpleXML with PHP, load xml file into an object:
```php
$xml = simplexml_load_file('filename.xml');
```
If you have a bunch of XML strings use this instead:
```php
$xml = simplexml_load_string($xml_string);
```
Access specific elements:
```php
echo $xml -> elementname;
```
If there are several elements, access them as elements in an array:
```php
echo $xml -> elementname[0];
```
For nested elements:
```php
$xml -> product[0] -> name;
```
Or use a foreach loop:
```php
foreach ($xml -> product as $product) {
    echo $product -> name;
    echo $product -> price;
}
```
To access attributes:
```php
$xml -> elementname['attributename'];
```
You also can modify the loaded XML data using ```addChild()``` or ```addAttribute()``` methods.

To change the value of an element:
```php
$xml -> product -> name = 'Heavy T-shirt';
```
Example:
```php
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>SimpleXML Parser</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
<?php /*  This script will parse an XML file.
 *  It uses the simpleXML library, a DOM parser. */
 // Read the file:
$xml = simplexml_load_file('books4.xml');
// Iterate through each book:
foreach ($xml->book as $book) {
    // Print the title:
    echo "<div><h2>$book->title";  
    // Check for an edition:
	if (isset($book->title['edition'])) {
	    echo " (Edition {$book->title['edition']})";
	}
	echo '</h2>';    
    // Print the author(s):
	foreach ($book->author as $author) {
	    echo "<span class=\"label\">Author</span>: $author<br>";
	}  
    // Print the other book info:
	echo "<span class=\"label\">Published:</span> $book->year<br>";
	if (isset($book->pages)) {
	    echo "<span class=\"label\">Pages:</span> $book->pages<br>";
	}     
    // Print each chapter:
	if (isset($book->chapter)) {
	    echo 'Table of Contents<ul>';
	    foreach ($book->chapter as $chapter) {     
			echo '<li>';
			if (isset($chapter['number'])) {
			    echo "Chapter {$chapter['number']}: ";
			}
			echo $chapter;
			if (isset($chapter['pages'])) {
			    echo " ({$chapter['pages']} Pages)";
			}
			echo '</li>';           
        }
        echo '</ul>';
    }    
    // Handle the cover:
	if (isset($book->cover)) {
	    // Get the image info:
	    $image = @getimagesize ($book->cover['filename']);
	    // Make the image HTML:
	    echo "<img src=\"{$book->cover['filename']}\" $image[3] border=\"0\" /><br>";    
	}   
    // Close the book's DIV tag:
    echo '</div>';   
} // End of foreach loop.
?>
</body>
</html>
```

#### Iterating with SimpleXML
SimpleXML provides a means to access childern and attributes without needing to know their names. In fact, SimpleXML will even tell you their names.
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
// Load an XML string
$xmlstr = file_get_contents('library.xml');
$library = simplexml_load_string($xmlstr);

// or load an XML file
$library = new SimpleXMLElement('library.xml', NULL, true);

foreach ($library->children() as $child) {
  echo $child->getName() . ":\n";
  
  // Get attributes of this element
  foreach ($child->attributes() as $attr) {
    echo ' ' . $attr->getName() . ': ' . $attr . "\n";
  }
  
  // Get children
  foreach ($child->children() as $subchild) {
    echo ' ' . $subchild->getName() . ': ' . $subchild . "\n";
  }
  echo "\n";
}
```
The XML Path Language (XPath) is used to access and search XML docunments, like a query language for retrieving data from an XML document. If query is used on the root element, it will search the entire XML document. If used on achild, it will search the child and any childern it may have:
```php
// Search the root element
$results = $library->xpath('/library/book/title');
foreach ($results as $title) {
  echo $title . "\n";
}

// Search the first child element
$results = $library->book[0]->xpath('title');
foreach ($results as $title) {
  echo $title . "\n";
}
```
To modify XML Document, (add a new element and children):
```
$book = $library->addChild('book');
$book->addAttribute('isbn', '081255');
$book->addChild('title', "Ender's Game");
$book->addChild('author', 'O. Card');
$book->addChild('publisher', 'Tor Science Fiction');

header('Content-type: text/xml');
echo $library->asXML();
```
Called without a parameter, ```asXML()``` method returns an XML string. It also accepts a file path as a parameter, which will cause it to save the XML document to the given path and return a Boolean value to indicate success. If a file with the same path already exists, a call to ```asXML()``` will overwrite it without warning.

To only remove a child element and it's attribute. It will not remove attributes from the "book" level though. For that, export the SimpleXMLElement to DOM.
```php
$library->book[0] = NULL;
```

**Working with Namespaces**
This example presents namespaces:
```
<?xml version="1.0"?>
<library xmlns="http://example.org/library"
  xmlns:meta="http://example.org/book-meta"
  xmlns:pub="http://example.org/publisher"
  xmlns:foo="http://example.org/foo">
  <book meta:isbn="0456757">
    <title>The Silmarillion</title>
    <author>J.R.R. Tolkien</author>
    <pub:publisher>G. Allen &amp; Unwin</publisher>
  </book>
</library>
```
Returning document namespaces (all declared)
```php
  $namespaces = $library->getDocNamespaces();
  foreach ($namespaces as $key => $value) {
    echo "{$key} => {$value}\n";
  }
```
Returning document namespaces (only those that were actually used)
```php
  $namespaces = $library->getNamespaces(true);
  foreach ($namespaces as $key => $value) {
    echo "{$key} => {$value}\n";
  }
```
#### Interfacing with DOM
```php
$dom = new DOMDocument();
$dom->load('library.xml');
$sxe = simplexml_import_dom($dom);
echo $sxe->book[0]->title;
```
