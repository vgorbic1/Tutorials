## Plugin Development Checklist
Following this checklist you can be confident you have a proper plugin foundation for your new plugin:
- Determine a unique and descriptive plugin name. Is the name descriptive of your plugin’s function? Have you verifi ed the plugin doesn’t exist in the Plugin Directory?
- Set a unique plugin prefix. Is the prefix unique enough to avoid conflicts?
- Create your plugin folder structure. Will your plugin need a PHP directory? Will your plugin need a JavaScript directory? Will your plugin need a CSS directory? Will your plugin need an images directory?
- Create your default plugin files. Create your primary file named the same as your plugin folder. Create the uninstall.php file for your uninstall procedures.
- Create your plugin’s header code. Set your plugin name as you want it displayed. Add a detailed description about your plugin’s purpose. Set the proper version for your plugin. Verify both Plugin URI and Author URI values are set.
- Include a license for your plugin. Place the license code directly below your plugin header.
- Create your plugin’s activation function. Does your plugin require a specific version of WordPress or higher to function? Does your plugin require default options to be set when activated?
- Create your plugin’s deactivation function. Does your plugin require something to happen when it is deactivated?
- Create your plugin’s uninstall script. Create an uninstall.php file Include uninstall scripts in the file.
- File references. Use the proper directory constants and functions to determine paths within WordPress and your plugin.
