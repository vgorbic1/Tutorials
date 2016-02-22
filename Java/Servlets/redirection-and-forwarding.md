## Redirection And Forwarding
- Forward is happening on the Server-side.
- Redirect is happening via HTTP and Browser.

#### Forwarding
Servlet or JSP uses the RequestDispatcher to transfer control. Control is transferred entirely on the server. 
No network traffic is involved. The user does not see the address of the destination JSP page!

![forwarding](https://cloud.githubusercontent.com/assets/13823751/13236851/b178ad62-d98c-11e5-973e-91ef652381ac.png)

Code to transfer with a forward:
```java
String url = "/transferDemo.jsp";
RequestDispatcher dispatcher =     
        getServletContext().getRequestDispatcher(url);
dispatcher.forward(request, response);
```

#### Redirection
Servlet use HTTP to transfer control. Control is transferred by sending the client a 302 status code and a Location response header. The transfer requires additional network traffic. The user sees the address of the destination page and can bookmark it.

![redirection](https://cloud.githubusercontent.com/assets/13823751/13236860/c712e9e4-d98c-11e5-8472-c1cf26a5c02f.png)

Code to transfer with a forward:
```java
String url = "/transferDemo.jsp";
response.sendRedirect(url);
```

