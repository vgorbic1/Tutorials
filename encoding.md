## Encoding

- Text is always a sequence of bits which needs to be translated into human readable text using lookup tables. 
If the wrong lookup table is used, the wrong character is used.
- You're never actually directly dealing with "characters" or "text", you're always dealing with bits as seen through several layers of abstractions. 
Incorrect results are a sign of one of the abstraction layers failing.
- If two systems are talking to each other, they always need to specify what encoding they want to talk to each other in. The simplest example of this 
is this website telling your browser that it's encoded in UTF-8.
- In this day and age, the standard encoding is UTF-8 since it can encode virtually any character of interest, is backwards compatible with the 
de-facto baseline ASCII and is relatively space efficient for the majority of use cases nonetheless.

#### ASCII
To use bits to represent anything at all besides bits, we need rules. 
We need to convert a sequence of bits into something like letters, numbers and pictures using an encoding scheme, or encoding for short:
```
01100010 01101001 01110100 01110011
b        i        t        s
```
The above encoding scheme happens to be ASCII. A string of 1s and 0s is broken down into parts of eight bit each (a byte for short). 
The ASCII encoding specifies a table translating bytes into human readable letters:
```
bits	character
01000001	A
01000010	B
01000011	C
01000100	D
01000101	E
01000110	F
```
In total there are 128 characters defined in the ASCII encoding, which is a nice round number (for people dealing with computers), 
since it uses all possible combinations of 7 bits (0000000, 0000001, 0000010 through 1111111). ASCII does not use the first bit in a byte, 
so an ASCII character is represented by a byte, that always starts with 0.

**Character set**, (charset) is the set of characters that can be encoded. The ASCII encoding encompasses a character set of 128 characters.
 
**Code page** is a "page" of codes that map a character to a number or bit sequence. A.k.a. "the table".

Now that we know what we're talking about, let's just say it: 95 characters really isn't a lot when it comes to languages. It covers the basics 
of English, but what about writing a risqué letter in French? A Straßen­übergangs­änderungs­gesetz in German? 
An invitation to a smörgåsbord in Swedish? Well, you couldn't. Not in ASCII. There's no specification on how to 
represent any of the letters é, ß, ü, ä, ö or å in ASCII, so you can't use them.

#### Multi-Byte Encodings
To create a table that maps characters to letters for a language that uses more than 256 characters, one byte simply isn't enough. 
Using two bytes (16 bits), it's possible to encode 65,536 distinct values. [BIG-5](https://en.wikipedia.org/wiki/Big5) is such a double-byte encoding.
Instead of breaking a string of bits into blocks of eight, it breaks it into blocks of 16 and has a big (I mean, BIG) table that specifies which 
character each combination of bits maps to. BIG-5 in its basic form covers mostly Traditional Chinese characters. GB18030 is another encoding which 
essentially does the same thing, but includes both Traditional and Simplified Chinese characters.
```
bits	 character
10000001 01000000	丂
10000001 01000001	丄
10000001 01000010	丅
10000001 01000011	丆
10000001 01000100	丏
```

#### Unicode
Finally somebody had enough of the mess and set out to forge a ring to bind them all create one encoding standard to unify all encoding standards. 
This standard is Unicode. It basically defines a ginormous table of 1,114,112 code points that can be used for all sorts of letters and symbols. 
That's plenty to encode all European, Middle-Eastern, Far-Eastern, Southern, Northern, Western, pre-historian and future characters mankind knows 
about. So, how many bits does Unicode use to encode all these characters? **None**. Because Unicode is not an encoding.

Unicode first and foremost defines a table of code points for characters. That's a fancy way of saying "65 stands for A, 66 stands for B and 9,731 
stands for ☃". How these code points are actually encoded into bits is a different topic. To represent 1,114,112 different values, two bytes aren't 
enough. Three bytes are, but three bytes are often awkward to work with, so four bytes would be the comfortable minimum. But, unless you're actually 
using Chinese or some of the other characters with big numbers that take a lot of bits to encode, you're never going to use a huge chunk of those four 
bytes. If the letter "A" was always encoded to 00000000 00000000 00000000 01000001, "B" always to 00000000 00000000 00000000 01000010 and so on, any 
document would bloat to four times the necessary size.

To optimize this, there are several ways to encode Unicode code points into bits. UTF-32 is such an encoding that encodes all Unicode code points 
using 32 bits. That is, four bytes per character. UTF-16 and UTF-8 are variable-length encodings. If a character can be represented using a single 
byte (because its code point is a very small number), UTF-8 will encode it with a single byte. If it requires two bytes, it will use two bytes and 
so on. It has elaborate ways to use the highest bits in a byte to signal how many bytes a character consists of. This can save space, but may also 
waste space if these signal bits need to be used often. UTF-16 is in the middle, using at least two bytes, growing to up to four bytes as necessary.
```
character	encoding	bits
A	        UTF-8	    01000001
A	        UTF-16	    00000000 01000001
A	        UTF-32	    00000000 00000000 00000000 01000001
あ	        UTF-8	    11100011 10000001 10000010
あ	        UTF-16	    00110000 01000010
あ	        UTF-32	    00000000 00000000 00110000 01000010
```
Unicode is a large table mapping characters to numbers and the different UTF encodings specify how these numbers are encoded as bits. Overall, Unicode 
is yet another encoding scheme.

