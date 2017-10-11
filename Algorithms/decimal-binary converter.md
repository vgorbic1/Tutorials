## Convert Decimal Number to Binary Code
```java
// Java
public class DecimalToBinary {
  public static void main(String[] args) {
    int n = Integer.parseInt(args[0]);
    String b = "";
    
    if (n == 0) System.out.print(0);
			
    while (n > 0) {
      int rem = n % 2; // 1 or 0
      b = rem + b; // put into correct order (last number displays first)
      n = n / 2;
    }
		
    System.out.print(b);
  }
}
```
