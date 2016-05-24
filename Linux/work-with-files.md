## Work With Files
###SEARCHING THROUGH THE FILES AND PACKAGES
Ubuntu file database has all files in it. To search that database:
```
locate filetofind.txt
```
Find files not accessed in last sixty days:
```
find /home/username/ -atime +60
```
A general search tool for find packages. It returns a long list of packages:
```
sudo apt-cache search kde
```
#### FILE PERMISSIONS
To remove write permission from a file:
```
chmod a-w readme.txt		chmod 600 readme.txt
```
To change an owner of the file:
```
chown oneowner:anotherowner filename.txt
```
To create a file:
```
touch filename.txt		touch directory/filename.txt
```
To create a directory:
```
mkdir directoryname		mkdir directory/directoryname
```
To delete a directory:
```
rmdir directoryname
```
To delete a file in a directory:
```
rm filename.txt
```
To delete directory and all files in it:
```
rm –r /full/path/to/dirrectory
```
To move or rename a file:
```
mv oldfile.txt newfile.txt			mv directory/oldfile newfile
```
To copy a file:
```
cp directory/oldfile newfile
```
To copy a file and name it differently:
```
cp dircetory/oldfile archive/newfile
```

#### DISPLAY CONTENT OF A FILE
```
cat filename
less filename
nano filename
```

#### REDIRECTION
To redirect output use < and > or << and >>. If use < or > the file will be overridden. If use << and >> the output will append to any existing data.

To redirect output from a command to a new file use:
```
cat /proc/cpuinfo > file.txt
```
The file will be created (if it does not exist) and the output will be placed in that file. Any previous data will be erased.

To redirect from a file to a program:
```
cat < file.txt
```
- Standard input (stdin) 0
- Standard output (stdout) 1
- Standard error (stderr) 2
To redirect an error message to a log file:
```
anyunixcommand 2> error.log
```
Redirect to a bit bucket:
```
ls /tmp 2> /dev/nul
```

#### COMPARE FILES
To compare two files use:
```
diff fileone filetwo
```
The output will tell you what is a difference in content of those two files.

To find similarities between two files use:
```
comm fileone filetwo
```
The output will tell you what is content is identical.

#### COMBINING COMMANDS
To combine commands use a pipe: |

For example, for sorting files use:
```
sort names.txt | uniq
```
This command will remove all duplicate lines from the file.
