## System

#### System requirements
The root directory mounting point is located on ```/dev/hda2```

For Ubuntu we need at least 3GB pf disk space.

SWAP file should be 1.5 times your RAM, but no more than 2GB.

### System Structure
#### /bin
Contains essential command binaries. Usually contains bash, csh and commonly used commands like cp, mv, cat, ls and boot scripts. This directory has no other directories.

#### /boot
Contains static files of the boot loader and everything related to the boot process, except for configuration files.

#### /dev
Location of special or devices files. 
- block devices - are devices that store or hold data
- character devices - are devices that transmit or transfer data

#### /etc
A nerve center of the system. All system configuration files are here. Backup this directory regularly.

#### /home
All configuration files for a particular user. When a new user is created this dot-files are taken from ```/etc/skel```

#### /lib
Contains kernel modules and shared libraries. ```/lib/modules/``` is the home for all the kernel modules or drivers.

#### /lost+found
Contains all files that were recovered after system crash.

#### /media
Contains mount points for removable media. Before one can use a filesystem, it has to be mounted. The devicce file gives access to the raw contents of the disk, the mounted directory gives access to the files on the disk. All mounting is performed with superuser (root) rights.

#### /opt
Reserved for all the software and add-on packages that are not part of the default installation.

#### /proc
Virtual file system. It is a control and information system for kernel. There is no real files here.

#### /root
Home directory for sysadmin.

#### /sbin
Contains oly binaries essential for booting, recovering, adn repairing the system. Addition to the ```/bin```

#### /usr
Largest share of data. It has all the usr binaries, documentation, and libraries. User programs like telnet, ftp are also here. It is shareable read-only data. ```/usr/bin``` has the vast majority of user's binaries.

#### /var
Contains variable data that system can write into during operation. ```/var/log``` contains all system log files.

#### /srv
Contains site-specific data tgat seved by the system.

#### /tmp 
Contains most of the files that require only temporarily.
