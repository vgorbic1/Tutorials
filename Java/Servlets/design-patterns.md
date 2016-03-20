## Design Patterns Used with Servlets and JSP

#### Model 1 Pattern
The Model 1 pattern uses a JSP to handle both the request and response of the application. In addition, the JSP does all of the
processing for the application. To save the data of the business classes, the application maps the data to a database or files that can be called the data store for the application. This is also known as persistent data storage because it exists after the application ends.
![model1](https://cloud.githubusercontent.com/assets/13823751/13902206/bf11830a-ee0d-11e5-9b1f-9e8d413be87e.jpg)
Although the Model 1 pattern is sometimes adequate for applications that have limited processing requirements, this pattern is not recommended for most applications.


