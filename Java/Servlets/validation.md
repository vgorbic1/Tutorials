## Data Validation
Whether or not the user data is validated on the client, it is always validated on the server.
#### The code for the JSP (index.jsp)
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Java Servlets and JSP</title>
  <link rel="stylesheet" href="styles/main.css" type="text/css" />
</head>
<body>
  <hl>Join our email list</hl>
  <p>To join our email list, enter your name and email address below.</p>
  <p><i>${message}</i></p>
  <form action="emailList" method="post" >
    <input type="hidden" name="action" value="add" >
   <label class="pad_top">Email:</label>􀀄􀀄􀀄􀀄􀀄􀀄􀀄􀀄􀀄-
   <input type="email" name="email" ;value="${user.email}"><br>
   <label class="pad_top">First Name:</label>
   <input type="text" name="firstName" ;value="${user.firstName}"><br>
   <label class= "pad_top" >Last Name: </label>
   <input type="text" name="lastName" tvalue="${user.lastName}"><br>
   <label>&nbsp;</label>
   <input type="submit" value="Join Now" class="margin_left">
  </form>
</body>
</html>
```
#### A doPost method that validates the data
```java
@Override
protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
  String url = "/index.jsp";
  // get current action
  String action = request.getParameter("action");
  if (action == null) {
    action = "join"; // default action
  }
  // perform action and set URL to appropriate page
  if (action.equals("join")) {
    url = "/index.jsp"; // the "join" page
  }
  else if (action.equals("add")) {
    // get parameters from the request
    String firstName = request.getParameter("firstName");
    String lastName = request.getParameter("lastName");
    String email = request.getParameter("email");
    // store data in User object
    User user = new User(firstName, lastName, email);
    // validate the parameters
    String message;
    if (firstName == null || lastName == null || email == null ||
        firstName.isEmpty() || lastName.isEmpty() || email.isEmpty()) {
      message = "Please fill out all three text boxes.";
      url = "/index .jsp";
    } else {
      message = "";
      url = "/thanks .jsp";
      UserDB.insert(user);
    }
    request.setAttribute("user", user);
    request.setAttribute("message", message);
  }
  getServletContext().getRequestDispatcher(url).forward(request, response);
}
```
