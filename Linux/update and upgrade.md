## Install, Update, Upgrade
In the Linux world, software
packages come in a variety of formats, with two in particular dominating: RPM and DEB. 
- RPM (Red Hat Package Manager) is used by distributions such as Red Hat, Fedora Core, SUSE, and other RPM-based distributions.
- DEB is used by Debian-based distributions such as Debian itself, Ubuntu and its many children, Linux Mint, Knoppix, and many others. 

Check repositories for any upgrades to the installed software:
```
sudo apt-get update
```
Insure that all dependencies get upgraded:
```
sudo apt-get dist-upgrade
```
All packages live in /var/cache/apt/archives.

Install new packages:
```
sudo apt-get install
```
To clean up unwanted old packages:
```
sudo apt-get clean	sudo apt-get autoclean
```
To permanently remove a package from the system (configuration files stay intact):
```
sudo apt-get remove
```
To remove the program files and configuration files:
```
sudo apt-get remove –purge
```
