## Date Time API

In Java 8 a whole new date time API was added. The new Java date time API is located in the Java package java.time which is part of the standard Java 8 class library. 
The date and time is represented by the number of seconds and nanoseconds since Jan. 1st 1970. The number of seconds can be both positive and negative and is represented by a long. The number of nanoseconds is always positive and is represented by an int.

The static method System.currentTimeMillis() returns the time since January 1st 1970 in milliseconds. The value returned is a long:
```
long timeNow = System.currentTimeMillis();
```
The returned long value can be used to initialize java.util.Date, java.sql.Date, java.sql.Timestamp and java.util.GregorianCalendar objects.
It is not the worlds most precise or fine grained timer!
It can be used to measure time:
```
long startTime = System.currentTimeMillis();
callOperationToTime();
long endTime   = System.currentTimeMillis();
long totalTime = endTime - startTime;
```
The variable totalTime will now contain the total time it took to execute the callOperationToTime() method.
The calculations listed earlier in this text are rather trivial yet tedious to do, and could be encapsulated in a Timer class:
```java
public class Timer {
  private long startTime = 0;
  private long endTime   = 0;
  public void start(){
    this.startTime = System.currentTimeMillis();
  }
  public void end() {
    this.endTime   = System.currentTimeMillis();  
  }
  public long getStartTime() {
    return this.startTime;
  }
  public long getEndTime() {
    return this.endTime;
  }
  public long getTotalTime() {
    return this.endTime - this.startTime;
  }
}
```
Here is an example of how to use it:
```java
Timer timer = new Timer();
timer.start();
callOperationToTime();
timer.end();
```

#### java.util.date
Use this class to represent date:
```
java.util.Date date = new java.util.Date();
```
You can access the date and time contained in a java.util.Date instance using the getTime() method:
```
java.util.Date date = new java.util.Date();
long time = date.getTime();
```
The methods to get the year, month, day of month, hour etc. are deprecated. Apparently the algorithms used internally were not entirely correct.

#### java.util.Calendar
Java's java.util.Calendar class is used to do date and time arithmetic. Whenever you have something slightly more advanced than just representing a date and time, this is the class to use.

Accessing Year, Month, Day etc:

The Calendar class has a couple of methods you can use to access the year, month, day, hour, minutes, seconds, milliseconds and time zone of a given date:
```java
Calendar calendar = new GregorianCalendar();
int year       = calendar.get(Calendar.YEAR);
int month      = calendar.get(Calendar.MONTH); 
int dayOfMonth = calendar.get(Calendar.DAY_OF_MONTH); // Jan = 0, not 1
int dayOfWeek  = calendar.get(Calendar.DAY_OF_WEEK);
int weekOfYear = calendar.get(Calendar.WEEK_OF_YEAR);
int weekOfMonth= calendar.get(Calendar.WEEK_OF_MONTH);
int hour       = calendar.get(Calendar.HOUR);        // 12 hour clock
int hourOfDay  = calendar.get(Calendar.HOUR_OF_DAY); // 24 hour clock
int minute     = calendar.get(Calendar.MINUTE);
int second     = calendar.get(Calendar.SECOND);
int millisecond= calendar.get(Calendar.MILLISECOND);
```

#### Instant
The Instant class in the Java date time API (java.time.Instant) represents a specific moment on the time line. The instant is defined as an offset since the origin (called an epoch). The origin is Jan. 1st 1970 - 00:00 - Greenwhich mean time (GMT).
```
Instant now = Instant.now();
```
#### Local Date
The LocalDate Java class is located in the java.time package, so its fully qualified class name is java.time.LocalDate. LocalDate instances are immutable, so all calculations on a LocalDate return a new LocalDate.
```java
LocalDate localDate = LocalDate.now();
int   year       = localDate.getYear();
Month month      = localDate.getMonth();
int   dayOfMonth = localDate.getDayOfMonth();
int   dayOfYear  = localDate.getDayOfYear();
DayOfWeek dayOfWeek = localDate.getDayOfWeek();
```
#### Local Time
You can create a LocalTime instance in several ways. The first way is to create a LocalTime instance that represents the exact time of now:
```
LocalTime localTime = LocalTime.now();
```

#### Local Date Time
The LocalDateTime class in the Java 8 date time API (java.time.LocalDateTime) represents a local date and time without any time zone information.
