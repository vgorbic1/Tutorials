##Runnin Java

To run Java ```.jar``` file from the command prompt in Windows:
```
java -jar jar-file-name.jar
```
this will work when the created jar file is a runnable jar.
If you don't have a manifest in your jar use this command:
```
java -cp jar-file-name.jar full.package.name.ClassName
```
