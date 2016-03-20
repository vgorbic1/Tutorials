## Design Patterns Used with Servlets and JSP

#### Model 1 Pattern
The Model 1 pattern uses a JSP to handle both the request and response of the application. In addition, the JSP does all of the
processing for the application. To save the data of the business classes, the application maps the data to a database or files that can be called the data store for the application. This is also known as persistent data storage because it exists after the application ends.

![model1](https://cloud.githubusercontent.com/assets/13823751/13902206/bf11830a-ee0d-11e5-9b1f-9e8d413be87e.jpg)

Although the Model 1 pattern is sometimes adequate for applications that have limited processing requirements, this pattern is not recommended for most applications.

#### Model 2 (MVC) Pattern
This pattern separates the code for the application into three layers: the model, the view, and the controller. As a result,
this pattern is also known as the Model-View-Controller pattern (MVC pattern). This pattern works better than the Model 1 pattern whenever the processing requirements are substantial.

In the MVC pattern, the model defines the business layer of the application. This layer is usually implemented by JavaBeans. This type of class defines the data for the business objects and provides the methods that do the business processing.

![model2](https://cloud.githubusercontent.com/assets/13823751/13902232/d7a4331c-ee0e-11e5-85fb-57d1676aa6ca.jpg)

The view defines the presentation layer of the application. Since it's cumbersome to use a servlet to send HTML to a browser, an MVC application uses HTML documents or JSPs to present the view to the browser. 

The controller manages the flow of the application, and this work is done by one or more servlets. To start, a servlet usually reads any parameters that are available from the request. Then, if necessary, the servlet updates the model and saves it to the data store. Finally, the servlet forwards the updated model to one of several possible JSPs for presentation.

Most applications need to map the data in the model to a data store. But the JavaBeans usually don't provide the methods for storing their own data. Instead, data access classes like the UserDB class provide those methods. That separates the business logic from the data access operations.

#### Post-Redirect-Get (PRG) Pattern
Parameters of POST request usually contain input data, which can change state of server application. Same data submitted twice may produce unwanted results. Submission of the same data more than once in a POST request is undesirable and got its own name: Double Submit problem. The answer to double submit problem is redirection. PRG pattern splits one request into two. Instead of returning a result page immediately in response to POST request, server responds with redirect to result page. Browser loads the result page as if it were an separate resource. After all, there are two different tasks to be done. First is to POST input data to the server. Second is to GET output to the client.
