## Creating Custom Database Tables
In typical circumstances, we create the database tables manually before moving
into the implementation. With the WordPress plugin-based architecture, it's certain
that we might need to create custom tables using plugins in the later stages of
the projects. Creating custom tables through plugins involves certain predefined
procedures recommended by WordPress. Since table creation is a one-time task,
we can implement the process on plugin activation or installation.
```php
public function create_custom_tables() {
 global $wpdb;
 // Include the upgrade.php file to make use of the dbDelta function.
 require_once( ABSPATH . 'wp-admin/includes/upgrade.php' );
 $user_activities_table = $wpdb->prefix.'user_activities';
 // check the existence of a database table
 if ($wpdb->get_var("show tables like '$user_activities_table'") != $user_activities_table) {
  $sql = "CREATE TABLE $user_activities_table (
  id mediumint(9) NOT NULL AUTO_INCREMENT,
  time datetime DEFAULT '0000-00-00 00:00:00' NOT NULL,
  user_id mediumint(9) NOT NULL,
  activity text NOT NULL,
  url VARCHAR(255) DEFAULT '' NOT NULL,
  UNIQUE KEY id (id));";
  dbDelta( $sql );
 }
}
```
It's more efficient to use a
single call to `register_activation_hook` to handle multiple functions. Therefore,
we will change the implementation of activation initialization function as follows:
```php
register_activation_hook( __FILE__ , array( $this, 'activate_portfolio_manager' ) );
```
Execute all the activation-related functions inside the `activate_portfolio_manager`:
```php
public function activate_portfolio_manager(){
  // Creates all the user types
  $this->add_application_user_roles();
  // Remove unused user roles
  $this->remove_application_user_roles();
  // Create custom capabilities for user roles
  $this->add_application_user_capabilities();
  // Flush rewrite rules
  $this->flush_application_rewrite_rules();
  // Create custom tables
  $this->create_custom_tables();
}
```
We created the custom tables using the `dbDelta` function inside the plugin
activation. WordPress recommends the dbDelta function over direct SQL queries
for table creation since it examines the current table structure, compares it to the
desired table structure, and makes the necessary modifications without breaking
the existing database tables. Apart from the table creation, we can execute quite a
few database-related tasks on plugin activation such as altering tables, populating
initial data to custom tables, and upgrading the plugin tables.

Even though custom
tables offer you more flexibility within WordPress, there will be a considerable number
of limitations, as listed here:
- Custom tables are hard to manage in WordPress upgrades.
- WordPress default backups will not include custom tables.
- No built-in functions for accessing database. All the queries,
filtering, and validation need to be done from scratch, using the
existing $wpdb variable.
- User interfaces for displaying these table data needs to be created
from scratch.

Therefore, you should avoid creating custom tables in all possible circumstances,
unless you have a distinct advantage from the perspective of your application.
