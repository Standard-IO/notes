# Docker notes
# Docker
## Basic commands
* Run a image (continer) `docker run -d --port [portlocal:containerPort] --name [containerName] [imageName]`
* Dowload an image:`docker pull [imageName]`
* delete a image `docker rmi [containerName]`
* dowload a image to cache `docker pull [imageName]`
* login docker image `docker login`

Containers
* list all container `docker ps -a`
* delete a container `docker rm [containterName]`
* open a terminal in a container `docker exec -it [container name] /bin/bash`

## docker file

Build a image using a docker file

* `docker build -t [name:tag] .` (the dot is the file name, this is used when the docker file is in the same folder)
* `docker build -t [name:tag] -f [fileName]` with this can build a image with a file in a different folder
* `docker build tag [imageName] [name:tag]` tag an existing image

docker image parts

`FROM [imageNameBase]` this part uses another image to build in the top
`COPY [fileOrigin] [fileDestinantion] ` copy a file to the container
`RUN [commmands]` run a command inside the container
`WORKDIR [dir]` indicate the work dir
`EXPOSE 8080`  add meta data the port to see
`ENTRY POINT ["node", "./app.js"]` what command to run when the docker container runs

## docker volumenes

The volumnes are used to prevent losing data. All the data in the docker container is lost once the job is terminated. To use it with a container we must to do:

```
docker run -d --name devtest -v myvol:/app nginx:latest
```

The option `-v` in the `run` command helps us to mounta volume in the container to use it.
`myvol:/app` maps the volume to a folder inside the container to use it.

**Note** instead of use a volume we can use a folder but this use is only for testing not for production use. So take this in count when use it and never use as production.

`docker create volume [volumeName]` create a volume
`docker volume ls` list the volumes
`docker volume inspect [volumeName]` inspect a volume
`docker volume rm [volumeName]` delete a volume
`docker volume prune` delete all the volumes not mounted 



