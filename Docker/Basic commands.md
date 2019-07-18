## Basic Commands
```
docker container
docker image
docker run
```
Add options to those commands to run a Docker task

### List Docker Images
```
docker image ls
```

### List Docker Containers
- Running containers:
```
docker container ls
```
- All containers (Runnong and Exited):
```
docker container ls -a
```

### Run Docker Image
```
docker run <image>
```
Here <image> may be a REPOSITORY column name or 4 first characters of the IMAGE ID column that was seen in the List 
of Docker Images section.

### Stop Docker Container
```
docker container stop <id>
```
<id> is the id of the running container. You also may user a name of the container

### Run a Python File Example
- Create a Python file on the file system witb any text editor:
```
#Python
print("Hello World")
```
- Create a Volume. Mount present working directory of the working machine (current folder in terminal) on 
the container folder called `src`:
```
-v $(pwd):/src
```
- Specify which image you want to use for the container:
```
python:3
```
- Tell what file to run on the container:
```
python /src/hello-world.py
```
The full command may look like this:
```
docker run -v $(pwd):/src python:3 python /src/hello-world.py
```
Docker will download an image (if the image is not present on the machine yet) and run the file.
### Remove Docker Container
```
docker container rm <id>
```
where <id> is the container id or 4 characters of the id.
- To remove a container then it is finished executing, the run command should have ```--rm``` flag:
```
docker run --rm -v $(pwd):/src python:3 python /src/hello-world.py
```
- To remove all containers currnetly present:
```
docker container rm $(docker ps -a -q)
```
### Running Terminal (Bash) Inside Docker Container (Python example above)
```
docker run -it --rm python:3 /bin/bash
```
`-it` flag means "interactive mode"

Now you are inside the docker container file system.
- To exit from the container hit `Control + d`
### Running Node Image Interactively
```
docker run -it --rm node:latest /bin/bash
```
