## Shell
### history
Every time you type a command in your shell, that command is saved in a file named
.bash_history in your home directory.

To see last 10 commands in command-line history:
```
history 10
```
### alias
After you create an alias, you simply type its name, and
the command (or commands) referenced by the alias runs. If a command is particularly
complicated or involves several lines, you should instead turn it into a script or function. You might find them in `.bashrc`, but you really should use `bash_aliases` instead.

To display all commands aliases:
```
alias
```
To create a new temporary alias:
```
alias lsd="ls -d */"
```
To remove it:
```
unalias lsd
```
To create a new permanent alias, add it to the `.bash_aliases` file. If there is no such file, add it to `.bashrc`:
```
alias lsd="ls -d */"
```
Some people discourage aliases that take a normal command and change its behavior, like
`alias rm="rm -i"`, because they say that you will get too dependent upon your alias and
will forget that it’s missing when you use another computer, potentially doing some damage. I
think that’s a pretty silly argument. If an alias makes things easier for you, use it. I’m sure that
you have enough brains to remember that a different machine won’t have your aliases on it.
### Functions
If you need something more complex than an alias but less complex than a script, you want a function.

There are two ways to declare a function. You could use the function command, followed by your
function name, with the commands you want to run in the function inside the curly braces { and }. Or
you can use a method that’s more comfortable to programmers in which you start with the function
name and then follow it with an empty pair of parentheses and then the curly braces.

#### Temporary Functions
Short, temporary functions can be created on a single line:
```
mkcd () { mkdir -p "$1"; cd "$1"; }
$ mkcd mynewdirectory
```
If you use the single-line method, then you must use semicolons after each command, even the last
one. `$1` in the function is a positional parameter that
is replaced with the first argument you type after the function name.

Multiline execution:
```
mkcd () {   // press enter
 mkdir -p "$1" // press enter
 cd "$1" // press enter
}
```
No matter how you create it, a function created via the command line lasts only as long as your shell
session is active. Log out, and your function, like the passenger pigeon, is gone.

To remove the function:
```
unset -f functionname
```
#### Permanent Functions
To create a new permanent function open `.bashrc` or `.bash_aliases` in a text editor or create a new file 
`.bash_functions` in your home directory and put there:
```
if [ -f ~/.bash_functions ]; then 
  source ~/.bash_functions
fi
```
To add a function to the file write in the file:
```
mkcd () { mkdir -p "$1"; cd "$1"; }
$ mkcd mynewdirectory
```
or
```
mkcd () {   // press enter
 mkdir -p "$1" // press enter
 cd "$1" // press enter
}
```
Save the file and close it. You now need to reload the `.bash_aliases` (if the function was written there) file for the new function to work, so run this command:
```
source ~/.bash_aliases
```
To display all functions you have to create a new function like this:
```
listfunc () {
for func in $(compgen -A function | grep -v _);
do
declare -f $func;
echo -e "\r";
done
}
```
Run `listfunc` and you will have a list of all your custom functions.

To remove the permanent function, just comment out (with #) or delete the lines in your function file. Save the file and reload teh bash.




