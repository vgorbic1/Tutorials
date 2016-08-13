## ENCRIPTING
What if you want to encrypt and decrypt data that's not being stored in a database?
Use ```MCrypt``` for this. You need to install MCrypt library for this, and configure PHP to support it.
First define which algorithm and mode to use.
```php
$m = mcrypt_mode_open('rijndael-256', '', 'cbc', '');
```
Here, rijndael-256 (Advanced Encryption Standard) algorithm is used. It stands up to US government standards.

The mode is Cipher Block Changing (CBC). Best for encrypting blocks of text.

Now, create an Initialization Vector (IV), which is required, optional, or unnecessary, depending on the mode being used:
```php
$iv = mcrypt_create_iv(mcrypt_enc_get_iv_size($m), MCRYPT_DEV_RANDOM);
```
Create buffers for encryption:
```php
mcrypt_generic_init($m, $key, $iv);
```
Where $key is a hard to guess string of particular length. For Rijndael cipher we are using 256-bit key, so 256/8 = 32. We need a 32-character string. You can randomize the key even more using md5() which returns exactly 32-character string:
```php
$key = md('some string');
```
Now, encrypt data:
```php
$encrypted = mycypt_generic($m, $data);
```
Close all buffers and modules:
```php
mcrypt_generic_deinit($m);
mcrypt_module_close($m);
```
For this example, I'm going to store an encrypted value in the session. The data will be decrypted in the subsequent example. The key and data to be encrypted will be hard-coded into this script. In addition, because the same key and IV are needed to decrypt the data, the IV will also be stored in the session without any security issues.
```php
<?php /* This page uses the MCrypt library
 *	to encrypt some data.
 *	The data will then be stored in a session,
 *	as will the encryption IV. */
// Start the session:
session_start(); ?>
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>A More Secure Session</title>
</head>
<body>
<?php // Encrypt and store the data...
// Create the key:
$key = md5('77 public drop-shadow Java');
// Data to be encrypted:
$data = 'rosebud';
// Open the cipher:
// Using Rijndael 256 in CBC mode.
$m = mcrypt_module_open('rijndael-256', '', 'cbc', '');
// Create the IV:
// Use MCRYPT_RAND on Windows instead of MCRYPT_DEV_RANDOM.
$iv = mcrypt_create_iv(mcrypt_enc_get_iv_size($m), MCRYPT_DEV_RANDOM);
// Initialize the encryption:
mcrypt_generic_init($m, $key, $iv);
// Encrypt the data:
$data = mcrypt_generic($m, $data);
// Close the encryption handler:
mcrypt_generic_deinit($m);
// Close the cipher:
mcrypt_module_close($m);
// Store the data:
$_SESSION['thing1'] = base64_encode($data);
$_SESSION['thing2'] = base64_encode($iv);
// Print the encrypted format of the data:
echo '<p>The data has been stored. Its value is ' . base64_encode($data) . '.</p>'; ?>
</body>
</html>
```

#### Decrypting data
To start:
```php
$m = mcrypt_module_open('rijndael-256', '', 'cbc', '');
mcrypt_generic_init($m, $key, $iv);
$data = mdecypt_generic($m, $encrypted);
```
To successfully decrypt the data, you will need the exact same key and IV used to encrypt it.

Close up your resources:
```php
mcrypt_generic_deinit($m);
mcrypt_module_close($m);
```
Trim with ```rtrim()``` decrypted data, as the encryption process may add white spaces as padding to the end of the data.

Decrypting example:
```php
<?php /*	This page uses the MCrypt library
 *	to decrypt data stored in the session. */
session_start(); ?>
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>A More Secure Session</title>
</head>
<body>
<?php
// Make sure the session data exists:
if (isset($_SESSION['thing1'], $_SESSION['thing2'])) {
	// Create the key:
	$key = md5('77 public drop-shadow Java');	
	// Open the cipher...
	// Using Rijndael 256 in CBC mode:
	$m = mcrypt_module_open('rijndael-256', '', 'cbc', '');	
	// Decode the IV:
	$iv = base64_decode($_SESSION['thing2']);	
	// Initialize the encryption:
	mcrypt_generic_init($m, $key, $iv);	
	// Decrypt the data:
	$data = mdecrypt_generic($m, base64_decode($_SESSION['thing1']));	
	// Close the encryption handler:
	mcrypt_generic_deinit($m);
	// Close the cipher:
	mcrypt_module_close($m);	
	// Print the data:
	echo '<p>The session has been read. Its value is "' . trim($data) . '".</p>';
} else { // No data!
	echo '<p>There\'s nothing to see here.</p>';
}
?>
</body>
</html>
```
