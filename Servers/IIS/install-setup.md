## Install / Set Up IIS
IIS stands for Internet Information Server. IIS is a group of Internet servers (including a Web or Hypertext Transfer Protocol server and a File Transfer Protocol server) with additional capabilities for Microsoft's Windows NT and Windows 2000 Server operating systems.

#### Install IIS on Windows 7
Keep in mind that your version of Windows may not come with IIS. I’m using Windows 7 Ultimate edition.
- Go to Control Panel, and then click on Programs. There is a link “Turn Windows features on or off”
- Expand the Internet Information Services tree. Check "IIS Management console" within Web Management tools and everything under World Wide Web Services. Click OK.
- Navigate to ```localhost```. You should see a default web page.

#### Setting up IIS
- Go to Control Panel and type "inetmgr" to open IIS management panel.
- Icon on the left hand side that represents your server. It will named with some combination of numbers and letters.
- Find "Sites" folder under the server. Right-click on it and choose "Add Web Site".
- Give the Site a name (typically the site the domain name like: test.com)
- Assign a physical path to the folder on the computer to host the site files. ```C:\inetpub\wwwroot\test.com```
- Assign a Host Name. Host Names are the names that IIS uses to bind the incoming request to the actual physical files of the site. You must have a host name configured for test.com and www.test.com. Host names should be unique. For now put only ```test.com``` and click OK. 
- Right-click on the new icond under the Sites that represent your new site and choose "Edit Bindings...". Add ```www.test.com```
- Point the A Record of both test.com and www.test.com. Once your domain name A records are pointed to the IP address of your server, your domain names should resolve to that server.
 
### Setting FastCGI and PHP
- Install CGI module through Control Panel > Programs > Turn Windows features on or off > Internet Information Services > World Wide Web Services > Application Development Features > CGI. The CGI module has old CGI and new CGI packets.
- Install PHP if not yet installed.
- With IIS Manager go to Modules and check that both CgiModule and FastCgiModule are present.
- With IIS Manager go to Handler Mappings and add new Moule Mapping. 
- Set Request path to ```*.php```. Select FastCgiModule. In Executable set the path to your PHP'd installation ```php-cgi.exe``` Name the mapping "PHP FastCGI" or something like this.
- Test that you can serve .php scripts now.
