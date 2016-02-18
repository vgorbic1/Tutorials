##Annotations

Annotations are used to provide meta data for your Java code. They have no specific meaning in Java.

Simple annotation:
```
@Entity
```
Annotation with some value:
```
@Entity(tableName = "vehicles")
```
Single element annotation:
```
@InsertNew(value = "yes")
  // or just:
@InsertNew("yes")
```
Annotation with multiple elements:
```
@Entity(tableName = "vehicles", primaryKey = "id")
```
Annotation placement:
```
@Entity
public class Vehicle {
}
```
#### Built-in Java Annotations
Java comes with three built-in annotations which are used to give the Java compiler instructions: 
- The **@Deprecated** annotation is used to mark a class, method or field as deprecated, meaning it should no longer be used:
```java
@Deprecated
/**
  @deprecated Use MyNewComponent instead.
*/
public class MyComponent { … }
```
- The **@Override** annotation is used above methods that override methods in a superclass. If the method does not match a method in the superclass, the compiler will give you an error.
```java
public class MySuperClass {
    public void doTheThing() {
        System.out.println("Do the thing");
    }
}

public class MySubClass extends MySuperClass{
    @Override
    public void doTheThing() {
        System.out.println("Do it differently");
    }
}
```
- The **@SuppressWarnings** annotation makes the compiler suppress warnings for a given method.
```java
@SuppressWarnings
public void methodWithWarning() { … }
```

#### Custom annotations
Annotations are defined in their own file, just like a Java class or interface:
```java
@interface MyAnnotation {
    String   value();
    String   name();
    int      age();
    String[] newNames();
}
```
To use the above annotation, you could use code like this:
```java
@MyAnnotation(
    value="123",
    name="Jakob",
    age=37,
    newNames={"Jenkov", "Peterson"}
)
public class MyClass { … }
```
