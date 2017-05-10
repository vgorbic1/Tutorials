## Work With Files
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
To move a level up:
```
cd ..
```
To go to home directroy:
```
cd 
```
To create a file:
```
touch filename.txt		touch directory/filename.txt
```
To create a directory:
```
mkdir directoryname		mkdir directory/directoryname
```
To create a directory several outer (parent) directories:
```
mkdir -p dirname/dirname/dirname
```
To delete an empty directory:
```
rmdir directoryname
```
#### Removing (Deleting) files

To delete a file in a directory:
```
rm filename
```
To remove and distroy the file immediately:
```
shred filename
```
To remove files with interaction (safe mode):
```
rm -i filename
```
To remove files without questons asked (fast but unsafe):
```
rm -rf directory/
```
To delete directory and all files in it:
```
rm –r /path/to/dirrectory/  or rm -R /path/to/dirrectory/
```
#### Moving (Renaming) files

To move file to the current directory:
```
mv file .
```
To move file to another directory:
```
mv file directory/
```
To rename a file:
```
mv oldfile.txt newfile.txt			mv directory/oldfile newfile
```
To copy a file:
```
cp oldfile newfile    cp directory/oldfile newfile
```
To copy a file and name it differently:
```
cp dircetory/oldfile archive/newfile
```
To copy all files in this directory to another:
```
cp * /another-directory
```
To copy all files with a specific extension:
```
cp *.jpg /another-folder
```
To copy a file from some directory to current one:
```
cp directory/filename .
```
To copy all files in chosen directory:
```
cp-r directory newdirectory
```

#### DISPLAY CONTENT OF A FILE
```
cat filename
less filename
nano filename
```
To display a content of the file starting from the bottom line and in reverse order:
```
tac filename
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
