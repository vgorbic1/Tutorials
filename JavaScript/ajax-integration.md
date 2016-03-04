## AJAX Integration
Use serverside code as a single piece of data, that will be handled by JavaScript. The serverside code may be written in PHP outputing a string:
```PHP
<?php
  echo "hello";
?>
```
as an xml string:
```PHP
<?php
  header('Content-type: application/xml');
  $output = "<users><user><id>1</id><name>bill</name></user><user><id>2</id><name>steve</name></user></users>";
  echo $output;
?>
```
as a JSON:
```PHP
<?php
  header('Content-type: application/json');
  $users = array(); 
  $users[] = array("id"=>1, "name"=>"bill");
  $users[] = array("id"=>2, "name"=>"steve");
  echo json_encode($users);
?>
```
or in Java as a servlet
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class Hello extends HttpServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/plain");
        PrintWriter out = response.getWriter();
        out.println("hello");
    }
}
```


