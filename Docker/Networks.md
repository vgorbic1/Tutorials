## Docker Networks
Use a network of Docker containers to profide communication among them.
### Create a Network
```
docker network create net_1
```
### List Docker Networks
```
docker network ls
```
### Add a Docker Container to Network
- Add the first container
```
docker run --rm -d --net net_1 --name my_py -v $(pwd):/src python:3 python3 /src/run.py
```
- Add a second container
```
docker run --rm -it --net net_1 --name my_node node:latest /bin/bash
```
- Contact one container from another
```
ping my_py
```
By default all containers have access to the Internet
```
ping yahoo.com
```
### Remove Docker Container Network
```
docker network rm net_1
```
### An Example Network of Two Containers
Use a network to communicate with the first container from the second. For this example
two MySQL containers are created. One provides MySQL service (serves as a database) and
another is just accessing the first one with the bash terminal. (The second one is also MySQL 
just to provide continues run of the container)
- Create a network:
```
docker network create net_2
```
- Add first container to the network (running in background):
```
docker run -d --rm -e MYSQL_ROOT_PASSWORD=abc123 --name my_sql1 --net net_2 mysql:latest
```
- Add another container to the network (runnting interactively):
```
docker run -it --rm -e MYSQL_ROOT_PASSWORD=abc123 --name my_sql2 --net net_2 mysql:latest /bin/bash
```
- Communicate with the first container (which will run mysql terminal now):
```
mysql -h my_sql1 -u root -p
```
