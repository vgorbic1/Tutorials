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
