## Set up PHP 7.2 on macOS Mojave (with homebrew)

To check the version of PHP in the terminal, type the following command:
```
php -v
```
or can see what versions of PHP are installed with 
```
brew list | grep php
```
Maybe it’s worth cleaning up some of the old packages from brew. It’s up to you.

Make sure brew is up to date:
```
brew update
brew upgrade
```
Let’s finally install 7.2 version of PHP
```
brew install php@7.2
```
If you need to have this version of PHP first in your PATH run the following command:
```
echo 'export PATH="/usr/local/opt/php@7.2/bin:$PATH"' >> ~/.bash_profile
echo 'export PATH="/usr/local/opt/php@7.2/sbin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
```
And the result?
```
php --version
```
### Where is a php.ini file?

Your .ini file is located in /usr/local/etc/php/7.2/php.ini. To check just type
```
php --ini
```
### How to install extensions?

PHP extensions have been removed and now should be installed from PECL:
```
pecl install xdebug
```
