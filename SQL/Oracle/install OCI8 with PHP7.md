## Install PHP Oracle OCI Extension (11.2) on Mac OS X (10.11)

### Check if OCI8 is already installed
if the oci extension isn't installed, then you'll get a fatal error with 
```php
<?php function_exists('oci_connect'); ?>
```
### Preparation
Make sure that [PECL](https://pecl.php.net/) is installed on your machine.

Download the following files from [Oracle website](https://www.oracle.com/technetwork/topics/intel-macsoft-096467.html) (you need to create an account and accept terms):
```
instantclient-basic-macos.x64-11.2.0.3.0.zip
instantclient-sqlplus-macos.x64-11.2.0.3.0.zip
instantclient-sdk-macos.x64-11.2.0.3.0.zip
```

Unzip all theses files into a the directory 
```/usr/local/instantclient/11.2.0.4/```

This directory will look like:

```
.
├── BASIC_README
├── SQLPLUS_README
├── adrci
├── genezi
├── glogin.sql
├── libclntsh.dylib.11.1
├── libnnz11.dylib
├── libocci.dylib.11.1
├── libociei.dylib
├── libocijdbc11.dylib
├── libsqlplus.dylib
├── libsqlplusic.dylib
├── ojdbc5.jar
├── ojdbc6.jar
├── sdk
│   ├── SDK_README
│   ├── demo
│   ├── include
│   ├── ott
│   └── ottclasses.zip
├── sqlplus
├── uidrvci
└── xstreams.jar
```

### Create symlinks
```
ln -s /usr/local/instantclient/11.2.0.4/sdk/include/*.h /usr/local/include/
ln -s /usr/local/instantclient/11.2.0.4/sqlplus /usr/local/bin/
ln -s /usr/local/instantclient/11.2.0.4/*.dylib /usr/local/lib/
ln -s /usr/local/instantclient/11.2.0.4/*.dylib.11.1 /usr/local/lib/
ln -s /usr/local/lib/libclntsh.dylib.11.1 /usr/local/lib/libclntsh.dylib
```

### Install extension with pecl
```
pecl install oci8
```
If the script prompt you to provide the path to ORACLE_HOME directory, respond with:
```
instantclient,/usr/local/lib
```

If there is an error "cannot find library files" create direct symlinks to those liraries, for example:
```
ln -s /usr/local/instantclient/11.2.0.4/libnnz11.dylib /usr/local/lib/libnnz11.dylib
```
And your are done, normally pecl will automatically load the extension in your *php.ini*. If not, add the following line to your *php.ini*:

```
extension=oci8.so
```
Restart your HTTP Server and test.

Enjoy (or try to...)
