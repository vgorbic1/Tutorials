## phpMyAdmin

#### Hide default databases
To hide default databases that are installed with phpMyAdmin in XAMPP or WAMPP
set the following in phpMyAdmin:
- Settings > Features > General > Hide databases 
- enter your value with regular expression, for example:
```
^(information_schema|performance_schema|mysql|phpmyadmin|test)$
```
