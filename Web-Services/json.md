## JSON

Historically, JSON originated from JavaScript.
However, nowadays, it is considered to be a language-independent format because of its wide
adoption by all modern programming languages.

JSON is represented by the following two data structures:

1. **An unordered collection of name-value pairs (representing an object):** The attributes of an
object and their values are represented in the name-value pair format; the name and the value in
a pair is separated by a colon (:). Names in an object are strings, and values may be of any of
the valid JSON data types such as number, string, Boolean, array, object, or null. Each
name:value pair in a JSON object is separated by a comma (,). The entire object is enclosed in
curly braces ({ }).

For instance, the JSON representation of a department object is as follows:
```json
{ "departmentId":10, "departmentName":"IT", "manager":"John Chen" }
```
This example shows how you can represent various attributes of a department, such as
departmentId, departmentName, and manager, in the JSON format.

2. **An ordered collection of values (representing an array):** Arrays are enclosed in square
brackets ([ ]), and their values are separated by a comma (,). Each value in an array may be of
a different type, including another array or an object.

The following example illustrates the use of an array notation to represent employees working in
a department:
```json
{"departmentName":"IT",
  "employees":[
    {"firstName":"John", "lastName":"Chen"},
    {"firstName":"Ameya", "lastName":"Job"},
    {"firstName":"Pat", "lastName":"Fay"}
  ],
  "location":["New York", "New Delhi"]
}
```

Basic data types available with JSON:

- **Number:** This type is used for storing a signed decimal number that may optionally contain a
fractional part. Both integer and floating point numbers are represented by using this data type.
The following example uses the decimal data type for storing totalWeight:
```json
{"totalWeight": 123.456}
```
- **String:** This type represents a sequence of zero or more characters. Strings are surrounded with
double quotation marks and support a backslash escaping syntax. Here is an example of the
string data type:
```json
{"firstName": "Jobinesh"}
```
- **Boolean:** This type represents either a true or a false value. The Boolean type is used for
representing whether a condition is true or false, or to represent two states of a variable
(true or false) in the code. Here is an example representing a Boolean value:
```json
{"isValidEntry": true}
```
- **Array:** This type represents an ordered list of zero or more values, each of which can be of any
type. In this representation, comma-separated values are enclosed in square brackets. The
following example represents an array of fruits:
```json
{"fruits": ["apple", "banana", "orange"]}
```
- **Object:** This type is an unordered collection of comma-separated attribute-value pairs enclosed
in curly braces. All attributes must be strings and should be distinct from each other within that
object. The following example illustrates an object representation in JSON:
```json
{"departmentId":10,
"departmentName":"IT",
"manager":"John Chen"}
```
- **null:** This type indicates an empty value, represented by using the word null. The following
example uses null as the value for the error attribute of an object:
```json
{"error":null}
```
