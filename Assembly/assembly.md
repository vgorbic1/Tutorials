## Assembly

There is actually only one language ever needed, which is called "machine language" or "machine code". It looks like this:
```
0010000100100011
```
Assembly language was created as an exact shorthand for machine level coding, so that you wouldn't have to count *0*s and *1*s 
all day. It works the same as machine level code: with instructions and operands.

Each assembly language was created for just one processor or family of processors as the instructions mapped directly to 
opcodes run by the processor.

Assembly language has a ONE-TO-ONE relationship with machine language, meaning that each assembly language instruction 
corresponds to a single machine-language instruction. High-Level languages have a ONE-TO-MANY relationship with machine 
language. A single C++ statement expands to multiple machine instructions.
```
// C++
int Y;
int X = (Y + 4) *3;

// Assembly
mov eax, Y;   
add eax, 4;   
mov ebx, 3;
imul ebx; 		
mov X, eax;
```
Meaning:
```
mov eax,Y; 		mov Y to the EAX register
add eax,4; 		add 4 to the EAX register
mov ebx,3; 		mov 3 to the EBX register
imul ebx; 		multiply EAX by EBX
mov X,eax; 		mov EAX to X
```
Registers (e.g. EAX, EBX) are named storage locations in the CPU that hold intermediate results of operations.

### Portability
Any language whose SOURCE programs can be compiled and run on a wide variety of computer systems is said to be PORTABLE.
Java, for example, is very portable. Its major feature is that it can run on nearly any computer system. Assembly is **not
portable**, since it is designed for a specific processor family.

### x86
```
byte        8 bits
word        16 bits (2 bytes)
doubleword  32 bits (4 bytes)
quadword    64 bits (8 bytes)
```

### Mnemonic
- **mov**	Move (assign) one value to another
- **add** 	Add two values
- **sub**	Subtract one value from another
- **mul** 	Multiply two values
- **jmp**	Jump to a new location
- **call**	Call a procedure

Assembly instructions can have from zero to three operands.


