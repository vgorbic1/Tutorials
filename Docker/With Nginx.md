## Docker with Nginx
Run a Docker container with Nginx image.
```
docker run --rm -d -v $(pwd):/usr/share/nginx/html \
-p 80:80 --name my_nginx nginx:latest
```
- `--rm` means remove container after it finishes executing
- `-d` means the container should run in the background, so logs of MySQL are not displayed
- `-v` mount volume from current directory to `/usr/share/nginx/html` directory of the container (just to serve html files)
- `-p` use (forward) port 80 of current system (localhost) to work with container's port 80
- `--name my_nginx` specify the name of the container
- `-e` sets the environment variable MYSQL_ROOT_PASSWORD to "some-pwd"
- `mysql:latest` means use the latest version of MySQL image

Create a simple index.html file with some test text. Run the container.
Go to localhost with your browser to see the content of your index.html file.

You also can change the port to go from host machine port 1234 to 80 of the container using `-p 1234:80`