**Code Points** are characters, referred to by their "Unicode code point". Unicode code points are written in hexadecimal 
(to keep the numbers shorter), preceded by a "U+" (that's just what they do, it has no other meaning than "this is a Unicode code point"). 
The character Ḁ has the Unicode code point U+1E00. In other (decimal) words, it is the 7680th character of the Unicode table.

Any character can be encoded in many different bit sequences and any particular bit sequence can represent many different characters, 
depending on which encoding is used to read or write them. The reason is simply because different encodings use different numbers of bits per 
characters and different values to represent different characters:
```
bits	            encoding	     characters
11000100 01000010	Windows Latin 1	 ÄB
11000100 01000010	Mac Roman	     ƒB
11000100 01000010	GB18030	         腂
```

#### Problems
If you open a document and it looks like this:
```
ÉGÉìÉRÅ[ÉfÉBÉìÉOÇÕìÔÇµÇ≠Ç»Ç¢
```
it means that the text editor, browser, word processor or whatever else that's trying to read the document is assuming the wrong encoding. The 
computer always needs to be told what encoding some text is in. Otherwise it can't know.

Many times certain bit sequences are invalid in a particular encoding. The program you're opening it with may decide to silently discard any bytes 
that aren't valid in the chosen encoding, or possibly replace them with ```?```. There's also the "Unicode replacement character" &#65533; (U+FFFD) 
which a program may decide to insert for any character it couldn't decode correctly when trying to handle Unicode. 
If a document is saved with some characters gone or replaced, then those characters are really gone for good with no way to reverse-engineer them.

#### How To Handle Encodings Correctly?
Know what encoding a certain piece of text is in, then interpret it with that encoding. If you're writing an app that allows the user to input 
some text, specify what encoding you accept from the user. For any sort of text field, the programmer can usually decide its encoding. For any sort 
of file a user may upload or import into a program, there needs to be a specification what encoding that file should be in. Alternatively, the user 
needs some way to tell the program what encoding the file is in. This information may be part of the file format itself, or it may be a selection 
the user has make.

If you need to convert from one encoding to another, do so cleanly using tools that are specialized for that. Converting between encodings is the 
tedious task of comparing two code pages and deciding that character 152 in encoding A is the same as character 4122 in encoding B, then changing 
the bits accordingly. If your system needs to work with other encodings, convert them to Unicode upon input and convert them back to other encodings 
on output as necessary. 

#### UTF-8 And ASCII
The ingenious thing about UTF-8 is that it's binary compatible with ASCII, which is the de-facto baseline for all encodings. All characters available 
in the ASCII encoding only take up a single byte in UTF-8 and they're the exact same bytes as are used in ASCII. Any character not in ASCII takes up 
two or more bytes in UTF-8. For most programming languages that expect to parse ASCII, this means you can include UTF-8 text directly in your 
programs:
```
$string = "漢字";
```
Saving this as UTF-8 results in this bit sequence:
```
00100100 01110011 01110100 01110010 01101001 01101110 01100111 00100000
00111101 00100000 00100010 11100110 10111100 10100010 11100101 10101101
10010111 00100010 00111011
```
Only bytes 12 through 17 (the ones starting with 1) are UTF-8 characters (two characters with three bytes each). All the surrounding characters are 
perfectly good ASCII. A parser would read this as follows:
```
$string = "11100110 10111100 10100010 11100101 10101101 10010111";
```
To the parser, anything following a quotation mark is just a byte sequence which it will take as-is until it encounters another quotation mark. If 
you simply output this byte sequence, you're outputting UTF-8 text. No need to do anything else. The parser does not need to specifically support 
UTF-8, it just needs to take strings literally. Naive parsers can support Unicode this way without actually supporting Unicode. Many modern languages 
are explicitly Unicode-aware though.

#### Tools
If you need to convert a string from any other encoding to any other encoding, look no further than [iconv](http://www.php.net/manual/en/function.iconv.php).

#### Encoding with PHP
The whole issue of PHP's (non-)support for Unicode is that it just doesn't care. Strings are byte sequences to PHP. What bytes in particular doesn't matter.
PHP doesn't do anything with strings except keeping them stored in memory. PHP simply doesn't have any concept of either characters or encodings.
The only requirement PHP has of encodings is that PHP source code needs to be saved in an ASCII compatible encoding. The PHP parser is looking for certain 
characters that tell it what to do.

Any external file you process with PHP can be in whatever encoding you like. If PHP doesn't need to parse it, there are no requirements to meet to keep the 
PHP parser happy.
```
$foo = file_get_contents('bar.txt');
```
The above will simply read the bits in bar.txt into the variable $foo. PHP doesn't try to interpret, convert, encode or otherwise fiddle with the contents. 
The file can even contain binary data such as an image, PHP doesn't care.

#### Encoding with JavaScript
Javascript for example supports Unicode. In fact, any string in Javascript is UTF-16 encoded. In fact, it's the only thing Javascript deals with. You 
cannot have a string in Javascript that is not UTF-16 encoded. Javascript worships Unicode to the extent that there's no facility to deal with any 
other encoding in the core language. Since Javascript is most often run in a browser that's not a problem, since the browser can handle the mundane 
logistics of encoding and decoding input and output.
