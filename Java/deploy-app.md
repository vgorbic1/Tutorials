## Deploying and Application

Three ways of deployment:
1. Executable Jar (100% local)

2. Combination:

- Web Start
- RMI app

3. Servlets (100% remote)

#### JARS
The compiler has to generate class files for all inner classes including GUI event listeners. Separate source code (.java) and class files (.class)

Standard organizational scheme:

Using compiler flag –d (directory) that is responsible for which directory the compiled code lands in.

COMPILE YOUR CODE:
```
cd MyProject/source
javac –d ../classes *.java
```
RUNNING YOUR CODE:
```
cd MyProject/classes
java myJavaProgram
```
To bundle all classes use executable JAR (Java Archive) which is based on pkzip file format. The JAR should have a manifest file in it. 

CREATE MANIFEST FILE:

1) State which class has the main() method in the first line of the manifest.txt file: 
Main-Class: MyApp 
2) Press return after typing that line, otherwise the file may not work! 
3) Put manifest file into the classes directory.
4) Run the jar tool to create a JAR file:
cd MyProject/classes
jar –cvmf manifest.txt appl.jar *.class

EXECUTING JAR:
cd MyProject/classes
java –jar app1.jar
(The -jar flag tells JVM that you are giving it a JAR instead of a class)
On Windows or Mac OS just double click the app1.jar file. 








PACKAGING

1) To prevent name collisions, always put your own classes in a package and then jar it. Use your reverse domain name for a unique name for your package: com.headfirstjava.PackageExercise

2) Put the first statement in all your classes that will be in your package.
package com.headfirstjava;
import javax.swing.*;
public class PackageExercise {
…

COMPILE YOUR CODE:
cd MyProject/source
javac –d ../classes com/headfirstjava/*.java
(You need to create only the source branch of the folders, since the –d flag will automatically create the whole structure of the classes branch folders if it is not exist!) 

RUN YOUR CODE:
cd MyProject/classes
java com.headfirstjava.PackageExercise



JAR WITH PACKAGE:
1) Make sure all classes are within the correct package structure.
2) Create a manifest.txt file:
Main-Class: com.headfirstjava.PackageExercise 
Put the manifest file into the classes directory.
3) Run ajar tool to create a JAR file:
cd MyProject/classes
jar –cvmf manifest.txt packEx.jar com

EXTRACTING JAR WITH PACKAGE:
1) List the content of a JAR
jar –tf file.jar  (The –tf flag stands for Table File meaning to show the table of the current JAR file) 
2) Extract the contents of the JAR (unjar)
cd FolderWithTheJarFile
jar –xf file.jar (The –xf flag stands for Extract File)
When the contents are extracted you will see a META-INF folder with a MANIFEST-MF file in it.


JAVA WEB START
End-users launch a Java Web Start (JWS) application by clicking on a link in a Web page. Once the app downloads it runs outside the browser. Java Web Start app is just an executable JAR that is distributed over the Web. The JWS can detect when a part of application (even a single class) has changed on the server, then (without any end-user intervention) download and integrate the updated code. The JWS is set up as a simple HTML page with a link to the application.

THE WAY JWS WORKS:
1) The client clicks on a Web page link with MyApp.jnlp file (Java Network Launch Protocol) that describes your app.
2) The server sends the .jnlp file which is a XML document. (fully described in Head First Java p.599)
3) The browser starts a helper app that reads the .jnlp file and asks server for the MyApp.jar file.
4) The web server sends the requested .jar file.
5) Application starts by calling the specified main() method.

DEPLOYING JWS:
1) Make an executable JAR.
2) Write a .jnlp file.
3) Place the files on server
4) Add a new mime type to the server that will cause the server to send the .jnlp file with the correct header so every one knows what it is:
application/x-java-jnlp-file
5) Create a web page with a link to the .jnlp file.


RMI APPLICATION

RMI (Remote Method Invocation) use helpers, the objects that do the communicating between two heaps. The client object thinks it is calling a method on the remote service, because the client helper is pretending to be the service object. The client helper (stub) does not have any of the actual method logic, though. It only contacts the server, transfers information about the method call and waits for a return from the server. 
On the server side, the server helper (skeleton) receives the request from the client helper through a socket connection, unpacks the information about the call and invokes the real method on the real service object. 
Then the service helper gets the return value from the service, packs it up and ships it back through the socket output stream to the client helper. The client helper unpacks the information and returns the value to the client object. 

With RMI you don’t write any of the networking or I/O code. All that is done by RMI. The helpers talk to each other using either IIOP protocol or JRMP protocol.
JRMP is a native protocol made for Java-to-Java remote calls.
IIOP is the protocol for CORBA (Common Object Request Broker Architecture) and lets you make remote calls on non-Java objects. It is much more complicated than JRMP.

MAKING THE REMOTE SERVICE
(Instructions in Head First Java p.616-622)

SERVLETS

Servlets are Java programs that run on and with an HTTP web server. Most common use of J2EE technology is to mix servlets and EJBs (Enterprise Java Beans) together, where servlets are the client of the EJB. Servlets are using RMI to talk to the EJB. 

STEPS FOR MAKING AND A RUNNING SERVLET
1) The server should be configured to support servlets. Find where your servlet classes have to be placed. Check with ISP or hosting provider.
2) Package servlets classes into the servlets.jar and add it to your classpath. Without these classes it is impossible to compile servlets.
3) Write a servlet class by extending HttpServlet:
public class MyServletA extends HttpServlet {…}
4) Write an HTML page that invokes your servlet:
<a href=”servlets/MyServletA”>My servlet</a>
(Example can be found: Head First Java p.627)

