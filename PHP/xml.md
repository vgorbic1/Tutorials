## XML

#### PARSING XML WITH EXPAT
Expat's parsing events resemble the events defined in the Simple-API-for-XML (SAX), but Expat is not a SAX-compliant parser. Projects incorporating the Expat library often build SAX and possibly DOM parsers on top of Expat. While Expat is mainly a stream-based (push) parser, it supports stopping and restarting parsing at arbitrary times, thus making the implementation of a pull parser relatively easy. Expat makes use of callback functions when events occur. The Expat library can read an XML document, but it cannot validate one.

To use Expat with PHP first create a new parser:
```php
$p = xml_parser_create();
```
Identify the functions to use for handling events. You need to tell to PHP what user-defined functions should be called when each of events occurs. When the parser encounters the different events, it will automatically send that content to the proper function:
```php
xml_set_element_handler($p, 'open_element_fx', 'close_element_fx');
xml_set_character_data_handler($p, 'data_fx');
```
Parse the file. The third argument tells the parser when to stop working:
```php
xml_parse($p, $data, $stop);
Free up the resources used by the parser:
xml_parser_free($);
```
This script uses Expat to make a legible Web page from an XML file:
```php
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>XML Expat Parser</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
<?php /*  This script will parse an XML file.
 *  It uses the Expat library, an event-based parser. */
// Function for handling the open tag:
function handle_open_element($p, $element, $attributes) {
    // Do different things based upon the element:
    switch ($element) {  
        // Need to address: book, title, author, year, chapter, and pages!    
        case 'BOOK': // Books are DIV's:
            echo '<div>';
            break;           
        case 'CHAPTER': // Chapters are Ps:
            echo "<p>Chapter {$attributes['NUMBER']}: ";
            break;      
        case 'COVER': // Show the image...
            // Get the image info:
            $image = @getimagesize($attributes['FILENAME']);  
            // Make the image HTML:
            echo "<img src=\"{$attributes['FILENAME']}\" $image[3] border=\"0\"><br>";
            break;          
        case 'TITLE': // Titles are H2s:
            echo '<h2>';
            break;            
        // Everything else is just displayed:
        case 'YEAR':
        case 'AUTHOR':
        case 'PAGES':
            echo '<span class="label">' . $element . '</span>: ';
            break;
            
    } // End of switch.    
} // End of handle_open_element() function.
// Function for handling the closing tag:
function handle_close_element($p, $element) {
    // Do different things based upon the element:
    switch ($element) {    
        // Close up HTML tags...
        case 'BOOK': // Books are DIV's:
            echo '</div>';
            break;     
        case 'CHAPTER': // Chapters are Ps:
            echo '</p>';
            break;     
        case 'TITLE': // Titles are H2s:
            echo '</h2>';
            break;    
        // Add a break to the others:
        case 'YEAR':
        case 'AUTHOR':
        case 'PAGES':
            echo '<br>';
            break;
    } // End of switch.   
} // End of handle_close_element() function.
// Function for printing the content:
function handle_character_data($p, $cdata) {
    echo $cdata;
}
// Create the parser:
$p = xml_parser_create();
// Set the handling functions:
xml_set_element_handler($p, 'handle_open_element', 'handle_close_element');
xml_set_character_data_handler($p, 'handle_character_data');
// Read the file:
$file = 'books4.xml';
$fp = @fopen($file, 'r') or die("<p>Could not open a file called '$file'.</p></body></html>");
while ($data = fread($fp, 4096)) {
    xml_parse($p, $data, feof($fp));
}
// Free up the parser:
xml_parser_free($p);
?>
</body>
</html>
```

#### PARSING XML WITH SimpleXML
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

#### CREATING RSS FEED
Really Simple Syndication (RSS), used to mean Rich Site Summary, is the way for Web sites to provide listings of the site's content. RSS is a closed standard and frozen from further development. Users access the feeds (XML files with pre-established tags) by RSS client, usually a Web browser. See the formal specifications at www.rssboard.org/rss-specification Atom is an open standard offshoot of RSS. 

To create a server-side RSS feed with PHP:
```php
<?php /*	This script will create an RSS feed.
 *	The feed content will be based upon an array. */
// Send the Content-type header:
header('Content-type: text/xml'); 
// Create the initial RSS code:
echo '<?xml version="1.0" encoding="utf-8"?>
<rss version="2.0">
<channel>
<title>Larry Ullman&apos;s Important Things</title>
<description>The most recent things Larry has been writing about.</description>
<link>http://LarryUllman.com/</link>
';
// Manufacture the data:
$data = array(
	0 => array('title' => 'SSH Key Authentication', 'description' => 'The wonderful hosting company that I use', 'link' => 'http://www.larryullman.com/2012/05/25/ssh-key-authentication/', 'pubDate' => '1337930580'),
	1 => array('title' => 'What It Means to Be a Writer, Part 1', 'description' => 'A little while back, I had a series of emails', 'link' => 'http://www.larryullman.com/2012/05/23/what-it-means-to-be-a-writer-part-1-defining-your-book/', 'pubDate' => '1337683425'),
	2 => array('title' => 'Learn to Write', 'description' => 'There was a recent posting by', 'link' => 'http://www.larryullman.com/2012/05/18/learn-to-write/', 'pubDate' => '133733103')
);
// Loop through the data:
foreach ($data as $item) {
	// Print each record as an item:
	echo '<item>
	<title>' . htmlentities($item['title']) . '</title>
	<description>' . htmlentities($item['description']) . '...</description>
	<link>' . $item['link'] . '</link>
	<guid>' . $item['link'] . '</guid>
	<pubDate>' . date('r', $item['pubDate']) . '</pubDate>
	</item>
	';	
}
// Complete the channel and rss elements:
echo '</channel>
</rss>
';
```
Load this application by any Feed reader (browser).

To check if the created feed is valid use: feedvalidator.org
