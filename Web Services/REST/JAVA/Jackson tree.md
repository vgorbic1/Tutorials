## Processing JSON with Jackson Tree Model APIs

The Jackson tree model API provides an in-memory representation of the JSON data. A client can
optionally modify the object model representation.

Use the `com.fasterxml.jackson.databind.ObjectMapper` class to convert the JSON
data into a tree representation. This class has a variety of APIs to build a tree from the JSON data.

The tree representation built from JSON is made up of
`com.fasterxml.jackson.databind.JsonNode` instances. This is similar to the DOM nodes in an
XML DOM tree.

A sample JSON string in `emp-array.json` file:
```json
[{"employeeId":100,"firstName":"John","lastName":"Chen","email":"john.chen@xxxx.com","hireDate":"2008-10-16"},
{"employeeId":101,"firstName":"Ameya","lastName":"Job","email":"ameya.job@xxx.com","hireDate":"2013-03-06"},
{"employeeId":102,"firstName":"Pat","lastName":"Fay","email":"pat.fey@xxx.com","hireDate":"2001-03-06"}]
```
The following code snippet will help understand the use of these APIs:
```java
// Other imports are removed for brevity
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.node.ObjectNode;

// Read in the JSON employee array form emp-array.json file
InputStream inputStream = getClass().getResourceAsStream("/emp-array.json");

// Create ObjectMapper instance. 
// ObjectMapper provides functionality for creating tree structure for JSON content
ObjectMapper objectMapper = new ObjectMapper();

// Read JSON content in to tree
JsonNode rootNode = objectMapper.readTree(inputStream);

// Check if the json content is in array form
if (rootNode.isArray()) {

  // Iterate over each element in the array
  for (JsonNode objNode : rootNode) {
  
    // Find out the email node by traversing tree
    JsonNode emailNode = objNode.path("email");
    
    //if email is null, then update with a system generated email
    if (emailNode.textValue() == null ) {
      String generatedEmail = getSystemGeneratedEmail();
      ((ObjectNode)objNode).put("email", generatedEmail );
    }
  }
}

// Write the modified tree to a json file
objectMapper.writeValue(new File("emp-modified-array.json"), rootNode);

if (inputStream != null) inputStream.close();
```
