##Hooks
Hooks are the backbone of WordPress. They enable plugin developers to “hook” into the WordPress workflow to change how it works without directly modifying the core code. This enables users to easily upgrade to newer versions of WordPress without losing modifications. 
WordPress has two primary types of hooks: action hooks and filter hooks. The former enables you to execute a function at a certain point, and the latter enables you to manipulate the output passed through the hook. Hooks aren’t just for plugins. WordPress uses hooks internally.

####Actions
Action hooks enable you to fire a function at specific points in the WordPress loading process or when an event occurs. For example, you might want a function to execute when WordPress first loads a page or when a blog post is saved.

**do_action()**

When hooking into WordPress, your plugin won’t call this function directly; however, your plugin will almost always use it indirectly.
```php
  do_action( $tag, $arg = '' );
```
- $tag — The name of the action hook.
- $arg — Value(s) passed to registered actions. Action hooks have the option to pass any number of parameters or no parameters at all. You need to check the WordPress source code for specific hooks because the number of parameters changes on a per-hook basis. 

```wp_head``` hook is fired within the <head> area on the front end of the site. WordPress and plugins usually use this hook to add meta information, style sheets, and scripts.
```php
do_action( 'wp_head' );
```
When this code fires in WordPress, it looks for any actions registered for the ```wp_head``` action hook. It then executes them in the order specified. As you can see, it has a name of ```wp_head``` but passes no extra parameters. This is often the case with action hooks.
