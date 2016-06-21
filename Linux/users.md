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
New users, by default, are unprivileged. This means that they will only be able to modify files in their own home directory, which is what we want.

If this is your first new user, and you are currently logged in as the root user, you can use the following syntax to create a new user:
```
adduser newuser
```
If you are logged into a user that you added previously and gave sudo privileges, you can create a new user by invoking sudo with the same command:
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
If the user you created will be your primary user on the system, you usually want to enable sudo privileges so that you can do routine configuration and maintenance. We give users access to the sudo command with the visudo command. If you have not assigned additional privileges to any user yet, you will need to be logged in as root to access this command:
```
visudo
```
Once you have assigned sudo privileges to your user, you can access the same functionality from within your user's session by typing:
```
sudo visudo
```
When you type this command, you will be taken into a text editor session with the file that defines sudo privileges pre-loaded. We will have to add our user to this file to grant our desired access rights.

Find the part of the file that is labeled "User privilege specification". It should look something like this:
```
# User privilege specification
root    ALL=(ALL:ALL) ALL
```
We give a user sudo privileges by copying the line beginning with "root" and pasting it after. We then change the user "root" on the new line to our new user, like this:
```
# User privilege specification
root        ALL=(ALL:ALL) ALL
newuser    ALL=(ALL:ALL) ALL
```
We can now save the file and close it. By default, you can do that by typing Ctrl-X and then typing "Y" and pressing "Enter".

To see password status of any user account, enter:
```
passwd -S userNameHere
```
Sample outputs:
```
vivek P 05/05/2012 0 99999 7 -1
```
The status information consists of 7 fields as follows:
- vivek : Account login name (username)
- P : This field indicates if the user account has a locked password (L), has no password (NP), or has a usable password (P)
- 05/05/2012 : Date of the last password change.
- 0 : Password expiry minimum age
- 99999 : Password expiry maximum age.
- 7 : Password expiry warning period.
- -1 : Inactivity period for the password (see chage command for more information).

To get more info about password aging for a specific user called vivek, enter:
```
# chage -l vivek
```
Append a user to an existing group
```
sudo usermod -a -G <group-name> <username>
```
Check what groups the user belongs to
```
groups <username>
 or
id <username>
```
