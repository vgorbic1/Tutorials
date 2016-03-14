## Maven
Maven is a project management and comprehension tool. Maven provides developers a complete build lifecycle framework. Development team can automate the project's build infrastructure in almost no time as Maven uses a standard directory layout and a default build lifecycle. Maven makes life of developer easy while creating reports, checks, build and testing automation setups.

Maven project structure and contents are declared in an xml file, pom.xml referred as Project Object Model (POM), which is the fundamental unit of the entire Maven system. Maven uses Convention over Configuration which means developers are not required to create build process themselves. Developers do not have to mention each and every configuration detail. Maven provides sensible default behavior for projects. When a Maven project is created, Maven creates default project structure. Developer is only required to place files accordingly and he/she need not to define any configuration in pom.xml.

#### Setup
* Maven is Java based tool, so the very first requirement is to have JDK installed on your machine. 
* Download Maven 3.3.3 from http://maven.apache.org/download.cgi
* Add M2_HOME, M2, MAVEN_OPTS to environment variables.
* Add Maven bin directory location to system path.

#### POM
POM stands for Project Object Model. It is fundamental Unit of Work in Maven. It is an XML file. It always resides in the base directory of the project as pom.xml. The POM contains information about the project and various configuration detail used by Maven to build the project(s). 

While executing a task or goal, Maven looks for the POM in the current directory. It reads the POM, gets the needed configuration information, then executes the goal. Before creating a POM, we should first decide the project group (groupId), its name(artifactId) and its version as these attributes help in uniquely identifying the project in repository.
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
   http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>

   <groupId>com.companyname.project-group</groupId>
   <artifactId>project</artifactId>
   <version>1.0</version>

</project>
```
There should be a single POM file for each project. All POM files require the project element and three mandatory fields: groupId, artifactId, version. 

All POMs inherit from a parent (despite explicitly defined or not). This base POM is known as the Super POM, and contains values inherited by default.

Maven use the effective pom (configuration from super pom plus project configuration) to execute relevant goal. It helps developer to specify minimum configuration detail in his/her pom.xml. Although configurations can be overridden easily.

An easy way to look at the default configurations of the super POM is by running the following command:
```
mvn help:effective-pom
```

#### Build Life Cycle



