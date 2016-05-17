## Accessing Files
If you store a file in a directory that's web accessible, such as the root directory for a web application, any user who enters the correct URL can access the file. However, the WEB-INF directory and its subdirectories aren't directly web-accessible. As a result, if you want to keep a file private, you can store it in the WEB-INF directory or one of its subdirectories. Or, you can restrict access to
the file or directory.
Code that gets the absolute path for a file:
```java
ServletContext sc = this.getServletContext();
String path = sc.getRealPath("/WEB-INF/EmailList.txt");
```
A more concise way to get the absolute path for a file:
```java
String path = this.getServletContext().getRealPath("/WEB-INF/EmailList.txt");
// A possible value for the real path variable:
// C:\vlad\build\web\WEB-INF\EmailList.txt
```
