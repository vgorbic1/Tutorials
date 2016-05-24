## Ubuntu Basic Commands

#### COMMAND LINE GENERAL
To open terminal:
```
Ctrl+Alt+T
```
To open command line (tty1 virtual console):
```
Ctrl+Alt+F1
```
To get a full path to where you are now:
```
pwd
```
To exit session:
```
exit  	logout		Ctrl+D
```
Reboot the system:
```
sudo shutdown –r now		sudo shutdown –r 0
```
Shut down system:
```
sudo shutdown –h now		sudo shutdown –h 0	
```
Shut down system at 6pm with a message:
```
sudo shut down –h 18:30 "System is going down at 6:30pm."
```

#### READING DOCUMENTATION
To read a system manual about say, a "rm" (remove) command:
```
man rm		info rm
```
To read a manual about a topic you are looking for, for example "partition":
```
apropos partition
```
To find a command you are looking for, say "fdisk":
```
whereis fdisk
```

#### NAVIGATING FILE SYSTEM
Listing the content:
```
ls
```
Listing including hidden files:
```
ls –a
```
Listing including hidden files and descriptive info:
```
ls –al
```
Listing files with the newest on top:
```
ls –alt
```
To change directory:
```
cd somedir		cd full/path/to/somedir
```
To move to the parent directory:
```
cd ..
```
To return to your home directory:
```
cd 		cd ~		cd $HOME
```
