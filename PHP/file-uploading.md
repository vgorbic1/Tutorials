## File Uploading

Check whether your server supports uploads
```php
<?php phpinfo(); ?>
```
find ```file_uploads``` section.
- **max_execution_time** is the maximum number of seconds that a PHP script can run. If the script takes longer, PHP generates a fatal error. (Default 30)
- **max_input_time** is the maximum number of seconds thata PHP script is allowed to parse the $_POST and $_GET arrays, and file uploads. Very large uploads are likely to run out of time. (Default 60)
- **post_max_size** is the maximum permitted size of all _$POST data, including file uploads. (Default 8M)
- **upload_tmp_dir** is where PHP stores uploaded files until your script moves them to a permanent location. If no value is defined in php.ini, PHP uses the system default temporary directory.
- **upload_max_filesize** the maximum permitted size of a single upload file. (Default 2M)
