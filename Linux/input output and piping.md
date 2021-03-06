## Input and Output
There are three standard streams of data for Linux shell:
- standard input,
- standard output,
- standard error

Identifier | Name | Abbreviation | Typical Default
--- | --- | --- | ---
0 | Standard input | stdin | Keyboard
1 | Standard output | stdout | Terminal
2 | Standard error | stderr | Terminal

Instead of having output appear on the terminal, you can redirect it to another parogram. Or instead of acquiring input from
your typing, a program can get it from a file.

## Piping
Piping provides ability to send data from one program to another feeding from left to the fight. To send data from one program to a file or any other output, use redirection.

The pipe ```|``` takes the output from the first command and uses it as input for the second.

To display only three lines in all list of file in current directory:
```
ls | head -3
```
To redirect a command's output to a file , use ```>``` charavter:
```
ls -l > myfile.txt
```
If the file does not exist, it will be created. If it exists, the file will be overwritten.

it is possible to combine piping with redirection. 
To display only three lines in all list of file in current directory and save it to a file called "myoutput":
```
ls -al | head -3 > myoutput
