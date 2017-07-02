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
