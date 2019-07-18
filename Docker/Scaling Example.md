## Scaling with Docker
This example provides a configuration and commands to run Docker Composer for scaling web traffic.
### Files:
Python web server (/py/app.py):
```
import socket
from flastk inport Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "My container is named: " + socket.gethostname()
```
Nginx load balancer (/nginx/nginx.conf):
```
upstream serv {
    server docker-scaling_flask_1:5000;
    server docker-scaling_flask_2:5000;
    server docker-scaling_flask_3:5000;
    server docker-scaling_flask_4:5000;
    server docker-scaling_flask_5:5000;
    server docker-scaling_flask_6:5000;
}
server {
    listen 80;
    location / {
        proxy_pass http://serv;
    }
}
```
Docker Compose (/docker-compose.yml):
```
version: '3'
services: 
    flask:
        build: .
        volumes:
            - ./py:/src
        environment:
            - FLASK_APP=/src/app.py
    nginx:
        image: nginx:latest
        ports:
            - "2000:80"
        volumes:
            - ./nginx:/etc/nginx/conf.d
        depends_on:
            - flask
```
(`depends_on` means that nginx container will start only when all flask containewrs will be running)
Docker File (/dockerfile) to create Flask image
```
FROM python:3
RUN plp3 install flask
CMD flask run --host=0.0.0.0
```
### Create Scaling Network
In order to make everything work just run:
```
docker-compose up --scale flask=6
```
### Test on the Browser
Go to ```localhost:2000``` and check that each request returns different web server (container id)
