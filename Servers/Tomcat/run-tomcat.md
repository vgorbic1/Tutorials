## How to run Tomcat
Download the latest version of [Tomcat](http://tomcat.apache.org/).
#### Setup Apache Tomcat
* Unpack the binary distribution into a convenient location. For example in `C:\apache-tomcat` on Windows, or `/usr/local/apache-tomcat` on Linux/Unix.
* Set `CATALINA_HOME` environment variable pointing to the installation locations.

#### Start Tomcat
Tomcat can be started by executing the following commands on Windows machine, or you can simply double click on startup.bat:
```
 %CATALINA_HOME%\bin\startup.bat
```
Tomcat can be started by executing the following commands on Unix (Solaris, Linux, etc.) machine:
```
$CATALINA_HOME/bin/startup.sh
```
After a successful startup, the default web applications included with Tomcat will be available by visiting `http://localhost:8080/`.

#### Stop Tomcat
Tomcat can be stopped by executing the following commands on Windows machine:
````
%CATALINA_HOME%\bin\shutdown
````
Tomcat can be stopped by executing the following commands on Unix (Solaris, Linux, etc.) machine:
```
$CATALINA_HOME/bin/shutdown.sh
```
