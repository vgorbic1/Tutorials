## Including Code from other files

Normally, ```include()``` is the only command you need. It continues processing the code even included file is missing.
- ```require()``` is used when the file is mandatory.
- ```require_once()``` and ```include_once``` is to ensure that the external file doesn't reset any variables that may bhave been assigned  a new value elsewhere.
