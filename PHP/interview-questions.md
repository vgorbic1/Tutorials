## Interview Questions

**What is the difference between $message and $$message?**

This $$message treats '$message' as its value. It is called variable variable, and (I believe) rarely used.

**What are the differences between require and include, include_once?**

- `require()` will stop executing code if it fails to find the required chunk of code.
- `include()` will still allow script to run if there is no chunk of conde to include.
- `include_once()` will include the chunk of code only once and ignore any following references to this code chunk.

**What is meant by nl2br()?**

This function replaces all newlines (\n) with HTML <br> element in the given string

**How can we encrypt the username and password using php?**
- Use MD5 function: md5("password");
- Use SHA1 function: sha1("password");

**What is the functionality of the function strstr and stristr?**
- `strstr()` looks for the first occurrence of the given parameter inside given string and return the rest: ```strstr('I found a perfect job!', 'perfect' ); will return perfect job!```
- `stristr()` is basically the same, but case-insensitive: ```stristr('I found a perfect job!', 'PERFECT' ); will return perfect job!```

**What is the functionality of the function htmlentities?**

This function is used to convert some characters to HTML. Used to sanitize strings: ```htmlentities('<>'); // will return &lt;&rt```

**What is the difference between the functions unlink and unset?**

`unlink()` deletes the file, `unset()` clears the content of the file.


