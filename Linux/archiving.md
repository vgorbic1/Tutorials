## Archiving

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

#### Gzip
To compress files only use gzip command.

To zip a file and rename it with .gz extension:
```
gzip -v filename
```
To test integrity of gzipped file:
```
gzip -tv filename.gz
```
To get detailed info:
```
gzip -lv filename.gz
```
To compress all files in the directory:
```
gzip -rv directoryname
```
To unzip:
```
gunzip -v filename.gz
```
