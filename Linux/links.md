## Linking Files

#### Hard Link
A hard link is just another name for the same file. Since each file has its own inode, a hard link points to the same node that the file has. Hard link has no its own inode.
- Associate two or more files with the same inode.
- Cannot be created for a directory.
- Cannot be created for a target file on a different filesystem.
- Moves with the target file.
- If target file name is changed, the hard link still works.

To create a hard link:
```
sudo ln targetfile linkname
```
To get a list of inodes in current directory:
```
ls -i
```

#### Soft Link (Symbolic Link or Symlink)
A soft link is a shortcut to the oringinal file and has its own inode.
- Contais a path to a target file.
- Points to the name of the file, not inode of the file.
- Can be created for a directory.
- Can be created for a target file on a different filesystem.
- Cannot be moved if the target file is moved. The link will be broken.
- Breaks if the target file name is changed.

To create a symbolic link
```
sudo ln -s targetfilename linkname
```
To create a symbolic link with the same name as the target directory (the link will be created in the current directory):
```
sudo ln -s /var/www
```
