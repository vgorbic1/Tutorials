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
