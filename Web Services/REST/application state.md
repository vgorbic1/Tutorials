## Application State Engine
Hypermedia as the Engine of Application State (HATEOAS) is a principle that the model of application changes from one state
to another by traversing the hyperlinks present in the current set of resource representations (the
model).

With REST, the client
just needs to know how to deal with the hypermedia links present in the response body; next, the call
to retrieve the appropriate resource representation is made by using these dynamic media links.

Here is an example illustrating the HATEOAS principle. In this example, the
`http://www.packtpub.com/resources/departments/IT` URI returns the following response to
the client:
```json
{"departmentId":10,
"departmentName":"IT",
"manager":"John Chen,
"links": [ {
 "rel": "employees",
 "href": "http://packtpub.com/resources/departments/IT/employees"
} ]"}
```
Now, to get the employees belonging to the department, the
client traverses the hyperlink present in the response body, namely
`http://www.packtpub.com/resources/departments/IT/employees`. This URI returns the
following employee list. The application state now changes into the following form (as represented
by the response content):
```json
[{"employeeId":100,
 "firstName":"Steven",
 "lastName":"King",
 "links": [ {
  "rel": "self",
  "href": "http://www.packtpub.com/resources/employees/100"
 }]
},
{"employeeId":101,
 "firstName":"Neena",
 "lastName":"Kochhar",
 "links": [ {
  "rel": "self",
  "href": "http://www.packtpub.com/resources/employees/101"
 }]
}]
```
