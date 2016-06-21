## User Operations

In order for a user to use SUDO the user account must belong to the admin group and also be listed in /etc/sudoers file, with permission 440. 

The whole point of SUDO is to grant you someone else's privileges (usually root) without asking for this other account's password (unlike su).

To get access to SUDO if you lost it completely:
- Hold down Shift while the computer I booting.
- When GRUB appears use down-arrow key to go to recovery mode and press Enter. 
- Select the menu entry for Root: "Drop to root shell prompt"
- Remount the file system: 
```
root@computer: ~# mount –o rw, remount
```
If there is no user account:
```
adduser username admin
```
If permission on sudores file was changed:
```
chmod 440 /etc/sudoers
```
To edit or look at SUDO configuration file (/etc/sudoers):
```
sudo vi sudo
```
To add another user to sudo group, modify the /etc/group file and add:
```
sudo:x: 27: vlad, newuser
```
To use a root account:
```
su –
```
To change back to your account:
```
su – vlad
```
To change the root password:
```
sudo passwd
```
To create a user:
```
sudo useradd newusername	
```
To create a user with all necessary folders:
```
sudo useradd –m newusername
```
To create a password for the new user:
```
sudo passwd newusername
```
To delete user, home directory, and mail:
```
sudo usrdel –r username
```
To delete a user with all folders and entries:
```
sudo deluser –remove-all-files –remove-home usernametodelete
```
To list the most recent successful logins:
```
last
```
To list the most recent unsuccessful logins:
```
sudo lastb
```
To list who is currently logged in:
```
who –u		users			who am i
```

**Change file owner**
```
sudo chown <new-username> <file-to-change>
```
**Change directory owner including all files in the directory**
```
sudo chown -R <new-username> <directory-to-change>
```
**Append a user to an existing group**
```
sudo usermod -a -G <group-name> <username>
```
**Check what groups the user belongs to**
```
groups <username>
 or
id <username>
```
