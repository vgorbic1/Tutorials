##Using INI file for settings configuration
The INI (initialization) file format is the standard format for configuration files in the Windows operating system. PHP comes with a handy
```parse_ini_file()``` function that will greatly simplify the creation of our settings parser:
```
;db.config.ini file
[Production]
dbuser = matc
dbpass = abcdefg
dbloc = localhost
dbschema = matc
```
INI configuration files aren’t handled in the same way as PHP files, at least not in Apache. If a user tries to access an INI file, it will probably not be modified and the user could have access to sensitive configuration settings such as username and passwords. You should always take steps to deny access to these files, and it would be best to even store them outside of a web-accessible directory.
```php
public function getDB() {
  if (file_exists('/Web/dbconn/db.config.ini')) {
    $ini_array = parse_ini_file('/Web/dbconn/db.config.ini');
    if (array_key_exists('dbuser',$ini_array)
      && array_key_exists('dbpass',$ini_array)
      && array_key_exists('dbloc',$ini_array)
      && array_key_exists('dbschema',$ini_array)) {
      $dbuser = $ini_array['dbuser'];
      $dbpass = $ini_array['dbpass'];
      $dbloc = $ini_array['dbloc'];
      $dbschema = $ini_array['dbschema'];
    }
  }

  try {
    $dbHandler = new PDO("mysql:host=$dbloc;dbname=$dbschema", $dbuser, $dbpass);
    return $dbHandler;
  } catch(PDOException $e) {
    echo $e->getMessage();            
  }        
}
```
