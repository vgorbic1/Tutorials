## Meta Boxes
WordPress features multiple sections, or meta boxes, on the post, page, and link manager screens.
These meta boxes enable you to easily add additional data to your content.

To create a custom meta box in WordPress, you use the `add_meta_box()` function. This function
enables you to define all aspects of your meta box. Following is how this function is used:
```php
<?php add_meta_boxes( id, title, callback, page, context, priority, callback_args ); ?>
```
The `add_meta_boxes()` function accepts the following parameters:
- id — The CSS ID added to the DIV element that wraps your meta box
- title — The name of your meta box displayed in its heading
- callback — Function to be called to display your meta box
- page — The screen where your meta box should show
- context — The part of the page where the meta box should be shown
- priority — The priority in which your meta box should be shown
- callback_args — Arguments to pass into your callback function
You can add a custom meta box to any custom post type in WordPress by simply
setting the page parameter to the name of your custom post type.

The real power of meta boxes is saving data
to a post, page, or any type of content in
WordPress. Any data saved against your
content is called metadata. In the WordPress
edit screens, the meta box for custom fi elds
exists by default. Custom fi elds are just a
quick way to save metadata against your
content.

If your metadata name starts with an underscore, it does not display in the
default custom fi elds meta box in WordPress. This can help eliminate confusion
by the user when entering metadata.

Create a meta box on the
post screen to save two fields of data against
your post:
```php
add_action( 'add_meta_boxes', 'boj_mbe_create' );
function boj_mbe_create() {
  //create a custom meta box
  add_meta_box( 'boj-meta', 'Excelsior Meta Box', 'boj_mbe_function',
	'post', 'normal', 'high' );
}

function boj_mbe_function( $post ) {
  //retrieve the metadata values if they exist
  $boj_mbe_name = get_post_meta( $post->ID, '_boj_mbe_name', true );
  $boj_mbe_costume = get_post_meta( $post->ID, '_boj_mbe_costume', true );
  echo 'Please fill out the information below';
?>

<p>Name: <input type="text" name="boj_mbe_name" value="<?php echo esc_attr( $boj_mbe_name ); ?>" /></p>
<p>Costume: <select name="boj_mbe_costume">
	<option value="vampire"<?php selected( $boj_mbe_costume, 'vampire' ); ?>>Vampire</option>
    <option value="zombie"<?php selected( $boj_mbe_costume, 'zombie' ); ?>>Zombie</option>
    <option value="smurf"<?php selected( $boj_mbe_costume, 'smurf' ); ?>>Smurf</option>
  </select>
</p>
<?php }
//hook to save the meta box data
add_action( 'save_post', 'boj_mbe_save_meta' );
function boj_mbe_save_meta( $post_id ) {
  //verify the metadata is set
  if ( isset( $_POST['boj_mbe_name'] ) ) {
    //save the metadata
    update_post_meta( $post_id, '_boj_mbe_name',
    strip_tags( $_POST['boj_mbe_name'] ) );
    update_post_meta( $post_id, '_boj_mbe_costume',
    strip_tags( $_POST['boj_mbe_costume'] ) );
   }
}
```


