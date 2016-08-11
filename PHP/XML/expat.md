## PARSING XML WITH EXPAT
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
