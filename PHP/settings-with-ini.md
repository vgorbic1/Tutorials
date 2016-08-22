##Using INI file for settings configuration
The INI (initialization) file format is the standard format for configuration files in the Windows operating system. PHP comes with a handy
```parse_ini_file()``` function that will greatly simplify the creation of our settings parser:
```
database.default.type = mysql
database.default.host = localhost
database.default.username = username
database.default.password = password
database.default.port = 3306
database.default.schema = prophpmvc
```
