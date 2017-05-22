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

