## Decorator Pattern
The Decorator Pattern attaches additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality. They use open-closed principle, which states that classes should be open for extension, but closed for modification. However, applying the open-close principle everywhere is wasteful, unnecessary, and lead to complex, hard to understand code.
Decorators have the same supertype as the objects they decorate. You can use one or more decorators to wrap an object. The decorator adds its own behavior either and/or after delegating to the object it decorates to do the rest of the job. Objects can be decorated at any time: dynamically at runtime with as many decorators as we like.

![decorator](https://cloud.githubusercontent.com/assets/13823751/16876857/4d3c9c78-4a6b-11e6-8eaa-b3bc6ffca51c.jpg)

So we are using inheritance to achieve the type matching, but we aren’t using inheritance to get behavior.
Java I/O classes (java.io) are based on decorators. You can write your own concrete decorator for FileInputStream abstract decorator. Say, you need a decorator that converts all uppercase characters to lowercase in the input stream:
import java.io.*;
```java
public class LowerCaseInputStream extends FilterInputStream {
	public LowerCaseInputStream(InputStream in) {
		super(in);
	}
	public int read() throws IOException {
		int c = super.read();
		return (c == -1 ? c : Character.toLowerCase((char)c));
	}		
	public int read(byte[] b, int offset, int len) throws IOException {
		int result = super.read(b, offset, len);
		for (int i = offset; i < offset+result; i++) {
			b[i] = (byte)Character.toLowerCase((char)b[i]);
		}
		return result;
	}
}
```
