## Creating widgets
Registering the widgets is similar to the process used for
registering the widgetized areas:
```php
public function register_widgets() {
 $base_path = plugin_dir_path(__FILE__);
 include $base_path . 'widgets/class-home-list-widget.php';
 register_widget('Home_List_Widget');
}
```
