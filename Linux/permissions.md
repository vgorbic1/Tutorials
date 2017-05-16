## File Permissions
Who can change permissions?
- superuser (root user)
- owner of the file or directory
### Alphanumeric Representation:
Types of users:
```
u - user (owner)
g - group
o - other (the world)
```
Permission Letters and Their Meanings
```
r -read
w -write
x -execute

Permissions for directories:
r - you may read the content
w - you may write to the directory, crate files and other directories inside.
x - you may enter the directory (using cd command)

s -suid in place of x (Can execute file with owner's permission.)
s -sgid in place of x for a directory (A newly created files in a directory
  belong to the group that owns the directory.)
S -suid or guid but no x (Any user could execute the file with
  owners permission if suid is set or group permission if sgid
  set, but file is not executable.)
t -sticky bit (User cannot delete or rename files, unles he is
  the file's or containing directory's owner.)
T -sticky, but no x (User can only delete or rename files, but 
  cannot access to read files and subdirectories.)
```
The alphabetic method uses
a simple formula: the user group you want to affect (u, g, o); followed by a plus sign (+) to grant
permission, a minus sign (–) to remove permission, or an equal sign (=) to set exact permission;
followed by the letters (r, w, x, s, t) representing the permission you want to alter.
To view permissions:
```
ls -l
```
To change file permission using alphabetic notation (examples):
```
chmod g+w filename
chmod go+w filename
chmod o=r filename
chmod o= filename  //remove all permissions for others
```
The disadvantage to the alphabetic system is shown in the last example: If you want to make changes
to two or more user groups and those changes are different for each user group, you end up running
chmod at least two times.

### Numeric representation
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

owner group world
r w x r w x r w x
4+2+1 4+2+1 4+2+1

example:
 
530 = user: r-x, group: -wx, others ---
```
To change file permission using numeric notation:
```
chmod 530 filename
```
### Common Permissions:
```
400 -r-------- Owner can read, no one else can do anything
644 -rw-r--r-- Everyone can read, only owner can edit
660 -rw-rw---- Owner and Group can read and edit, but world can do nothing
664 -rw-rw-r-- Everyone can read, owner and group can edit
700 -rwx------ Owner can do everytnong, but no one else can do anything
744 -rwxr--r-- Everyone can read, only owner can edit and execute
755 -rwxr-xr-x Everyone can read and execute, only owner can edit
777 -rwxrwxrwx Not a good idea 
```
To change permissions recursively:
```
chmod -R 660 filename
```
To change directory permission:
```
chmod 400 directoryname
```
### sgid
If the shared directory is set to sgid, however, any new file created in that directory is still owned
by the user who created the file, but it’s also automatically assigned to the directory’s group.

To set sgid:
```
chmod g+s directoryname
 or
chmod 2755 directoryname // where 2 is sgid
```
### Sticky Bit
That means that the sticky bit is used on directories. After it is set on a folder, users cannot delete or
rename files in that folder unless they are that file’s owner or the owner of the directory that has the
sticky bit set on it. If the sticky bit isn’t set and the folder is writable for users, that also means that
those users can delete and rename any files in that directory. The sticky bit prevents that from happening.

You may see both a `t` and a `T` to indicate that the sticky bit is set. You see a `t` if the world
already had execute permissions (x) before you set the sticky bit, and a `T` if the world didn’t
have execute set before the sticky bit was put in place. The end result is the same, but the
capitalization tells you what was in place originally.

To set a sticky bit:
```
chmod +t directoryname
 or
chmod 1775 directoryname // where 1 is a sticky bit
```
