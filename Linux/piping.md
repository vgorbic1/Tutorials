## Piping
Piping provides ability to send data from one program to another feeding from left to the fight. To send data from one program to a file or any other output, use redirection.
To display only three lines in all list of file in current directory:
```
ls | head -3
```
it is possible to combine piping with redirection. 
To display only three lines in all list of file in current directory and save it to a file called "myoutput":
```
ls -al | head -3 > myoutput
