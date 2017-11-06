## Basics
MangoDB name came from "Humongous Data" expression.
Distributive site: [mongodb.com](https://mongodb.com)

### Install Community Server
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

### Database commands
#### List all databases
```
show dbs
```
#### List the current database
```
db
```
#### Create database
```
use databasename
```
#### Create a user (with roles)
```json
db.createUser(
   {
     user: "accountUser",
     pwd: "password",
     roles: [ "readWrite", "dbAdmin" ]
   }
);
```
#### Create a collection (like a table in a relation database)
```
db.createCollection('collectionname');
```
#### List conllections in the current database
```
show collections
```

### CRUD commands
#### Insert document to collection
```
db.customers.insert({ ... });
// where { ... } is the document to insert
```
The document object may be for example:
```
{first_name: "John", last_name: "Doe"}
```
#### To see documents in collection
```
db.customers.find();
```
With some nice formatting:
```
db.customers.find().pretty();
```
#### Insert several docunents to collection
Use an array of documents:
```
db.customers.insert([
{first_name: "John", last_name: "Doe"},
{first_name: "James", last_name: "Bond", gender: "male"}
]);
```
you may add an extra property (like `gender` here) with no problem.
