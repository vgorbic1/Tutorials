## Unable to upload images and update plugins

The fix:
- Create a phpinfo test page.
- Scroll down to "apache2handler" or look for "User/Group."
- Remember the name listed for the user. My entry was apache(#)/#, the name was "apache."
- Log into a terminal as the root user. 
- Navigate to the folder just above where your WP is installed.
- Type ```chown -R (your the username from earlier) (your wp directory)/``` - for me, ```chown -R apache httpdocs/```. 
This changes the ownership of the directory to apache.
Navigate to your wp-content folder: httpdocs/wp-content/
Type ```chmod -R 766 uploads/```. This changes permissions so that apache can read, write, and execute there.
