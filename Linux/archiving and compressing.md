## Archiving and Compressing

### Zip
Around since 1989, and now ubiquitous on most commonly-used operating systems, zip both
archives and compresses files, thus making it great for sending multiple files as email attachments,
backing up items, or saving disk space.

To zip a file:
```
zip archivefinename.zip filetozip anotherfiletozip
```
To zip a directory:
```
zip archivedirname.zip dirtozip
```
To adjust a level of compression (from 0 - no compression to 9 - maximum compression):
```
zip -9 archivename.zip filetozip
```
Default is 6.

To password protect archive:
```
zip -e archivename.zip filetozip
```
Do not use -P for password protecting! The pass can be seen in user's bash history.

To extract a zip archive:
```
unzip archivename.zip
```
Use `-v` (verbose) flag for more information.

To test archive whether it is become corrupted:
```
unzip -t archivename.zip
```
To check the list of files in an archive:
```
unzip -l archivename.zip
```

### Gzip
Gzip is focused on compression, and was designed as an open-source replacement for an older UNIX program, *compress*. It’s
found on virtually every UNIX-based system in the world, including Linux and Mac OS X, but it’s not
present on Windows.

With zip, you need to specify the name of the
newly created zip file or zip won’t work; with gzip, though, you can just type the command and the
name of the file you want to compress.

When you gzip
a file, you’re left with only the new gzipped file. The original is gone.

To create a gzip archive:
```
gzip filetogzip
```
To create a gzip archive and leave the original file copy:
```
gzip -c filetoarchive > archivename.gz
```
To archive everything in the current directory (but not in sub directories):
```
gzip *
```
To archive everything in the current directory including sub directories:
```
gzip -r *
```
The gzip command cannot combine all the files into one big file, like you can
with zip. To do that, you need to incorporate tar.

To extract a gzip archive:
```
gunzip archivename.gz
```
Gunzip removes the .gz file, leaving you with the final gunzipped result.

To uszip a gzip archive and leave the original archive file:
```
gunzip -c archivename.gz > filename
```
To test integrity of gzipped file:
```
gzip -t archivename.gz
```
To get detailed info:
```
gzip -lv archivename.gz
```








#### Fast commands:

To archive a directory:
```
tar cvf file.tar directoryname/
```
To compress a tar file:
```
gzip file.tar
```
To unzip and untar a file:
```
tar zxvf file.tar.gz
```

#### Tar
"Tarchiver" creates compressed archives.

To created a compressed acrcive of a directory
```
tar czf compressed.tgz directoryname
```
To scroll through the archive file to look for the content:
```
tar tzf archivefile | less
```
To expand the content of compressed archive:
```
tar zxf archivefile
```

Flags:
- c create backup archive
- x exract file from archive
- d compare differences between archives
- u update files in archive
- t list the content of the archive
- f file name. Should be right before the file name, if you use it
- z do gzip compression
- v verbose description

To unzip and untar a file into current directory:
```
tar xzvf myfile.tar.gz
```
To add a file to archive:
```
tar rvf archivename.tar myfilename
```
To delete a file from archive:
```
tar --delete file.txt -f archivename.tar
```


