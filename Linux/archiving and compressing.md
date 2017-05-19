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

To test archive whether it is become corrupted (if OK nothing will happen):
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
To test integrity of gzipped file (if OK nothing will happen):
```
gzip -t archivename.gz
```
To get detailed info:
```
gzip -lv archivename.gz
```

### Bzip2
Designed to supersede gzip, bzip2 creates
smaller files, but at the cost of speed. That said, computers are so fast nowadays that most users
won’t notice much difference between the time it takes gzip or bzip2 to compress a group of files.

To archive a file:
```
bzip2 filetoacrchive
```
Just like gzip, bzip2 leaves you with just the zipped file. The original file is gone.

To archive a file and leave the copy of the original:
```
bzip2 -k filetoarchive
```
To unzip the file:
```
bunzip2 archive.bz2
```
To unzp the file and leave the copy of the archive:
```
bunzip2 -k archive.bz2
```
To test the integrity of the archive (if OK nothing will happen):
```
bunzip2 -t archive.bz2
```
### Tar
"Tape archive" doesn’t compress; it merely archives (the resulting archives are known as tarballs). Instead, tar uses other programs, such as gzip or bzip2, to compress the archives that tar creates.

Flags | Means
-- | --
 c | create backup archive
 x | exract file from archive
 d | compare differences between archives
 u | update files in archive
 t | list the content of the archive
 f | file name. Should be right before the file name, if you use it
 p | preserve permissions
 z | do gzip compression
 j | do bzip2 compression
 v | verbose description

To tar all .txt files in the current directory:
```
tar -cf archivename.tar *.txt
```
To created an acrcive of a directory
```
tar -cf archivename.tgz directoryname
```
To create a tar file and compress it with gzip:
```
tar -pzcvf archivename.tar.gz directoryname/
```
To test the archive:
```
tar -zvtf archivename.tar.gz
```
To expand the content of compressed archive (test the file first!):
```
tar -pzvxf archivefile
```
To scroll through the archive file to look for the content:
```
tar -tzf archivefile | less
```
To unzip and untar a file into current directory:
```
tar -xzvf myfile.tar.gz
```
To add a file to archive:
```
tar -rvf archivename.tar myfilename
```
To delete a file from archive:
```
tar --delete file.txt -f archivename.tar
```
