## Security
Making your plugin secure is dealing with vulnerabilities and data integrity and reliability. It’s both
preventing malicious attacks and making sure legitimate use cannot produce unexpected behavior.

Check if a user has a capability or a role before proceeding to a sensitive action, or die with a meaningful message:
```php
// Capability:
if ( !current_user_can('install_plugins') ) wp_die( 'Insufficient permissions' );
// Role:
if( !current_user_can('editor') ) wp_die( 'You cannot edit this setting' );
```
The function ```current_user_can()``` depends on ```get_currentuserinfo()```.
### Nonce
WordPress employs two different functions to create nonces in forms, as hidden fields, or in URLs,
as a GET parameter.

To create and add a nonce to a URL:
```
$url = wp_nonce_url( $url, $action );
```
The first parameter `$url` is a string of the URL address to which you want to append a nonce in the query string.

To create nonce in a form:
```
< form action=”” method=”post” >
< ?php wp_nonce_field( ‘boj_utags-rename_tag’.$id ); ? >
< input type=”hidden” name=”boj_action” value=”rename” / >
< input type=”hidden” name=”id” value=” < ?php echo $id; ? > ” / >
< input type=”text” name=”name” value=” < ?php echo esc_attr($name); ? > ” / >
< input type=”submit” value=”Rename” / >
< /form >
```

To verify nonce:
```
if( !current_user_can( ‘manage_options’ ) ) wp_die( ‘Insufficient privileges!’ );
$id = $_REQUEST[‘id’];
$action = $_REQUEST[‘boj_action’];
check_admin_referer( ‘boj_utags-’.$action.’_tag’.$id );
switch( $action ) {
 case ‘rename’:
  $newtag = array( ‘name’ = > $_POST[‘name’], ‘slug’ = > $_POST[‘name’] );
  wp_update_term( $id, ‘post_tag’, $newtag );
  break;
 case ‘delete’:
  wp_delete_term( $id, ‘post_tag’ );
  break;
}
```
### Data Validation and Sanitation
- Input should be validated and sanitized
- Output should be sanitized
You should never validate data and leave it in `$_POST`, `$_GET` or `$_REQUEST`
because it is important for developers to always be suspicious of data within
these superglobal arrays.
#### Integers
Use `intval()` or `is_int()` functions.
```
$data = 43;
// validate integers
return( intval( $data ) == $data );
// sanitize integers
return( intval( $data ) );
```
#### Text Strings
If you are expecting only letters:
```php
// Validate alphabetic strings
return( ctype_alpha( $num ) );
```
If you are expecting alphanumeric strings, such as for a nickname (for example, “ Bob43 ” ):
```php
// Validate alphanumeric strings
return( ctype_alnum( $num ) );
```
#### Email Strings
To validate emain use `is_email`:
```php
if( is_email( $email ) === email ) {
  // email seems valid
} else {
  // email is invalid
}
```
Function `sanitize_email()` either returns an empty string or a sanitized email address, depending
on how malformed the input was:
```
var_dump( sanitize_email( ‘ozh@ozh’ ) );
// string(0) “”
```
#### HTML
HTML fragments can be sanitized at input with WordPress function `force_balance_tags()`
#### URLs
```
var_dump( esc_url( $url1 ) );
```
To sanitize a URL for database usage, prefer `esc_url_raw()`, which sanitizes without entity translation.
