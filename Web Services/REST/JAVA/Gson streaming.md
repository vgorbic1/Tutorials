## Processing JSON with Gson streaming APIs
The streaming APIs in Gson follow the pull parser model.

### Reading JSON data with Gson streaming APIs
```java
// Step 1: Read emp-array.json file containing JSON array of employees
InputStream inputStream = getClass().getResourceAsStream("/emp-array.json");
InputStreamReader inputStreamReader = new InputStreamReader(inputStream);

// Step 2: Start parsing the contents List<Employee> employeeList = new ArrayList<Employee>();
JsonReader reader = new JsonReader(inputStreamReader);
reader.beginArray();
while (reader.hasNext()) {

  // The method readEmployee(...) is listed below
  
  Employee employee = readEmployee(reader);
  employeeList.add(employee);
}reader.endArray();
reader.close();

// This method is referred in the above code snippet to create Employee object
private Employee readEmployee(JsonReader reader) throws IOException {
  Employee employee = new Employee();
  reader.beginObject();
  while (reader.hasNext()) {
    String keyName = reader.nextName();
    switch (keyName) {
      case "firstName":
        employee.setFirstName(reader.nextString());
      break;
      case "lastName":
        employee.setLastName(reader.nextString());
      break;
      case "email":
        employee.setEmail(reader.nextString());
      break;
      case "employeeId":
        employee.setEmployeeId(reader.nextInt());
      break;
    }
  }
  reader.endObject();
  return employee;
}
```
### Writing JSON data with Gson streaming APIs
Use `com.google.gson.stream.JsonWriter` to write the JSON-encoded value to the stream:
```java
// Step 1: Build JsonWriter to read the JSON contents
OutputStream outputStream = new FileOutputStream("emp-array.json");
BufferedWriter bufferedWriter= new BufferedWriter(new OutputStreamWriter(outputStream));

// Create JsonWriter object
JsonWriter writer = new JsonWriter(bufferedWriter);

// Step 2: Start writing JSON contents
// Start with writing array
writer.beginArray();
List<Employee> employees = getEmployeesList();
for (Employee employee : employees) {
  // Start encoding the object
  writer.beginObject();
  // Write name:value pair to the object
  writer.name("employeeId").value(employee.getEmployeeId());
  writer.name("firstName").value(employee.getFirstName());
  writer.name("lastName").value(employee.getLastName());
  writer.name("email").value(employee.getEmail());
  // Finish encoding of the object
  writer.endObject();
}

// Finish encoding of the array
writer.endArray();
writer.flush();

// Close writer
writer.close();
```
