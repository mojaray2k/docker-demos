# Docker Cheatsheet

Docker info:

`docker info`

## Containers

### List Images

`docker images`
`docker images -a`

#### Get an Image

 `docker pull <name>[:<tag>]`
 `docker pull ubuntu:16.04`

#### Run an Image

 `docker run --name bob_the_container ubuntu /bin/bash`

### Create a new container with interactive shell

`docker run --name bob_the_container -i -t ubuntu /bin/bash`

### Create a daemonized container passing a command

`docker run --name daemon_dave -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"`

### Make container auto-restart

#### syntax

`docker run --restart=[always|on-failure|on-failure:int]`

#### example

`docker run --restart=on-failure:5 --name daemon_dave -d ubuntu /bin/bash`

### List Containers

#### only shows running containers

`docker ps`  

#### List all, running or not

`docker ps -a`

#### Start

`docker start <name|id>`

#### Build

##### with dockerfile present

`docker build .`

#### Attach

`docker attach <name|id>`

#### Stop

#### Stop by sending `SIGTERM`

`docker stop <name|id>`

#### Or really mean in with `SIGKILL`

`docker kill <name|id>`

### Remove Image

`docker rm [-f] <name>`

### View Logs

`docker logs <name|id>`

### monitor logs like tail

`docker logs -f <name|id>`

### limit logs

`docker logs --tail 10 <name|id>`

### follow logs starting now

`docker logs --tail 0 -f <name|id>`

### add a timestamp for easier debugging with -t

`docker logs -f -t <name|id>`

### Inspecting Container

`docker top <name|id>`

### Stats

`docker stats [<name>|id>]`

### example stats

`docker stats bob_the_container daemon_dave`

#### Get a lot more info with `inspect`

`docker inspect <name>`

### Running process inside containers

### Run a background task with `-d`

#### example make a new file in the container

`docker exec -d daemon_dave touch /etc/new_config_file`

#### Run an interactive task with `-i -t`

#### example which opens a new shell

`docker exec -i -t daemon_dave /bash/bin`

### Delete a container

#### While a container is not running

`docker rm <name|id>`

#### Or you can delete a container that is running

`docker rm -f <name|id>`

## Networking

### working with a network

`docker network create <name>`
`docker network inspect <name>`
`docker network ls`

#### run a container with a network

`docker run -d --net=<network_name> --name <name> <image_name>`
`docker run -d --net=app --name db docker/redis`

#### connect an existing container to a network

`docker network connect <network_name> <container_name>`
`docker network connect app db`

#### disconnect a container

`docker network disconnect <network_name> <container_name>`
