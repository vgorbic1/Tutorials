## Text File Editors

To get the file's type:
```
file filename
```
To see frist 10 lines of a file:
```
head filename
```
To see last 10 lines of a file:
```
tail filename
```
To see last 10 lines interactively:
```
tail -f filename
```
To view file in stdout:
```
cat fiename
```
Cat is actualy concatenate files. The original purpose of the command is to concatenate two or more files together and print them of the screen:
```
cat filename anotherfilename
```
To concatenate files backward:
```
tac filenaeme anotherfilename
```
### Less
Less command is a pager, not an editor. It displays text files one page at a time.

To open a file with less:
```
less filename
```
Navigation in Less:

Command | Action
---|---
PgDn or Spacebar | forward one page
PgUp | back one page
Down arrow | forward one line
Up arrow | back one line
Right arrow | Scroll right
Left arrow | Scroll left
q | Quit

Search:

Command | Action
---|---
/pattern | search forward for pattern using regex
n | repeat search forward
N | repeat search backward

### Nano
```
nano file.txt
```
&uarr; &darr; page up or down

### Vi
```
vi file.txt
```
insert/editing mode:
- i - go to edit mode (insert text).
- a - append text in edit mode.
- esc - toggle out of insert mode.
- : - before entering a command
- h j k l - cursor movement.
- x - delete character.
- dd - delete line.
- :q - quit the program.
- :w - save the file.
