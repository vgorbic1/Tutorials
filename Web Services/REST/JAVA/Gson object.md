## Processing JSON with object model APIs in Gson
The main class in the Gson library that you will use for building an object model from the JSON data
is the `com.google.gson.Gson` class.

### Generating the object model from the JSON representation
This example demonstrates the Gson APIs for converting a JSON representation of a single
employee object into a Java object:
```java
// Other imports are removed for brevity
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;

// Get GsonBuilder object
GsonBuilder gsonBuilder = new GsonBuilder();

// Set date format for converting date presented in form (in JSON data) to java.util.Date
gsonBuilder.setDateFormat("yyyy-MM-dd");

// Get gson object
Gson gson = gsonBuilder.create();

// Read the json input file with current class's class loader emp.json contains JSON employee object
InputStream inputStream = getClass().getResourceAsStream("/emp.json");
BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));

// Convert JSON string to Employee object
Employee employee = gson.fromJson(reader, Employee.class);
```

### Generating the parameterized Java collection from the JSON representation
This example shows how to convert a JSON object array into a Java collection:
```java
// Step 1: Read emp-array.json
InputStream inputStream = getClass().getResourceAsStream(("/emp-array.json");
BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));

// Step 2: Define TypeToken
// Define a parameterized collection type to hold the List of Employees returned by Gson::fromJSon method call.
Type listType = new TypeToken<ArrayList<Employee>>(){}.getType();

// Step 3: Convert JSON array to List<Employee>
// Generates list of employees by calling Gson::fromJson()
Gson gson = new Gson();
List<Employee> employees = gson.fromJson(reader, listType);
```
### Generating the JSON representation from the object model
Gson has simplified APIs to convert the object model into the JSON content. Depending upon the type
of the object model, you can use either of the following APIs to get the JSON representation:
- To convert a Java object into JSON, you can call the toJson(Object src) method:
```java
// Get Employee object that needs to be converted into JSON
Employee emp = getEmployee();
Gson gson = new Gson();

// Create JSON String from Object
String jsonEmp = gson.toJson(emp);
```
- To convert a parameterized collection into a JSON string, you can use toJson(Object src,
Type typeOfSrc):
```java
// Get Employee list that needs to be converted into JSON
List<Employee> employees= getEmployeeList();
Gson gson = new Gson();

// Specify collection type that you want to convert into JSON
Type typeOfSource = new TypeToken<List<Employee>>(){}.getType();

// Create JSON String from Object
String jsonEmps = gson.toJson(employees, typeOfSource);
```
