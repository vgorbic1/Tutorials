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

Add a file upload field to a form
```html
<form action="" method="post" enctype="multipart/form-data" name="uploadImage" id="uploadImage">
  <p>
    <label for="image">Upload image:</label>
    <input type="file" name="image" id="image" />
  </p>
  <p>
    <input type="submit" name="upload" id="upload" value="Upload" />
  </p>
</form>
```
Safari does not allow direct filename input!

#### $_FILES array
To test upload array use this script after the form:
```php
</form>
<pre>
 <?php
    if (array_key_exists('upload', $_POST)) {
		print_r($_FILES);
	}
  ?>
</pre>
```
If you don't do anything with the uploaded file immediately after uploading, PHP discards it.

It is important to checkthe MIME type before allowing the upload process to be completed.

**Errors**

- 0 Upload successful
- 1 File exceeds maximum upload size specified in php.ini
- 2 File exceeds size specified by MAX_FILE_SIZE embedded in the form
- 3 File only partially uploaded
- 4 Form submitted with no file specified
- 5 (Currently not defined)
- 6 No temporary folder
- 7 Cannot write file to disk
