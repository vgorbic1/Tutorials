## Processing JSON with Jackson Data Binding APIs

Jackson data binding is used to convert the JSON representation into and from Plain Old Java
Object (POJO) by using property accessors or annotations. With this API, you can either generate
generic collection classes or more specific Java objects for representing JSON data.

### Simple Jackson data binding with generalized objects
Sometimes, you may need to deal with highly dynamic JSON content where you may not be able to
map data to a specific Java object as the structure of the data changes dynamically. In such a scenario,
you can use the simple binding APIs offered by the Jackson framework. You will use the Java maps,
lists, strings, numbers, Booleans, and nulls for representing dynamic JSON data:
```java
String jsonString = "{\" firstName\":\"John\",\"lastName\":\"Chen\"}";
ObjectMapper objectMapper = new ObjectMapper();

// Properties will store name and value pairs read from jsonString
Map<String, String> properties = objectMapper.readValue(jsonString, new TypeReference<Map<String, String>>() { });
```

### Full Jackson data binding with specialized objects
If the JSON data format, which a client receives, is well structured, you can directly map the content
to a concrete Java class. For instance, you can create
an Employee class for representing the employee data presented in the JSON format as long as the
JSON content structure does not change.
```java
// emp.json file has following contents:
// {"employeeId":100,"firstName":"John","lastName":"Chen"}
ObjectMapper objectMapper = new ObjectMapper();
Employee employee = objectMapper.readValue(new File("emp.json"), Employee.class);
```
The next example demonstrates how you can create a Java collection containing the `Employee` objects
from a JSON array of `employees`.
```java
ObjectMapper objectMapper = new ObjectMapper();
CollectionType collectionType = objectMapper.getTypeFactory().constructCollectionType(List.class, Employee.class);
// "emp-array.json" file contains JSON array of employee data
List<Employee> emp = objectMapper.readValue(new File("emp-array.json"), collectionType);
```
To convert a Java object into the JSON representation, you can call the `writeValue(OutputStream
out, Object value)` method on `ObjectMapper`. The `writeValue()` method serializes any Java
value to JSON and writes it to the output stream present in the method call:
```java
// Get the employee object
Employee employee = getEmployeeEntity();

// Convert the object in to JSON and write to a file
objectMapper.writeValue(new File("emp.json"), employee);
```
