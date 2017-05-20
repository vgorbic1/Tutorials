## Search for Files, Commands, Directories
Ubuntu file database has all files in it. On your computer, though, you’re probably using `slocate` instead of `locate` as a soft link.

To search that database for files, programs, and directories:
```
locate filetofind
```
Same, but case insensitive:
```
locate -i filetofind
```

### Search Inside Text Files for Patterns
The `locate` command searches the names of files and directories, but it can’t search inside those
files. To do that, you use `grep`:
```
grep thewordtofind filename
```
Grep all by itself works with basic [regular expressions](https://github.com/vgorbic1/Tutorials/blob/master/Linux/regexp.md).

To search in several directories and see it conveniently:
```
grep -R wordtosearch directoryname * | less
```
To search for words and highlight the results:
```
grep --color=auto filetosearch
```
To search ignoting case:
```
grep -i wordtosearch dirname/*
```
To search exactly for the word:
```
grep -w wordtofind filename
```
To search the output of another commands for specific words:
```
ls -al | grep wordtofind
```
To search for words inside search results:
```
ls -al | grep widerangeresult | grep wordtofind 
```

### Find Command
While `locate` searches a database for files, which makes it fast but dependent upon a constantly updated database, `find`
searches for files on the fly using criteria that you specify. Since `find` has to parse through your file
structure, it’s much slower than `locate`, but you can do lots of things with `find` that aren’t possible with `locate`.





Find files not accessed in last sixty days:
```
find /home/username/ -atime +60
```
A general search tool for find packages. It returns a long list of packages:
```
sudo apt-cache search kde
```
