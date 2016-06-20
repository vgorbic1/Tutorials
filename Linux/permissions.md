## File Permissions
Who can change permissions?
- superuser (root user)
- owner of the file or directory
```
r -read
w -write
x -execute
d -directory
```
To view permissions:
```
ls -l
```
File permission code:
```
0 ---
1 --x
2 -w-
3 -wx
4 r--
5 r-x
6 rw-
7 rwx
 
 example:
 
530 = user: r-x, group: -wx, others ---
```
To change file permission:
```
chmod 530 filename
```
Permissions for directories:
```
r - you may read the content
w - you may write to the directory, crate files and other directories inside.
x - enter the directory (using cd command)
```
To change directory permission:
```
chmod 400 directoryname
```
