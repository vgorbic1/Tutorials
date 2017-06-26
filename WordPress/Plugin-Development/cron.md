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
### Scheduling a Single Event
Typically events scheduled in cron are recurring, but there may be an occasion when you want to
schedule a single event in cron. This means the event would run once and not be scheduled to run
again. To schedule a single event use the `wp_schedule_single_event()` function:
```php
wp_schedule_single_event( timestamp, hook, args );
```
The function accepts the following parameters:
- `timestamp` — The time you want the event to run
- `hook` — The action hook name to execute
- `args` — Arguments to pass to the hook’s callback function

Working example:
```php
add_action( 'admin_menu', 'boj_cron_single_menu' );
function boj_cron_single_menu() {
 //create cron example settings page
 add_options_page( 'Cron Example Settings', 'Cron Settings', 'manage_options', 'boj-single-cron', 'boj_cron_single_settings' );
}
//create the custom hook for cron scheduling
add_action( 'boj_single_cron_hook', 'boj_cron_single_email_reminder' );
function boj_cron_single_email_reminder () {
 //send scheduled email
 wp_mail( 'you@example.com', 'Reminder', 'You have a meeting' );
}
function boj_cron_single_settings() {
 //verify event has not been scheduled
 if ( !wp_next_scheduled( 'boj_single_cron_hook' ) ) {
  //schedule the event to in one hour
  wp_schedule_single_event( time()+3600, 'boj_single_cron_hook' );
 }
}
```
When scheduling a single cron event, you do not need to unschedule it. The cron
event runs once and unschedules itself when complete.
### Unscheduling an Event
When a cron job is scheduled in WordPress, it is stored in the `wp_options` table. This means the
scheduled job will not be removed, or unscheduled, by simply deactivating the plugin that scheduled
it. If the plugin is deactivated without properly unscheduling the cron job. WordPress can’t execute
the scheduled job because the plugin code will no longer be available. However, the cron job
scheduled will still be stored and WordPress will try to execute it on the schedule set.
To properly unschedule a cron event, use the `wp_unschedule_event()` function.
```php
wp_unschedule_event( timestamp, hook, args );
```
The function accepts the following parameters:
- `timestamp` — Time of the next occurrence to run
- `hook` — The action hook to unschedule
- `args` — Arguments to pass to the hook’s callback function

A Full sample:
```php
/*
Plugin Name: View Cron Jobs Plugin
Plugin URI: http://example.com/wordpress-plugins/my-plugin
Description: A plugin demonstrating Cron in WordPress
Version: 1.0
Author: Brad Williams
Author URI: http://wrox.com
License: GPLv2
*/
add_action( ‘admin_menu’, ‘boj_view_cron_menu’ );
 function boj_view_cron_menu() {
 //create view cron jobs settings page
 add_options_page( 'View Cron Jobs', 'View Cron Jobs', 'manage_options', 'boj-view-cron', 'boj_view_cron_settings' );
}
function boj_view_cron_settings() {
 $cron = _get_cron_array();
 $schedules = wp_get_schedules();
 $date_format = 'M j, Y @ G:i';
?>
<div class="wrap" id="cron-gui">
<h2>Cron Events Scheduled </h2>
<table class="widefat fixed">
<thead>
<tr>
<th scope="col">Next Run (GMT/UTC) </th>
<th scope="col">Schedule </th>
<th scope="col">Hook Name </th>
</tr>
</thead>
<tbody>
<?php foreach ( $cron as $timestamp =>$cronhooks ) { ?>
 <?php foreach ( (array) $cronhooks as $hook=>$events ) { ?>
  <?php foreach ( (array) $events as $event ) { ?>
  <tr>
  <td><?php echo date_i18n( $date_format, wp_next_scheduled( $hook ) ); ?></td>
  <td><?php
   if ( $event[ 'schedule' ] ) {
    echo $schedules[ $event[ 'schedule' ] ][ 'display' ];
   } else {
    ?>One-time <?php
   } ?>
  </td>
  <td><?php echo $hook; ?></td>
  </tr>
  <?php } ?>
 <?php } ?>
<?php } ?>
</tbody>
</table>
</div>
<? }
```
