## Linking Files
- Hard link associate two or more files with the same inode.
- Soft link (symbolic link) is a small file that is a pointer to another file. It contais a path to a target file.

To create a symbolic link
```
ln -s targetfilename linkname
```
