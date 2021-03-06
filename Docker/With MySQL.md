## Docker with MySQL
Run a Docker container with MySQL image.
```
docker run --rm -d --name my_sql -e MYSQL_ROOT_PASSWORD=some-pwd mysql:latest
```
- `--rm` means remove container after it finishes executing
- `-d` means the container should run in the background, so logs of MySQL are not displayed
- `--name my_sql` specify the name of the container
- `-e` sets the environment variable MYSQL_ROOT_PASSWORD to "some-pwd"
- `mysql:latest` means use the latest version of MySQL image

### Execute commands within container
Make sure your container is running (`docker ps`)
```
docker exec -it my_sql mysql -h localhost -u root -p
```
Container will still run after exit from the mysql> command prompt (type 'exit')
