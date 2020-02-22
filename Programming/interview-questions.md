## Interview Questions
**What is ASCII chart?**

American Standard Code for Information Interchange stores characters of the English language in a computer’s 
memory by assigning a decimal value to each character and converting that to the binary number. ASCII used 
8-bit block of memory to store 128 characters where the first bit is a "dead" bit that is always 0.
```
A => [0100 0001] => (65 / 0x41)
z => [0111 1010] => (122 / 0x7A)
```
This chart was not globally accepted though since it represented only English characters.

**Why Unicode is a significant improvement to ASCII?**

UTF (Unicode Transformation Format) is a standard of globally accepted encoding schemes for information interchange. 
UTF provides the standard for encoding text in UTF-8, UTF-16 and UTF-32 encoding formats. Unlike ASCII, 
UTF-8 encoding use 8 bits or 1 byte to store a character. But since only 256 characters can be stored in 1 byte, 
UTF-8 uses maximum 4 bytes if a character needs more space to store its value.

**Is ASCII compliant with UTF-8?**

Since a character in ASCII encoding takes up 8 bits with the leading bit set to 0, UTF-8 does the same. In UTF-8 encoding, 
all ASCII compatible characters are saved in the ASCII format. Hence an ASCII reader program can parse UTF-8 encoded 
document with no problem.

**How UTF-8 adds more characters in the chart than ASCII?**

If a character is beyond the ASCII range (like a Chinese mandarin character), it will take more than 1-byte space. In that 
case, UTF-8 sets the leading bit to 1 to identify the non-ASCII character.

**What is extended-ASCII?**

Extended-ASCII encoding utilizes to the left-most bit (dead bit) to add another 128 characters to the set. But since 
this bit will be set to 1, the text file is no longer UTF-8 compatible.

**What are the code-points?**

A code-point is a decimal value given to each character. For example, the code-point of ASCII character A is 65. 
Code-point is different from Hexadecimal representation of the character. UTF has given each character ever in existence 
a fixed value and we identify the character in any encoding formats using this code-point.

**What is the code-point?**

Each byte (block) in UTF is called a code-unit. For example, character å. Unicode has assigned the code point value of 
229 for this character. In Hexadecimal, that would be E5. This character obviously can’t be stored in a single byte so it 
takes 2 code-units (2 bytes). In UTF-8 binary representation, it will look like 11000011 10100101.

**What is character set?**

A character set is a table that maps characters with their unique numbers. Encoding is how a character will be represented 
in binary numbers. So for example, in ASCII, the value of A will be stored in 7-bits. If an ASCII reader reads a value of 
65, it interprets that as character A. In the case of UTF, character set for UTF-8, UTF-16 and UTF-32 encoding is the same. 
That means, in each encoding, 65 means the character A. However, each encoding will read the data differently.
For UTF-8, it will consider blocks of 8-bits to construct a character. Similarly, UTF-16 will consider blocks of 16-bits 
or 2-bytes to construct a character.

**What is Typed Arrays in Javascript?**

The ES2015 version of JavaScript provides a few types of Array that can hold specific types of data.
Each element of a typed array is an integer number or a floating-point number. Depending on the type of a Typed Array, 
the value of a number must be between a specific range. For example, a 1-byte or 8-bits unsigned integer can have a
value between 0 and 255.

**What Typed Arrays are used for?**

Typed Arrays are primarily used to represent a chunk of memory in an array of bytes. For example, a 4-bytes 
or 32-bits chunk of memory can be divided into Int8Array or Uint8Array of length 4.  We can create an empty 
Typed Array using "new" keyword.

**What is an ArrayBuffer?**

JavaScript provides ArrayBuffer constructor to allocate a fixed-length binary-data buffer in memory. 
This constructor accepts the number of bytes to allocate in memory.
var buffer = new ArrayBuffer(4); // 4-bytes buffer

**What is Blob?**

A Blob is a file-like object of immutable raw-binary data but in memory.

