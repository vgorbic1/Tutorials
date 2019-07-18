## Docker Compose
Define a configuration of all containers in one Docker Compose (docker-compose.yml) file:
```
version: '3'
services:
    python:
        image: python:3
        container_name: my_py
        volumes: 
            - .:/src
        command: python3 /src/run.py
        restart: always
    mysql:
        image: mysql:latest
        container_name: my_mysql
        environment: 
            - MYSQL_ROOT_PASSWORD=abc123
            - SOME_OTHER_VAR
        restart: always
    ubuntu:
        image: ubuntu:latest
        container_name: my_ubuntu
        command: echo "Hello from Ubuntu!"
        restart: always
```
Run this file from the current directory:
```
docker-compose up
```
There is no need to create a network, because all containers in compose file are running on one network by default.

It is possible to use JSON format as docker-compose file.

### Stopping Containers
```
control + C
```
### Run Docker Compose in Background
```
docker-compose up -d
```
### Check Current Status of Docker Compose
```
docker-compose ps
```
### Stop Docker Compose
```
docker-compose down
```
