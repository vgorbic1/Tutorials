## How to run Tomcat
Download the latest version of [Tomcat](http://tomcat.apache.org/).
#### Setup Apache Tomcat
* Unpack the binary distribution into a convenient location. For example in `C:\apache-tomcat` on Windows, or `/usr/local/apache-tomcat` on Linux/Unix.
* Set `CATALINA_HOME` environment variable pointing to the installation locations.

*Windows:*

Using command prompt:
```
set JAVA_HOME=C:\ "top level directory of your java install"
set CATALINA_HOME=C:\ "top level directory of your Tomcat install"
set PATH=%PATH%;%JAVA_HOME%\bin;%CATALINA_HOME%\bin
```
or you can do the same:
1. Go to system properties
2. Go to environment variables and add a new variable with the name JAVA_HOME and provide variable value as C:\ "top level directory of your java install"
3. Go to environment variables and add a new variable with the name  CATALINA_HOME and provide variable value as C:\ "top level directory of your Tomcat install"
4. In path variable add a new variable value as ;%CATALINA_HOME%\bin;

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
