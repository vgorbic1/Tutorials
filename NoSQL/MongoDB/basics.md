## Basics
Distributive site: [mongodb.com](https://mongodb.com)

## Install Community Server
- Download the .msi file from the website.
- Run the installation and change the path to install the MongoDB files (Custom) For example:
```
C:\mongodb\
```
- Create `data` and `log` directories inside the `mongodb` directroy.
- Inside 'data` directory create `db` directroy. This is where the database filesystem will be stored.
- And open command prompt as Administrator and navigate to the `bin` folder.
- Run the following setup command:
```
C:\mongodb\bin> mongod --directoryperdb --dbpath D:\mongodb\data\db --logpath D:\mongodb\log\mongo.log --logappend --rest --install
```
#### Start MongoDB service in Windows:
```
C:\mongodb\bin> net start MongoDB
```
#### Stop MongoDB service in Windows:
```
C:\mongodb\bin> net stop MongoDB
```
#### Launch MangoDB shell:
```
C:\mongodb\bin> mongo
```
If you get `Access is denied` message, that means you don't run cmd as Administrator, or your Anty-Virus software prevent the file from running.
