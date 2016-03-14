## XML to JSON
One considerable advantage of using a JSON API is its ability to provide cross-domain requests while bypassing the restrictive same domain policy of the XmlHttpRequest object.

#### A Pragmatic Approach
A single structured XML element might come in seven flavors:

Description | XML | JSON
--- | --- | ---
an empty element | `<element />` | null
an element with pure text content | `<element>text</element>` | "text"
an empty element with attributes | `<element name="value" />` | {"@name": "value"}
an element with pure text content and attributes | `<element name="value">text</element>` | { "@name": "value", "#text": "text" }
an element containing elements with different names | `<element> <a>text</a> <b>text</b> </element>` | { "a": "text", "b": "text" }
an element containing elements with identical names | `<element> <a>text</a> <a>text</a> </element>` | { "a": ["text", "text"] } 
an element containing elements and contiguous text | `<element> text <a>text</a> </element>` | { "#text": "text", "a": "text" }

#### Preserving order
JSON is built on two internal structures:
* A collection of name/value pairs with unique names (associative array)
* An ordered list of values (array)


Map a structured XML element with repeating elements:
```xml
<element>
  <a>some</a>
  <b>textual</b>
  <a>content</a>
</element>
```
We need to collect all elements of identical names in an array:
```javascript
"element": {
  "a": [ "some", "content" ],
  "b": "textual"
}
```
Now we have a structure that doesn't preserve element order! A structured XML element can be converted to a reversible JSON structure, if all subelement names occur exactly once, or subelements with identical names are in sequence.
