## Password Security
With PHP 5.5, a new, simple password-hashing API was added to help ensure that best practices are used by everyone. The password-hashing API currently promotes bcrypt one-way hashing as the best algorithm; it is far superior to MD5, and even SHA-1.

#### Hashing Passwords
Hashing a password is as simple as calling the ```password_hash()``` function with the string to hash and the algorithm to use:
```php
$hashed = password_hash("password", PASSWORD_BCRYPT);
```
Displays something similar to:
```
$2y$10$zEsiam6Y6rlCGqGgS3lrve8FaeWruKJY3ElaeQUJRhEyhWOQ7ySqO
```
It is also possible to pass extra options to ```password_hash()``` by passing an associative array as the third argument. These options are:
- salt — You may provide a custom salt which will override the automatically generated salts. This is not recommended.
- cost — The cost denotes the algorithmic cost that should be used—the higher this number, the slower, and the better your security. The
default is 10. You should be aiming for a hash time of between one-half and one second.
```php
$hashed = password_hash("password", PASSWORD_BCRYPT, ['cost' => 12]);
```
Displays something similar to the following:
```
$2y$12$AGzXqsGLuHSXhW4nCzC6NeZauf.hrWoBJpNn/Q4pr9phL0BNvMIOa
```
#### Verifying password
To verify a password, we use the ```password_verify()``` function. It takes the user input, and the saved hash, and returns a boolean. This is possible because the resulting hash from ```password_hash()``` includes the algorithm, cost, and salt.
```php
// Assume $hashed contains the originally stored password
if (password_verify($_POST['password'], $hashed)) {
  // Password is valid
}
```

####Forward Compatibility
Automatically update your users’ passwords when new algorithms become available.
```php
// Assume $hashed contains the originally stored password
if (password_verify($_POST['password'], $hashed)) {
  // Password is valid
  if (password_needs_rehash($hashed, PASSWORD_DEFAULT)) {
    $newhash = password_hash($_POST['password'], PASSWORD_DEFAULT);
    // Store the $newhash
  }
}
```
This can allow you to upgrade your users in place without inconveniencing
them with a mass password reset. After a set period of time, say
30 days, you can reset the passwords of users who are still failing
```password_needs_rehash()``` to migrate inactive users and ensure security.


#### Example
```php
$pass = password_hash('123MyPass', PASSWORD_DEFAULT);

if (password_verify('123MyPass', $pass)) {
    echo 'Password is valid!';
} else {
    echo 'Invalid password.';
}
```

[PHP User Authentication System](https://www.tutorialrepublic.com/php-tutorial/php-mysql-login-system.php)
[UDEMY: Complete Login and Registration System with PHP & MYSQL](https://www.udemy.com/user-authentication-code-a-simple-login-system-with-php/)
