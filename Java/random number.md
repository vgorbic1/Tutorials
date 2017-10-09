## Generate a Random Number
What is your minimum number? Make it MIN.

What is your maximum number? Make it MAX.

Enter both numbers as arguments for the main();
```java
public class Random {
  public static void main(String[] args) {
    int MIN = Integer.parseInt(args[0]);
    int MAX = Integer.parseInt(args[1]);
    // Since random() gives you a double, cast it to integer
    int r = MIN + (int)(Math.random() * MAX);
    System.out.println(r);
  }
}
```
