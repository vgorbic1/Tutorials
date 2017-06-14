## WordPress UI
The most important part of using the WordPress styles is to wrap your plugin in the class `wrap` div. This class sets the stage for all admin styling.
```html
<div class="wrap">
  Plugin Page
</div>
```
### Icons
WordPress features a function to generate the icon divs called `screen_icon()`. This function accepts one parameter, and that is the screen icon you want to load.
```php
function boj_styling_settings() { ?>
  <div class="wrap">
  <?php screen_icon( 'plugins' ); ?>
  <h2>My Plugin</h2>
  </div>
  <?php
}
```
### Messages
When an action occurs in your plugin, such as saving settings, it’s important to display a message to
the user verifying whether the update was successful:
```php
<div id="message" class="updated">Settings saved successfully</div>
```
### Buttons and Links
```html
<input type="submit" name="Save" value="Save Options" />
<input type=”submit” name=”Save” value=”Save Options” class=”button-primary” />
<input type=”submit” name=”Secondary” value=”Secondary Button” />
<input type=”submit” name=”Secondary” value=”Secondary Button” class=”button-secondary” />
<input type=”submit” name=”highlighted” value=”Button Highlighted” class=”button-highlighted” />
```
Links can also take the form of a button by using the appropriate class.
```html
<a href=”#”> Search </a>
<a href=’#’ class=’button-secondary’> Search </a>
<a href=’#’ class=’button-highlighted’> Search </a>
<a href=’#’ class=’button-primary’> Search </a>
```
### Form
WordPress has a special table class just for forms called `form-table`:
```html
<form method=”POST” action=””>
 <table class=”form-table”>
  <tr valign=”top”>
   <th scope=”row”><label for=”fname”> First Name </label></th>
< td > < input maxlength=”45” size=”25” name=”fname” / > < /td >
< /tr >
< tr valign=”top” >
< th scope=”row” > < label for=”lname” > Last Name < /label > < /th >
< td > < input id=”lname” maxlength=”45” size=”25” name=”lname” / > < /td >
< /tr >
< tr valign=”top” >
< th scope=”row” > < label for=”color” > Favorite Color < /label > < /th >
< td >
< select name=”color” >
< option value=”orange” > Orange < /option >
< option value=”black” > Black < /option >
< / select >
< /td >
< /tr >
< tr valign=”top” >
< th scope=”row” > < label for=”featured” > Featured? < /label > < /th >
< td > < input type=”checkbox” name=”favorite” / > < /td >
< /tr >
< tr valign=”top” >
< th scope=”row” > < label for=”gender” > Gender < /label > < /th >
< td >
< input type=”radio” name=”gender” value=”male” / > Male
< input type=”radio” name=”gender” value=”female” / > Female
< /td >
< /tr >
< tr valign=”top” >
< th scope=”row” > < label for=”bio” > Bio < /label > < /th >
< td > < textarea name=”bio” > < /textarea > < /td >
< /tr >
< tr valign=”top” >
< td >
< input type=”submit” name=”save” value=”Save Options”
class=”button-primary” / >
< input type=”submit” name=”reset” value=”Reset”
class=”button-secondary” / >
< /td >
< /tr >
< /table >
</form>
```
### Tables
Tables can easily be styled in WordPress using the `widefat` class.
```
< table class=”widefat” >
< thead >
< tr >
< th > Name < /th >
< th > Favorite Holiday < /th >
< /tr >
< /thead >
< tfoot >
< tr >
< th > Name < /th >
< th > Favorite Holiday < /th >
< /tr >
< /tfoot >
< tbody >
< tr >
< td > Brad Williams < /td >
< td > Halloween < /td >
< /tr >
< tr >
< td > Ozh Richard < /td >
< td > Talk Like a Pirate < /td >
< /tr >
< tr >
< td > Justin Tadlock < /td >
< td > Christmas < /td >
< /tr >
< /tbody >
< /table >
```
### Pagination
WordPress has a few different classes to style your pagination:
```
< div class=”tablenav” >
< div class=”tablenav-pages” >
< span class=”displaying-num” > Displaying 1-20 of 69 < /span >
< span class=”page-numbers current” > 1 < /span >
< a href=”#” class=”page-numbers” > 2 < /a >
< a href=”#” class=”page-numbers” > 3 < /a >
< a href=”#” class=”page-numbers” > 4 < /a >
< a href=”#” class=”next page-numbers” > & raquo; < /a >
< /div >
< /div >
```
