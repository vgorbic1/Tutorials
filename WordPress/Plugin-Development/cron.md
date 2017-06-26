## Cron
Cron is how WordPress handles scheduled events. The term cron comes from the time-based
job scheduler in UNIX. These scheduled jobs
include checking for new versions of WordPress, checking for plugin and theme updates, and
publishing scheduled posts.

Cron is run when a frontend or admin
page is loaded on your web site. Every time a page is requested, WordPress checks if there are
any cron jobs to run. Any visit to your Web site can trigger cron, whether from a visitor or a
search engine bot.

Two types of cron events can be scheduled in WordPress: single and recurring. A recurring event is
a cron job that runs on a schedule and has a set recurring time in which it will run again. A single
event runs once and never runs again until it is rescheduled.

### Recurring Event
To schedule an event in WordPress, use the `wp_schedule_event()` function.
```php 
wp_schedule_event( timestamp, recurrence, hook, args );
```
The function accepts the following parameters:
- `timestamp` — The time you want the event to occur
- `recurrence` — How often the event should reoccur
- `hook` — The action hook name to execute
- `args` — Arguments to pass to the hook’s callback function

A simple example plugin to demonstrate the power of a cron scheduled task.
```php
add_action( 'admin_menu', 'boj_cron_menu' );
function boj_cron_menu() {
 //create cron example settings page
 add_options_page( 'Cron Example Settings', 'Cron Settings', 'manage_options', 'boj-cron', 'boj_cron_settings' );
}
add_action('boj_cron_hook', 'boj_cron_email_reminder');
function boj_cron_email_reminder() {
 //send scheduled email
 wp_mail( 'you@example.com', 'Elm St. Reminder', 'Don\'t fall asleep!' );
}
function boj_cron_settings() {
 //verify event has not been scheduled
 if ( !wp_next_scheduled( 'boj_cron_hook' ) ) {
  //schedule the event to run hourly
  wp_schedule_event( time(), 'hourly', 'boj_cron_hook' );
 }
}
```
