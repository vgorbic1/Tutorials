## Data Validation
Whether or not the user data is validated on the client, it is always validated on the server.
#### The code for the JSP (index.jsp)
```java
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
  <form action='' emailList'' method='' post'' >
    <input type=''hidden'' name=''action'' value='' add'' >
   <label class="pad_top">Email:</label>􀀄􀀄􀀄􀀄􀀄􀀄􀀄􀀄􀀄-
   <input type="email" name="email" ;value="${user.email}"><br>
   <label class="pad_top">First Name:</label>�􀀄􀀄-
   <input type="text" name="firstName" ;value="${user.firstName}"><br>
   <label class= "pad_top" >Last Name: </label>􀀇􀀇􀀇􀀇􀀇-
   <input type="text" name="lastName" tvalue="${user.lastName}"><br>
   <label>&nbsp;</label>
   <input type="submit" value="Join Now" class="margin_left">
  </form>
</body>
</html>
```
