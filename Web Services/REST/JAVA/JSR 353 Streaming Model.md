## JSR 353 Streaming Model

Streaming APIs are grouped in the javax.json.stream package in the JSR specification.
Streaming APIs read and write the content serially at runtime in accordance with client calls, which
makes them suitable for handling a large amount of data.

To refer to the complete list of the streaming APIs provided by JSR 353, visit
[http://docs.oracle.com/javaee/7/api/javax/json/stream/package-summary.html](http://docs.oracle.com/javaee/7/api/javax/json/stream/package-summary.html).

### Using sStreaming APIs to Parse JSON Data
This example illustrates the use of streaming APIs for converting a JSON array of the employee
objects present in the `emp-array.json` file into an appropriate Java class representation:
```json
[{"employeeId":100,"firstName":"John","lastName":"Chen","email":"john.chen@xxxx.com","hireDate":"2008-10-16"},
{"employeeId":101,"firstName":"Ameya","lastName":"Job","email":"ameya.job@xxx.com","hireDate":"2013-03-06"},
{"employeeId":102,"firstName":"Pat","lastName":"Fay","email":"pat.fey@xxx.com","hireDate":"2001-03-06"}]
```
The first step is to get the input stream for reading the `emp-array.json` file. Then, you can
create a `JsonParser` instance with the input stream, as follows:
```java
// Other imports are removed for brevity
import javax.json.stream.JsonParser;

// Read emp-array.json file that contains JSON array of employees
InputStream inputStream = getClass().getResourceAsStream("/emp-array.json");
JsonParser jsonParser = Json.createParser(inputStream);
```
Start parsing the content now:
```java
// Return true if there are more parsing states
while (jsonParser.hasNext()) {

  // Return the event for the next parsing state
  Event event = jsonParser.next();
  
  // Start of a JSON object, position of the parser is after'{'
  if (event.equals(JsonParser.Event.START_OBJECT)) {
    employee = new Employee();
    employeeList.add(employee);
  } else if (event.equals(JsonParser.Event.KEY_NAME)) {
    String keyName = jsonParser.getString();
    switch (keyName) {
      case "firstName":
        jsonParser.next();
        employee.setFirstName(jsonParser.getString());
        break;
      case "lastName":
        jsonParser.next();
        employee.setLastName(jsonParser.getString());
        break;
      case "email":
        jsonParser.next();
        employee.setEmail(jsonParser.getString());
        break;
      case "employeeId":
        jsonParser.next();
        employee.setEmployeeId(jsonParser.getInt());
        break;
      case "hireDate":
        jsonParser.next();
        // Convert date string (from JSON) into java.util.Date object
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
        Date hireDate = dateFormat.Parse(jsonObject.getString("hireDate"));
        employee.setHireDate(hireDate);
        break;
    }
  }
}
```
Remember that JsonParser parses JSON by using the pull parsing programming model. In this case,
the client application code controls the progress of parsing. The client calls `next()` on `JsonParser`
to advance the parser to the next state after processing each element.

### Using Streaming APIs to Generate JSON
