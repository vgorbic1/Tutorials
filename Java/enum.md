## Enumerated List and toString();

Enum is a special Java class type used to define collections of constants. When you need a predefined list of values which do represent some kind of numeric or textual data, you should use an enum. You should always use enums when a variable (especially a method parameter) can only take one out of a small set of possible values. 

Why should we use enums?

If you use enums instead of integers (or String codes), you increase compile-time checking and avoid errors from passing in invalid constants, and you document which values are legal to use.

All enums implicitly extend ```java.lang.Enum```. Since Java does not support multiple inheritance, an enum cannot extend anything else.

Simple enum class:
```java
public enum Level {
    ONE, TWO, THREE
}
```
Refer to the constants above like this:
```
Level level = Level.ONE;
```
Iterate through an enum:
```
for (Level level : Level.values()) {
    System.out.println(level);
}
```
Enum fields:
```
public enum Level {
    HIGH  (3),  //calls constructor with value 3
    MEDIUM(2),  //calls constructor with value 2
    LOW   (1)   //calls constructor with value 1
    ; // semicolon needed when fields / methods follow
    private final int levelCode;
   private Level(int levelCode) {
        this.levelCode = levelCode;
    }
}
```
Enum methods:
```
public enum Level {
    HIGH  (3),  //calls constructor with value 3
    MEDIUM(2),  //calls constructor with value 2
    LOW   (1)   //calls constructor with value 1
    ; // semicolon needed when fields / methods follow
    private final int levelCode;
    Level(int levelCode) {
        this.levelCode = levelCode;
    }    
    public int getLevelCode() {
        return this.levelCode;
    }    
}
```
Call the method:
```
Level level = Level.HIGH;
System.out.println(level.getLevelCode());
```
