## Mounting
- Create a subdirectory in ```/mnt``` directory. Name the subdirectory whatever you  like. This is the directory where the harddrive will be mounted:
```
sudo mkdir /mnt/drive
```
- Find info about the hard drive that you are about to mount. It will list hard drives connected to the system. Look for something like ```/dev/sda5```
```
fdisk -l    (or)    mount
```
- To mount, write the following where the first path is the drive and the second path is the mount directory:
```
sudo mount /dev/sda5 /mnt/drive
```
- To unmount, just write the path of the drive:
```
sudo unmount /dev/sda5
```
- To mount a CD ROM:
```
sudo mount /dev/cdrom /mnt/cdrom
```
