## Redirecting
There three data streams in Linux:
- STDIN (0) Standard Input to a program
- STDOUT (1) Standard Output, printed by a program (defaults to terminal)
- STDERR (2) Standard Error, printed by a program (defaults to terminal)

#### Redirecting to a file:
```>``` shows that you want to save data into the file instead printing on terminal

To send the list of the directory to a (new) file output.txt rewriting the file:
```
ls > output.txt
```
To send the list of the directory to a (new) file output.txt appending to an existig data in the file:
```
ls >> output.txt
```
#### Redirecting from a file:
```<``` reads data from the file and sends it to the program via STDIN. File name is always on the right side!
The data sends ananymously, so the program never know from where it gets the data.

To count lines from the file myoutput.txt:
```
wc -l < myoutput.txt
```

#### Redirecting STDERR
```2>``` redirects error message from a program to a file.

To send error message to error.txt:
```
ls foo 2 > error.txt
```
To save data into a file and error message (if any) to terminal:
```
ls foo > myoutput.txt 2>&1
```
&1 means STDOUT
