##Set up Bootstrap and jQuery webjars
Bootstrap and jQuery may be installed as Maven (or Gradle) dependencies.
- Put necessary dependencies into pom.xml file.
```xml
<!-- Webjars for jquery and bootstrap -->

<dependency>
  <groupId>org.webjars</groupId>
  <artifactId>bootstrap</artifactId>
  <version>3.3.6</version>
</dependency>

<dependency>
  <groupId>org.webjars</groupId>
  <artifactId>jquery</artifactId>
  <version>2.1.4</version>
</dependency>
```
