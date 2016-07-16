##Singleton Pattern
The Singleton Pattern ensures a class has only one instance, and provides a global point of access to it. 
Whenever you need an instance, just query the class and it will hand you back the single instance. You can instantiate it in a lazy manner, which is especially important for resource intensive objects.

![singleton](https://cloud.githubusercontent.com/assets/13823751/16877217/a7eacb26-4a6c-11e6-9871-31d2daa2d231.jpg)

Singleton with lazy instantiation:
```java
public class Singleton {
    private static Singleton single;
    private Singleton() {}
    public static Singleton getSingle() {
        if (single == null) single = new Singleton();
        return singleton;
    }
}
```
For most Java applications, we need to ensure that the Singleton works in the presence of multiple threads. To avoid problems with multithreading use an eagerly created instance rather than a lazy instantiation. JVM guarantees that the instance will be created before any thread accesses the static single variable:
```java
public class Singleton {
    private static Singleton single = new Singleton();
    private Singleton() {}
    public static Singleton getSingle() {
        return single
    }
} 
```
Synchronize only the first time through using "double-checked locking" to improve performance. This does not work with Java versions before v.1.5:
```java
private class Singleton {
    private volatile static Singleton single;
    private Singleton() {}
    public static Singleton getSingle() {
        if (single == null) {
            synchronized (Singleton.class) {
                if (single == null) {
                    single = new Singleton();
                }
            }
        }
        return single;
    }
}
```
