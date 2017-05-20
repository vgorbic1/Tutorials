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
Find files not accessed in last sixty days:
```
find /home/username/ -atime +60
```
A general search tool for find packages. It returns a long list of packages:
```
sudo apt-cache search kde
```
###Search Inside Text Files for Patterns
The `locate` command searches the names of files and directories, but it can’t search inside those
files. To do that, you use `grep`:
```
grep thewordtofind filename
```
Grep all by itself works with basic regular expressions.
