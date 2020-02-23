## Install IIS 
### on Windows 10.
- Control Panel > Programs > Turn Windows Features On or Off.
- Check *Intenet Information Services* box and expand it.
- Check *ASP.NET* with a proper version and *CGI* if you need to run any PHP.
- Find IIS with search panel.

### on Windows Server 16 (19)
- Open Server Manager: Start > Server Manager tile.
- Manage > Add Roles and Features (right top corner)
- "Next" > "Role-based or Feature-based Installation" > Select the server > Check Web Server IIS > 
Add Features > Application Development
- Check *ASP.NET* with a proper version and *CGI* if you need to run any PHP.
- You should see IIS inside the server manager window (top left).
- Higlight IIS and expand Tool > Internet Information Services Manager (top right)

### Set a Static HTML site
- Go to IIS Manager and expand the server name > Site
- Right-click > Add Website
- Put a unique name of the website (usually as a domain name)
- Put path where your site resides `inetpub\wwwroot\`
- Put `localhost` as a Host Name
- If you have default files in the `wwwroot`, delete them
- Put your simple html page into inetpub\wwwroot\
- Go to a web browser and type *localhost* in the URL. You should see the content of the html page

### Set custom Domain Name locally
- Go to IIS Manager and expand the server name > Site >
- Select existing site. The site also appears in the central window.
- Right-click on the site in the central window and select Bindigs.
- Select `localhost` and change Host Name to desired domain name.
- Find `hosts` file on your Windows machine (C:\Windows\System32\drivers\etc)
- Edit the `hosts` file with a notpad in Administrator mode. Append:
```
127.0.0.1 mycusotmdomain.com
```
Now mycustomdomain.com will work as a local DNS address for your localhost

### Application Pool
- Go to IIS Manager and expand the server name > Site >
- Right-click the `Application Pools` and add application pool
- Name it as you wish and change/leave defaults.
- Select an existing site and right-click it and go to manage Website > Advanced Settings
- Select an application pool you just created
Now a `worker process` will be associated with sites that run on this application pool
- Check running worker processes: Server name > Worker processes (central window)

### Virtual Directory
- Go to IIS Manager and expand the server name > Site >
- Right-click on any existing site and select Add Virtual Directory
- Name it and add a physical path to the directory

### Install and Set FTP Service
- Open Server Manager: Start > Server Manager tile.
- Manage > Add Roles and Features (right top corner)
- Click "Next" until you get to Server Roles.
- Expand Web Server IIS and check "FTP Server". Click "Next" and install.
- Go to IIS Manager and expand the server name > Site > Site name
- Right-click the site name and select `Add FTP Publishing`.
- Set Basic authentication and Specific users.
- Set Username and Permissions for this user.

### Set Default Document
- Go to IIS Manager and expand the server name > Default Document (center window)
- Set a new default document (for example index.php to handle PHP directory index file)
- Move all other files according to importance.

### Add PHP handler
- Go to IIS Manager and expand the server name > Handler Mappings (center window)
- Click `Add Module Mapping` on the right side of the page.
```
Request path: *.php
Module: FastCgiModule
Executable: "C:\PHP\php-cgi.exe" (here should be the full path to php-cgi.exe of PHP installation)
Name: PHP via FastCGI
```
- You should note that if you don’t see in the modules space, "FastCgiModule" drop-down menu, it entails that
the module has either not been enabled or registered. To confirm that FastCGI module has been registered, 
access the IIS configuration `file%WINDIR%windowssystem32configapplicationHost.config`and confirm the line is 
also in the section of the <globalmodules>.
```
<add name="FastCgiModule" image="%windir%System32inetsrviisfcgi.dll" />
```
In that exact file, confirm that the <modules> section has had the FastCGI module added to it like the highlighted path below.
```
<add name="FastCgiModule" />
```
- Click "Yes"
- Check the PHP availability with `phpinfo();`
