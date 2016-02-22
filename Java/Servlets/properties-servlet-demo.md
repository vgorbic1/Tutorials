## Properties Servlet
```java
import java.io.*;
import java.util.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

/**
 * This is a simple servlet to show data
 * taken from properties file
 *
 *@author Vlad Gorbich
 */
@WebServlet (
    name = "propertiesServlet",
    urlPatterns = { "/properties-servlet" }
)
/**
 * This class contains the Servlet
 */
public class PropertiesServlet extends HttpServlet {

    private Properties properties;

    /** The method intitializes
     * loading Property List for the servlet.
     *
     * @throws ServletException
     */
    public void init() throws ServletException {
        loadProperties("/project2.properties");
    }

    /**
     * The method prints HTML page
     *
     * @param HttpServletRequest reqest from browser
     * @param HttpServletResponse response to browser
     * @throws ServletException
     * @throws IOException
     */
    public void doGet(HttpServletRequest request, HttpServletResponse response)
        throws ServletException, IOException {

        response.setContentType("text/html");

        PrintWriter out = response.getWriter();
        out.print("<!DOCTYPE html><html lang=\"en\">");
        out.print("<head><title>Properties Servlet</title>");
        out.print("<link href=\"style.css\" rel=\"stylesheet\" />");
        out.print("</head><body>");
        out.print("<h2>Properties Servlet</h2>");
        out.print("<table border=\"1\" " + "style=\"width:600px; border-collapse:collapse;\">");
        out.print("<tr><td>Author: </td>");
        out.print("<td>");
        out.print(properties.getProperty("author"));
        out.print("</td></tr>");
        out.print("<tr><td>Email: </td>");
        out.print("<td>");
        out.print(properties.getProperty("author.email.address"));
        out.print("</td></tr>");
        out.print("<tr><td>Course Title: </td>");
        out.print("<td>");
        out.print(properties.getProperty("course.title"));
        out.print("</td></tr>");
        out.print("<tr><td>Course Time: </td>");
        out.print("<td>");
        out.print(properties.getProperty("course.time"));
        out.print("</td></tr>");
        out.print("<tr><td>Course Instructor: </td>");
        out.print("<td>");
        out.print(properties.getProperty("course.instructor"));
        out.print("</td></tr>");
        out.print("<tr><td>Project Description: </td>");
        out.print("<td>");
        out.print(properties.getProperty("project.description"));
        out.print("</td></tr>");
        out.print("</table><br />");

        printProperties(out);

        out.print("<p><a href=\"/java112/\">Home</a></p>");
        out.print("</body></html>");
        out.close();
    }

    /**
     * The method prints HTML table with only properties data
     * @param out response variable
     */
    private void printProperties(PrintWriter out) {
        out.print("<table border=\"1\" " +
            "style=\"width:600px; border-collapse:collapse;\">");

        for (Map.Entry<Object, Object> entry : properties.entrySet()) {
            out.print("<tr><td>" + entry.getKey() + "</td>");
            out.print("<td>" + entry.getValue() + "</td></tr>");
        }

        out.print("</table>");
    }

    /**
     * The method loads properties from the properties file.
     * @param propertiesFilePath path to properties file
     */
    public void loadProperties(String propertiesFilePath) {
        properties = new Properties();
        try {
            properties.load(this.getClass().getResourceAsStream(propertiesFilePath));
        } catch(IOException ioException) {
            ioException.printStackTrace();
        } catch(Exception exception) {
            exception.printStackTrace();
        }
    }

}
```
This is the property file (just a plain text file):
```
author=Vlad Gorbich
author.email.address=example@site.com
course.title=Advanced Java
course.time=Tuesday 2:00
course.instructor=Instructor Name
project.description=Description \
of \
the project.
```
