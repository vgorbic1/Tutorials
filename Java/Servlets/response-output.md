##Simple output for Response
Use PrintWriter to print characters to the output:
```java
PrintWriter out = response.getWriter();
out.println("Some text and HTML");
```

Use OutputStream to write anything else (bytes):
```java
ServletOutputStream out = response.getOutputStream;
out.write(aByteArray);
```

**Example**
```java
public void doGet(HttpServletRequest request, 
        HttpServletResponse response) throws ServletException, IOException {
    response.setContentType("application/jar");

    ServletContext ctx = getServletContext();
    InputStream is = ctx.getResourceAsStream("/somefile.jar");

    int read = 0;
    byte[] bytes = new byte[1024];

    OutputStream os = response.getOutputStream();
    while((read = is.read(bytes)) != -1) {
        os.write(bytes, 0, read);
    }
    os.flush();
    os.close();
}  
```