## A basic file structure of the WordPress theme
WordPress powers its frontend with a concept called themes, which consists of a set
of predefined template files to match the structure of the default website layouts.

Even though default themes contain a number of files for providing
default features, only style.css and index.php files are enough for
implementing a WordPress theme. Complex web applications themes
are possible with the standalone index.php file.

The design and the content for pages are provided through the page.php template, while the content for posts
is provided through one of the following templates:
- index.php
- archive.php
- category.php
- single.php

In normal circumstances, WordPress sites have a blog built on posts, and all the
remaining content of the site is provided through pages. 
- **Archive pages** are used to provide summarized listings of data as a grid.
- **Single posts:** are used to provide detailed information about the
existing data in the system.
- **Single pages** are used for any type of dynamic content associated
with applications. Generally, we can use pages for form submissions,
dynamic data display, and custom layouts.

![wpap](https://github.com/vgorbic1/Tutorials/blob/master/WordPress/Theme-development/images/wpap.jpg)

WordPress looks for a page with the slug
or ID before executing the default page.php file.
