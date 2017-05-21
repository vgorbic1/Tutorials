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

`Find` command is used to look for files by name, or part of a name. The `-name` flag is case sensitive, the `-iname` is not.

To find all files with a specific word in the current directory:
```
find . -name "*nametofind*"
```
To find files in the current directory by user:
```
find . -user scott
```
To find files by size that a larger than 10 MB:
```
find . -size +10M
```
To find files by name and type:
```
find . -name "*filename*" -type f
```
(f -regular file, d - directory, l - symbolic link, b - block special file, p - FIFO, s - socket)

To find files not accessed in last sixty days:
```
find /home/username/ -atime +60
```
(`-amin` - accessed in minutes ago,  `-cmin` - status changed in minutes ago, `- mmin` - data modified in minutes ago, `-atime` - accessed in hours ago, `-ctime` - status changed in hours ago, `-ntime` - data modified in hours ago).

To find files by name AND type (so name and type should be exactly as specified):
```
find . -name "*filename*" -a -type f
```
To find files by name OR size:
```
find . -name "*filename*" -o -size +10M
```
To find eveything else BUT NOT:
```
find . ! -name "*filename*"
```
To find a file and execute a command after it:
```
find . -name "*mp3* | xargs rm // removes all files that have mp3 at the end in the current directory
```
