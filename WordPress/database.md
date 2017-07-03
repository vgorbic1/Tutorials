## WordPress database
Typical full stack web development frameworks don't come with a predefined
database structure. Instead, these frameworks focus on the core foundation of an
application while allowing the developers to focus on the application-specific features.
On the other hand, WordPress provides a preplanned database structure with a fixed
set of tables. WordPress is built to function as a content management system, and
hence, it can be classified as a product rather than a pure development framework.
The WordPress core database is designed to power the generic functionalities of
a CMS.

The WordPress database is intended to work with MySQL, and hence, we need
to have a MySQL database set up before installing WordPress. On successful
installation, WordPress will create eleven database tables to cater core functionality
with the default MySQL table engine.

MyISAM was used as the default MySQL table engine prior to version
5.5.5 and this has been changed to InnoDB from version 5.5 onwards.

WordPress core features will always be limited to these eleven tables and it's quite
surprising to see the flexibility of building a wide range of applications with such a
limited number of tables. Both WordPress and framework developers need to have
a thorough understanding about the existing tables in order to associate them in
web applications.

#### User-related tables
This section consists of two tables for keeping the user-related information of your
application.
- `wp_users`: All the registered users will be stored in this table with their
basic details such as name, e-mail, username, password, and so on.
- `wp_usermeta`: This table is used to store additional information about the
users as key-value pairs. User roles and capabilities can be considered as
the most important user-specific data of this table. Also, we have the
freedom to add any user-related information as new key-value pairs.

In web applications, the user table plays the same role as in a normal CMS.
Therefore, we don't have to worry about changing the default functionality. Any
other user-related functionalities should be associated with the `wp_usermeta` table.

It's a good rule of thumb to use metatables or custom tables for
advanced functionalities with your own unique keys by using a
prefix, instead of relying on the existing columns of core tables.

#### Post-related tables
This section consists of two tables to keep website posts- and page-related
information.
- `wp_posts`: This table is used to keep all the posts and pages of your website
with the details such as post name, author, content, status, post type, and
so on.
- `wp_postmeta`: This table is used to keep all the additional details for each
post as key-value pairs. By default, it will contain details such as page
template, attachments, edit locks, and so on. Also, we can store any
post-related information as new key-value pairs.

Usually, the wp_posts and wp_postmeta tables will act as the main data storage
tables for any web application. With the introduction of custom posts, we have
the ability to match most of our application data in these two tables. In web
applications, we can go beyond normal posts by creating various custom post
types.

#### Term-related tables
WordPress terms can be simply described as categories and tags. This section
consists of three tables for post category and tag related information.
- `wp_terms`: This table contains master data for all new categories and tags,
including custom taxonomies.
- `wp_term_taxonomy`: This table is used to define the type of terms and the
number of posts or pages available for each term. Basically, all the terms
will be categorized as category, post-tags, or any other custom terms
created through plugins.
- `wp_term_relationships`: This table is used to associate all the terms
with their respective posts.

Even though they're not as important as posts, terms will play a vital part in
supporting post functionalities.

#### Other tables
I have categorized the remaining four tables in this section as they play a less
important or independent role in web applications:
- `wp_comments`: This table is used to keep the user feedback for posts and
pages. Comments-specific details such as author, e-mail, content, and status
are saved in this table.
- `wp_commentmeta`: This table is used to keep additional details about each
comment. By default, this table will not contain much data as we are not
associating advanced comment types in typical situations.
- `wp_links`: This table is used to keep the necessary internal or external links.
This feature is rarely used in content management systems.
- `wp_options`: This table acts as the one and only independent table in the
database. In general, this is used to save application-specific settings that
don't change often.

Comments might not indicate a significant value with their default usage. However,
we can certainly think of many ways of incorporating comments into actual web
applications.

Most of the existing WordPress plugins use a single field to store all
the settings as a serialized array. It's considered a good practice, which
increases the performance due to a limited number of table records.

### Adapting existing tables into web applications
We should be trying to maximize the use of existing tables in every possible
scenario to get the most out of WordPress. Built-in database access functions are
optimized to work directly with existing tables, allowing us to minimize the time for
implementation. On the other hand, we need to write custom queries from scratch
to work with newly created tables.

### Querying the database
As with most frameworks, WordPress provides a built-in interface for interacting
with the database. Most of the database operations will be handled by the wpdb
class located inside the wp-includes directory. The wpdb class will be available
inside your plugins and themes as a global variable and provides access to all the
tables inside the WordPress database, including custom tables.

#### Inserting records
All the existing tables contain a prebuilt insert method for creating new records.
- `wp_insert_post`: This creates a new post or page in the `wp_posts` table.
If this is used on an existing post, it will update the existing record
- `add_option`: This creates a new option on the `wp_options` table, if it
doesn't already exist
- `wp_insert_comment`: This creates a new comment on the `wp_comments` table

#### Updating records
All the existing tables contain a prebuilt update method for updating existing
records.
- `update_post_meta`: This creates or updates additional details about posts
in the `wp_postmeta` table
- `wp_update_term`: This updates existing terms in the `wp_terms` table
- `update_user_meta`: This updates user meta details in the `wp_usermeta`
table based on the user ID

## Deleting records
We have similar methods for deleting records in each of the existing tables as
we have for updating records. 
- `delete_post_meta`: This deletes custom fields using the specified key in
the `wp_postmeta` table
- `wp_delete_post`: This removes existing posts, pages, or attachments from
the wp_posts table
- `delete_user_meta`: This removes the metadata matching criteria from a
user from the `wp_usermeta` table

#### Selecting records
As usual, there is a set of built-in functions for selecting records from the existing
tables.
- `get_posts`: This retrieves the posts as an array from the `wp_posts` table
based on the passed arguments. Also, we can use the `WP_Query` class
with necessary arguments to get the post list from the OOP method.
- `get_option`: This retrieves the option value of the given key from the
`wp_options` table.
- `get_users`: This retrieves a list of users as an array from the `wp_user` table.

#### Querying the custom tables
There are no built-in methods for accessing custom tables using direct
functions, so it's a must to use the `wpdb` class for handling custom tables.
- `$wpdb->get_results( "select query" )`: This can be used to select a
set of records from any database table.
- `$wpdb->query('query')`: This can be used to execute any custom query.
This is typically used to update and delete statements instead of select
statements, as it only provides the affected rows count as the result.
- `$wpdb->get_row('query')`: This can be used to retrieve a single row
from the database as an object, an associative array, or as a numerically
indexed array.

When executing these functions, we
have to make sure that we include the necessary filtering and validations, as these
are not built to directly work with existing tables:
```php
$wpdb->query(
  $wpdb->prepare("SELECT FROM $wpdb->postmeta WHERE post_id = %d AND meta_key = %s", 1, 'book_title')
);
```
WordPress version 3.5 and higher enforces a minimum of two
arguments to prevent developers from misusing the `prepare` function.
