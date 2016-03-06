## Core Concepts
A *node* is the generic term for a piece of content on your web site. The *content type* of the node will define what fields are included with it. Depending on the type of node, different fields will be attached. For example, a basic Page content type has attached fields such as title and body. Other examples of content type are: Book pages for use in Books, Discussion topics in forums, Blog pages in blogs, and News articles.

An *entity type* is a useful abstraction to group together fields. Entity types are used to store and display data, which can be nodes (content), comments, taxonomy terms, user profiles, or something custom developed.

Each *comment* is typically a small piece of content that a user submits, attached to a particular node. 

Pages on your Drupal site are laid out in *regions*. These can include the header, footer, sidebars, and main content regions. Your theme may define additional regions.

*Blocks* are discrete chunks of information that are displayed in the regions of your site's pages. Blocks can take the form of static chunks of HTML or text, menus (which are for site navigation), the output from modules (e.g. hot forum topics), or dynamic listings that you've created yourself (e.g. a list of upcoming events).

*Views* allows people to choose a list of nodes or other entities and present them as pages, blocks, RSS feeds, or other formats. The main use case for views is to create dynamically updating lists of content (for example, a listing of latest news), based on properties of that content (in the case of the news listing, that the content type is “News” and sorted by publication date).

Generally, Drupal allows each module to define *paths* that the module will be responsible for, and when you choose to visit a particular path Drupal asks the module what should be displayed on the page.

The *bootstrap* is the CPU (central processing unit) of Drupal. In other interactive software environments this is sometimes called the event loop. Drupal's core is a bit like that. It sits around waiting for a path request, and then starts processing that request.

*Permissions* can be set to control what users have access to view and/or edit particular areas of a site.

#### Users
- **Master Administrator**. This user has the ID one (1). User of ID one (1) is the primary admin user account created during Drupal installation. This user is very special because it has permission to do absolutely everything on the site.
- **Logged In**. These users are assigned a user ID when they register for the website. A user name and email address is associated with any user that isn't anonymous (therefore must be logged in).
- **Anonymous**. Anonymous users who visit the website but do not login all share a user ID of zero (0).

#### Content Types
In Drupal, each item of content is called a node, and each node belongs to a single content type, which defines various default settings for nodes of that type, such as whether the node is published automatically and whether comments are permitted.

**Article**

The Article content type (formerly, "story") is enabled in Drupal in the default installation profile. Articles are generally used for information that is updated more frequently and often cross-referenced and categorized (such as news items or resources). By default, Articles are sorted with the most recent post at the top, but this can be customized with contributed modules like Views.

**Basic page**

The Basic page content type is enabled in Drupal in the default installation profile. Typically Basic pages are used for static content that can (but are not required to) be linked into the main navigation bar. This is one of the most "basic" content types and can be very flexible.

**Blog Entry**

The Blog (short for weblog) content type was removed in Drupal 8. It is an online journal or diary, and Blog module allows registered users on your site to create their own blogs. Each entry in a user blog has content type Blog Entry.

**Book Page**

Book pages are designed to be part of a collaborative book, enabled by the core Book module. An example of a collaborative book is the Drupal developer documentation. In older versions of Drupal, only nodes of content type Book Page could be added to a book. However, since Drupal 7 nodes of any content type can be part of a book.

**Forum topic**

A Forum topic defines a topic for a forum discussion; people can reply to the topic by using comments. Forum nodes are organized into subject areas via a Taxonomy (list of categories).

**Poll**

A poll is a question with a set of possible responses. Once created, a poll automatically provides a simple running count of the number of votes received for each response.
