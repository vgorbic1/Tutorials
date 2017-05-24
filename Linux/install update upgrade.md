## Install, Update, Upgrade
In the Linux world, software
packages come in a variety of formats, with two in particular dominating: RPM and DEB. 
- RPM (Red Hat Package Manager) is used by distributions such as Red Hat, Fedora Core, SUSE, and other RPM-based distributions.
- DEB is used by Debian-based distributions such as Debian itself, Ubuntu and its many children, Linux Mint, Knoppix, and many others. 

The `rpm` command works with software installers that end in `.rpm`. To install an RPM package, you need to download it first.

To find out which RPM packages are installed on the system:
```
rpm -qa
```
To install an RPM package:
```
rpm -Uhv packagename.rpm
```
If a package already exists on your system and you’re trying to put a newer one on your machine, `-U` performs an upgrade; if a package doesn’t already exist on your system, `-U` notices that and instead installs it. `-h` is to show hash marks so you can watch the progress of the install, and `-v` is to be verbose and tell what it is doing.

To install many packages:
```
rpm -Uhv packagename.rpm anotherpackage.rpm
```
To install kernel use `-i` option instead of `-U` option, to keep a copy of the old kernel.

To remove an RPM package:
```
rpm -e pqckagename
```
The `yum` command installs, upgrades, and uninstalls software packages by acting as a wrapper around RPM. In addition, YUM automatically handles dependencies for you.

To install an RPM package with dependencies:
```
yum install packagename
```
To remove a package:
```
yum remove packagename
```
To list installed packages:
```
yum list installed
```
To update installed packages:
```
yum update
```
To install Debian-based packages:
```
dpkg -i packagename.deb
```
To remove a Debian-based package:
```
dpkg -r packagename
```
To list installed Debian-based packages:
```
dpkg -l
```
to install a new Debian-based package and its dependencies use apt (Advanced Package Tool):
```
sudo apt-get install package
```
To check repositories for any upgrades to the installed software:
```
sudo apt-get update
```
Insure that all dependencies get upgraded:
```
sudo apt-get upgrade
```
All packages live in /var/cache/apt/archives.

To join both commands create an elias in a `.bash_aliases` file:
```
alias upgrade='apt-get update && apt-get upgrade'
```
Reload the `.bash_aliases` file and type "upgrade" to execute the command.

To automatically install new software and remove installed packages that are no longer needed:
```
sudo apt-get dist-upgrade
```
To see the list of all packages:
```
sudo apt --installed list
```
To clean up unwanted old packages:
```
sudo apt-get clean	// removes all current .deb files
sudo apt-get autoclean // removes only obsolete packages
```
To permanently remove a package from the system (configuration files stay intact):
```
sudo apt-get remove
```
To remove the program files and configuration files:
```
sudo apt-get remove -–purge
```
