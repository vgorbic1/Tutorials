## JSR 353 Object Model
This category of APIs generates an in-memory tree model for JSON data and then, starts processing it
as instructed by the client. This is conceptually similar to the Document Object Model (DOM) API
for XML.

Refer to the complete list of the object model APIs available in JSR 353 at
[http://docs.oracle.com/javaee/7/api/javax/json/package-summary.html](http://docs.oracle.com/javaee/7/api/javax/json/package-summary.html).

### Generating the object model from the JSON representation (Example)
This example uses the JSON array of the employee objects stored in the `emp-array.json` file as an
input source. The contents of this file are listed under the A sample JSON file representing employee
objects section:
```json
[{"employeeId":100,"firstName":"John","lastName":"Chen","email":"john.chen@xxxx.com","hireDate":"2008-10-16"},{"employeeId":101,"firstName":"Ameya","lastName":"Job","email":"ameya.job@xxx.com","hireDate":"2013-03-06"},{"employeeId":102,"firstName":"Pat","lastName":"Fay","email":"pat.fey@xxx.com","hireDate":"2001-03-06"}]
```
The first step is to read the JSON content from the `emp-array.json` file
and store it in an appropriate data structure:
```java
//Import statements for the core classes
import java.io.InputStream;
import javax.json.JsonArray;
import javax.json.JsonReade;

//Get input stream for reading the specified resource.
InputStream inputStream = getClass().getResourceAsStream("/emp-array.json");

// Create JsonReader to read JSON data from a stream
Reader reader = new InputStreamReader(inputStream, "UTF-8");
JsonReader jsonReader = Json.createReader(reader);

// Create an object model in memory.
JsonArray employeeArray = jsonReader.readArray();
```
Now, let's see how to convert `JsonArray` elements into specific object types. In this example, we
will convert each `JsonObject` present in `employeeArray` into the Employee object.
```
// All import statements are removed for brevity

public class Employee {
 private String firstName;
 private String lastName;
 private String email;
 private Integer employeeId;
 private java.util.Date hireDate;
 
// Getters and Setter for the above properties are not
// shown in this code snippet to save space
}
```
In this example, we create the `Employee` instance for each `JsonObject` present in `employeeArray`.
The following code snippet is a continuation of the previous example. This example converts
`employeeArray` that we retrieved from the JSON input file into a list of `Employe`e objects:
```java
// Import statements for the core APIs used in the following code snippet
import javax.json.JsonObject;
import javax.json.JsonValue;
import java.text.SimpleDateFormat;
import java.util.Date;

// Iterate over employeeArray(JsonArray) and process each JsonObject
List<Employee> employeeList = new ArrayList<Employee>();
for (JsonValue jsonValue : employeeArray) {

  // Get JsonObject and read desired attributes and copy them to Employee object
  if (jsonValue.getValueType().equals(JsonValue.ValueType.OBJECT)) {
    JsonObject jsonObject = (JsonObject) jsonValue;
    Employee employee = new Employee();
    employee.setFirstName(jsonObject.getString("firstName"));
    employee.setLastName(jsonObject.getString("lastName"));
    employee.setEmployeeId(jsonObject.getInt("employeeId"));
    
    // Convert date string (from JSON) to java.util.Date object
    SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
    Date hireDate = dateFormat.parse(jsonObject.getString("hireDate"))
    employee.setHireDate(hireDate);
    employeeList.add(employee);
  }
}
```
The preceding code iterates over the `JsonArray` instance and builds the `Employee` instances.

By now, we have read the entire JSON content from the input file into the `Employee` objects. It is now
time for some cleanup activities:
```java
if (inputStream != null) {
  inputStream.close();
}
if (jsonReader != null) {
  jsonReader.close();
}
```
Once you have finished using the `InputStream`, `OutputStream`, `JsonReader`, or `JSonWriter`
objects, make sure that you close them to release the associated resources.

### Generating the JSON representation from the object model
Convert a Java object model into the JSON format, which is the opposite of the previous operation.

The very first step is to build an object model. You can use either of the following classes to generate
the object model. The choice of the builder class depends on whether you want to generate a JSON
object or a JSON array:
- **javax.json.JsonObjectBuilder**: This builder class is used for generating the JSON object
model from scratch. This class provides methods to add the name-value pairs to the object
model and to return the final object.
- **javax.json.JsonArrayBuilder**: This builder class is used for generating an array of the JSON
objects from scratch. This class provides methods to add objects or values to the array model
and to return the final array.

The builder classes can be created either from the `javax.json.Json` factory class or from the
`javax.json.JsonBuilderFactory` class. You may go for `JsonBuilderFactory` if you want to
override the default configurations for the generated objects (configurations are specific to vendors)
or if you need to create multiple instances of the builder classes.

The following code snippet illustrates the use of the `JsonArrayBuilder` APIs for converting an array
of the employee objects into the JSON array. The client builds the JSON objects by using
`JsonObjectBuilder` and adds them to `JsonArrayBuilder`. Finally, when the client calls the
`build()` method, `JsonArrayBuilder` returns the associated JSON array:
```java
// import statements for the core classes used in this example
import javax.json.Json;
import javax.json.JsonArray;
import javax.json.JsonArrayBuilder;
import javax.json.JsonObject;
import javax.json.JsonObjectBuilder;
import javax.json.JsonWriter;
import java.io.FileOutputStream;
import java.io.OutputStream;

// Creates a JsonArrayBuilder instance that is Build JsonArray
JsonArrayBuilder jsonArrayBuilder = Json.createArrayBuilder();

// Get a list of Employee instances.
List<Employee> employees = getEmployeeList();

// Iterate over the employee list and create JsonObject for each item
for (Employee employee : employees) {
  // Add desired name-value pairs to the JSON object and push each object in to the array.
  jsonArrayBuilder.add(Json.createObjectBuilder()
    .add("employeeId", employee.getEmployeeId())
    .add("firstName", employee.getFirstName())
    .add("lastName", employee.getLastName())
    .add("email", employee.getEmail())
    .add("hireDate", employee.getHireDate())
  );
}

// Return the json array holding employee details
JsonArray employeesArray = jsonArrayBuilder.build();

// Write the array to file
OutputStream outputStream = new FileOutputStream("emp-array.json");
JsonWriter jsonWriter = Json.createWriter(outputStream);
jsonWriter.writeArray(employeesArray);

// Close the stream to clean up the associated resources
outputStream.close();
```
The resulting file output content may look like the following:
```json
[ {"employeeId":100,"firstName":"John","lastName":"Chen",
"email":"john.chen@xxxx.com","hireDate":"2008-10-16"},
{"employeeId":101,"firstName":"Ameya","lastName":"Job",
"email":"ameya.job@xxx.com","hireDate":"2013-03-06"}]
```
