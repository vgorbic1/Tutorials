## A Simple HTML Servlet
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

/**
 * This is a servlet that generates
 * some HTML output and an image link
 *
 *@author Vlad Gorbich
 */
@WebServlet (
    name = "first112Servlet",
    urlPatterns = { "/image-servlet" }
)
/**
 * This class contains the Servlet
 */
public class First112Servlet extends HttpServlet {

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
        PrintWriter  out  = response.getWriter();

        out.print("<!DOCTYPE html><html lang=\"en\">");
        out.print("<head><title>Image Servlet</title>");
        out.print("<link href=\"style.css\" rel=\"stylesheet\" />");
        out.print("</head><body>");
        out.print("<p>Vlad Gorbich</p>");
        out.print("<p>Java 112 / Advanced Java</p>");
        out.print("<p><img src=\"images/author.jpg\" /></p>");
        out.print("<p><a href=\"/java112/\">Home</a></p>");
        out.print("</body></html>");
        out.close();
    }

}
```
