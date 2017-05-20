## Search for Files, Commands, Directories
Ubuntu file database has all files in it. On your computer, though, you’re probably using `slocate` instead of `locate`.

To search that database for files, programs, and directories:
```
locate filetofind
```

Find files not accessed in last sixty days:
```
find /home/username/ -atime +60
```
A general search tool for find packages. It returns a long list of packages:
```
sudo apt-cache search kde
```
