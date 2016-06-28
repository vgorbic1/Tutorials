## Partitions
Having several partitions provides higher security against disaster
- ```.data``` partition is a normal Linux data with root partition.
- ```.swap``` partition is an extra memory on hard drive.

Standard root partition has 100-500 MB. Standard instalation requires 250 MB. Swap partition is accessible only by the system and is hidden. You need 2 times of your RAM for a swap partition. Kernel sits on its own partition in ```/boot```.

To see info on partitions and theyr mount points:
```
df -h
```
To see a partition for the current folder:
```
df -h .
```

#### Inode
In a filesystem, a file represented by a inode. It is a serial number that contains info about the actual data that makes up the file. The inodes are stored in a special direcotry.

To see inode number:
```
ls -i
```
