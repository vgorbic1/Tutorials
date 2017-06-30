## User Roles
WordPress offers built-in functions for working with every aspect of user roles.

WordPress comes with six built-in user roles, including superadmin, which will not
be displayed on the user creation screen by default.

- Superadmin: A superadmin has administration permission in WordPress
multisite implementation
- Admin: An admin has permission to all administration activities inside
a single site
- Editor: An editor can create, publish, and manage posts, including
the posts of other users
- Author: An author can create and publish their own posts
- Contributor: A contributor can create posts, but cannot publish on
their own
- Subscriber: A subscriber can read posts and manage their profile

It doesn't matter whether you choose existing ones or new ones as long as you are
comfortable and the roles have a specific meaning within your application. Since
we choose custom roles, it's not necessary to keep the unused default roles.

### Creating Custom Roles
We can create a new user role by calling the `add_role` function.
The following code illustrates the basic form of user role creation:
```php
$result = add_role( 'role_name', 'Display Name', array(
  'read' => true, 'edit_posts' => true, 'delete_posts' => false)
);
```
The first parameter takes the role name, which is a unique key to identify the role.
The second parameter will be the display name, which will be shown in the admin
area. The final parameter will take the necessary capabilities of the user role.

Example code:
```php
public function add_application_user_roles() {
  add_role( 'follower', 'Follower', array( 'read' => true ));
  add_role( 'developer','Developer', array( 'read' => true ));
  add_role( 'member', 'Member', array( 'read' => true ));
}
```
The user roles are saved in the database as
settings. Therefore, only a single call to this function is required throughout the life
cycle of an application. We have two options for implementing this functionality.
Application installation and plugin activation are the most suitable places to call
these kinds of functions to eliminate duplicate executions:
- Application installation: WordPress provides a well-defined step-by-step
installation process. Similarly, every application or plugin needs an installation
process. Once installation is completed, these files are not accessible again.
Therefore, plugin installation is the ideal place to create user roles.
- Plugin activation: WordPress plugin activation hooks let us execute certain
functionality on plugin activation. This is also a one-time process in a plugin.
However, we can deactivate and reactivate the plugin multiple times. So,
this functionality gets executed multiple times and hence, we have to check
whether it's already been executed. If this is not checked, all the changes
made after the activation will be reset to default values. So, plugin activation
is the second best option for this type of functionality.

Here, we will be using plugin activation to add and remove application user
roles. We need to include the call to the `add_application_users` function inside the constructor:
```php
register_activation_hook( __FILE__ , array( $this, 'add_application_user_roles' ) );
```
The `register_activation_hook` function will be called when the plugin is
activated and hence, avoids duplicate calls to database.
A good rule of thumb is to prevent the inclusion of such settings
inside the init action as it will get executed in each request,
making unnecessary performance overhead.

### Removing Existing Roles
WordPress offers the remove_role function for deleting both custom and existing
user roles. 
Let's create a function that removes the unnecessary user
roles from the system:
```php
public function remove_application_user_roles() {
  remove_role( 'author' );
  remove_role( 'editor' );
  remove_role( 'contributor' );
  remove_role( 'subscriber' );
}
```
As mentioned earlier, the remove_role function involves database operations and
hence, it's wise to use it with the `register_activation_hook` function:
```
register_activation_hook( __FILE__, array($this, 'remove_application_user_roles') );
```
More in [User Capabilities](https://github.com/vgorbic1/Tutorials/new/master/WordPress/App-Development/user%20capabilities.md)
