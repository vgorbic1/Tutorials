## Update/ Upgrade
To upgrade or update software on Linux system use advanced package tool (APT).
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
