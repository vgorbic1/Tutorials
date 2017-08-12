## Processing JSON with Jackson streaming APIs
The Jackson framework supports the streaming API for reading and writing JSON content.
Use `org.codehaus.jackson.JsonParser` to read the JSON data and
`org.codehaus.jackson.JsonGenerator` to write data.

### Using Jackson streaming APIs to parse JSON data
```java
// Step 1: Find a resource with a given name.
InputStream inputStream = getClass().getResourceAsStream("/emp-array.json");

// Create Streaming parser
JsonParser jsonParser = new JsonFactory().createParser(inputStream);

// Step 2: Start parsing the contents
// Use data binding feature from ObjectMapper for populating employee object
ObjectMapper objectMapper = new ObjectMapper();

// Continue the parsing till stream is opened or no more token is available
while (!jsonParser.isClosed()) {
  JsonToken jsonToken = jsonParser.nextToken();
  
  // if it is the last token then break the loop
  if (jsonToken == null) {
    break;
  }
  
  //If this is start of the object, then create Employee instance and add it to the result list
  if (jsonToken.equals(JsonToken.START_OBJECT)) {
    // Use the objectMapper to copy the current JSON object to Employee object
    employee = objectMapper.readValue(jsonParser, Employee.class);
    // Add the newly copied instance to the list
    employeeList.add(employee);
  }
}

// Close the stream after the use to release the resources
if (inputStream != null) { inputStream.close(); }
if (jsonParser != null) { jsonParser.close(); }
```

### Using Jackson streaming APIs to generate JSON data
```java
jsonGenerator.writeStartArray();
List<Employee> employees = getEmployeesList();
for (Employee employee : employees) {
  jsonGenerator.writeStartObject();
  jsonGenerator.writeNumberField("employeeId", employee.getEmployeeId());
  jsonGenerator.writeStringField("firstName", employee.getFirstName());
  jsonGenerator.writeStringField("lastName", employee.getLastName());
  jsonGenerator.writeEndObject();
}

// JsonGenerator class writes the JSON content to the specified OutputStream.
jsonGenerator.writeEndArray();

//Close the streams to release associated resources
jsonGenerator.close();
outputStream.close();
```
