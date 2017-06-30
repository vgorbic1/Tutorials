## User Capabilities
Capabilities can be considered as tasks, which users are permitted to perform
inside the application. A single user role can perform many capabilities, while
a single capability can be performed by many user roles. Typically, we use the
term access control for handling capabilities in web applications.

Look at the `wp_user_roles` option
inside the `wp_options` table for all the available user roles and their capabilities.

You can find over fifty built-in capabilities in the WordPress default database. Most
of these capabilities are focused on providing permissions related to website or blog
creation.

There are plenty of great and free plugins for managing user roles and permissions.
One of them is the [Members plugin](http://wordpress.org/plugins/members/) by Justin Tadlock, 
as it's quite clean and simple.

### Creating a capability
Capabilities are always associated with user roles and hence, we cannot create
new capabilities without providing a user role:
```php
public function add_application_user_capabilities(){
  $role = get_role( 'follower' );
  $role->add_cap( 'follow_developer_activities' );
}
```
First, we need to retrieve the user role as an object using the get_role function.
Then, we can associate new or existing capability using the add_cap function. We
need to continue this process for each user role until we assign all the capabilities
to necessary user levels. Also, make sure to call this function on activation with the
`register_activation_hook` function.
