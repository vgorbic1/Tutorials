## File Permissions
```
r -read
w -write
x -execute
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
To change permissions:
```
chmod 530 filename
```
