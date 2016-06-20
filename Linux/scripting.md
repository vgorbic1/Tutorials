## Scripting
There are usually several shells available:
- sh (Bourne Shell) is the original UNIX shell. It is located in ```/bin/sh``` system directory.
- bash (Bourne Again Shell) is the standard GNU shell for common users, located in ```/bin/bash```
- csh (C-shell) with the syntax resembling C language
- ksh (Kornshell) beginner's nightmare.

To see all shells available:
```
cat /etc/shells
```
To see default shell:
```
cat /etc/passwd
```
To switch shells type "change shell" command and the name of the new shell:
```
chsh bash
```
Start a script file with shebang and the path to interpreter.
```
#!/bin/bash
```
To identify the path to interpreter use ```which``` or look in a system path ```echo $PATH```. Make sure that the script has "executable" permission, at least 755.

To define variables and their values (no "$" needed):
```
name = 'Vlad'
```
To access the defined variable (need "$"):
```
echo $name
```
#### Command Line Arguments
There are several reserved variables to use with command line: 
```
$0 - defines the name of the script
$1, $2 ... $9 - define command line arguments
$# - number of command line arguments
$* - the list of all arguments
```
To save output of a command to a variable use a back tick "`" character:
```
name = `cat $1 | wc`
```
To read from the command line, use ```read``` command with a variable to put the value of data red:
```
read answer
if [$answer !='y']
  then
  exit
fi
```
####IF Statement
Basic condition logic:
```
if []
  then
  ...
  else
  ...
fi
```
