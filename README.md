# Dockerize Python Application

## Installation

Require this project with docker desktop

## Use with Docker Development Environments

### flask application using a Redis 


Project structure:

```
.
├── Dockerfile
├── README.md
├── app/index.py
└── docker-compose.yml
```

[_docker-compose.yml_](docker-compose.yml)
```yaml

version: '3.8'
services:
    web:
        container_name: flask-redis
        build:
            context: .
            dockerfile: Dockerfile
        depends_on:
            - redis
        volumes:
            - ./app:/src/app
        ports:
            - 8000:80
    redis:
        container_name: redis-server
        image: redis
        restart: always
        ports:
            - "6379:6379"         
```

Deploy with docker compose

```cmd
docker compose up -d
[+] Running 2/2
 - Container redis-server  Started                                                                                 1.0s
 - Container flask-redis   Started
```


## Expected result

```
docker compose ps
NAME                SERVICE             STATUS              PORTS
flask-redis         web                 running             0.0.0.0:8000->80/tcp, :::8000->80/tcp
redis-server        redis               running             0.0.0.0:6379->6379/tcp, :::6379->6379/tcp
```

After the application starts, navigate to `http://localhost:8000` in your web browser or run:

```
$ curl localhost:8000
This webpage has been viewed 1 time(s)
```

Stop and remove the containers
```
$ docker compose down
 - Container flask-redis        Removed                                                                            0.4s
 - Container redis-server       Removed                                                                            1.8s
 - Network flask-redis_default  Removed
```
