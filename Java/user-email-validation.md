**Validate user name and email via web service

```java
package ...controller;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.ws.rs.core.MediaType;
import java.io.IOException;
import com.connorwaity.nickel.application.Nickel;
import com.connorwaity.nickel.entity.User;
import com.connorwaity.nickel.entity.UserRole;
import com.connorwaity.nickel.persistence.UserDao;
import com.connorwaity.nickel.persistence.UserRoleDao;
import com.sun.jersey.api.client.Client;
import com.sun.jersey.api.client.ClientResponse;
import com.sun.jersey.api.client.WebResource;
import com.sun.jersey.api.client.filter.HTTPBasicAuthFilter;
import com.sun.jersey.core.util.MultivaluedMapImpl;
import org.apache.log4j.Logger;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;

/**
 * Handles form data of sign up user to put user information into the database.
 */
@WebServlet(name = "SignUpUser", urlPatterns = { "/signUpUser" } )

public class SignUpUser extends HttpServlet {

    private final Logger log = Logger.getLogger(this.getClass());
    static String key;

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        Nickel nickel = (Nickel) getServletContext().getAttribute("nickel");
        key = nickel.getProperties().getProperty("mailgunKey");

        User user = new User();
        user.setUsername(req.getParameter("username"));
        user.setEmail(req.getParameter("email"));
        user.setPassword(req.getParameter("password"));

        boolean valid = validateEmail(user.getEmail());

        // if email is valid
        if (valid) {

            UserDao dao = new UserDao();

            // if username is taken
            // set error message
            if (dao.getIdFromUsername(user.getUsername()) >= 1) {
                req.setAttribute("error_message", "Username is already taken!");
                req.setAttribute("error", true);

                RequestDispatcher dispatcher = req.getRequestDispatcher("/signUp");
                dispatcher.forward(req, resp);
            } else {
                dao.addUser(user);
                UserRole userRole = new UserRole();
                userRole.setUser(req.getParameter("username"));
                userRole.setRole("user");
                new UserRoleDao().addUserRole(userRole);

                sendSignUpEmail(user.getEmail(), user.getUsername(), user.getPassword());

                RequestDispatcher dispatcher = req.getRequestDispatcher("/signIn" +
                        ".jsp");
                dispatcher.forward(req, resp);
            }
            // set error message
        } else {
            req.setAttribute("error_message", "Please enter a valid email!");
            req.setAttribute("error", true);
            RequestDispatcher dispatcher = req.getRequestDispatcher("/signUp");
            dispatcher.forward(req, resp);
        }
    }

    /**
     * Validates email, pass email string and tests against Mailgun, returns true if email is valid, and false if email is not valid
     * @param email email to be checked.
     * @return boolean validity of the email.
     */
    private boolean validateEmail(String email) {

        boolean valid = false;
        Client client = new Client();
        client.addFilter(new HTTPBasicAuthFilter("api",
                key));
        WebResource webResource =
                client.resource("https://api.mailgun.net/v3" +
                        "/address/validate");
        MultivaluedMapImpl queryParams = new MultivaluedMapImpl();
        queryParams.add("address", email);
        ClientResponse response = webResource.queryParams(queryParams).get(ClientResponse.class);
        try {
            JSONParser jsonParser = new JSONParser();
            Object object = jsonParser.parse(response.getEntity(String.class));
            JSONObject jsonObject = (JSONObject) object;
            valid = Boolean.valueOf(jsonObject.get("is_valid").toString());
        } catch (Exception e) {
            e.printStackTrace();
        }
        return valid;
    }

    /**
     * Get email username and password of user who has signed up, creates an email and sends it to them.
     * @param email Email of the user who has just signed up
     * @param username Username of the user who has just signed up
     * @param password User password, to be included in the email.
     * @return Client Response
     */
    public static ClientResponse sendSignUpEmail(String email, String username, String password) {
        Client client = Client.create();
        client.addFilter(new HTTPBasicAuthFilter("api",
                key));
        WebResource webResource =
                client.resource("https://api.mailgun.net/v3/sandboxb217a8a1956b42c48427f0f653874312.mailgun.org" +
                        "/messages");
        MultivaluedMapImpl formData = new MultivaluedMapImpl();
        formData.add("from", "Nickel <admin@nickel.com>");
        formData.add("to", email);
        formData.add("subject", "Hello");
        formData.add("html", "Thank you <i>" + username + "</i> for creating a Nickel account!");
        formData.add("html", "Your password is <i>" + password + "</i>.");
        return webResource.type(MediaType.APPLICATION_FORM_URLENCODED).
                post(ClientResponse.class, formData);
    }
}
```
