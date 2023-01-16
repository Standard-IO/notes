# Docker Compose

Docker compose is for small proyects that no need to power of application like kubernetes. Is very useful to dev enverioments before to use it in production with application like kubernetes.

Docker compose has two version previously `docker-compose` a python app but now is plugging written in go `docker compose`. Docker compose is used to run multiple containers at the time. So is very useful. This use a YAML file to use the containers like this:

```yaml
version 4.1

services:
    api1:
        image: myrepository.azurecr.io/api1
        ports:
            - '8080:80'
        restart: always

    api2:
        image: myrepository.azurecr.io/api2
        ports:
            - '8082:80'
        restart: always
```

* `docker compose build` buid the images
* `docker compose start` start the containers
* `docker compose stop` stop the containers 
* `docker compose up -d` build and start
* `docker compose ps` list what`s running
* `docker compose rm` Remove from memory
* `docker compose down` stop and remove
* `docker compose logs` get the logs
* `docker compose  exec [container] bash` run a command in a container 

To use docker compose is necessary to running inside the folder of the proyect. we can run multiple instances of the proyect assing it differents names previously this cannot be made but with the version 2.0 is possible.
```
docker compose up -d
```

In the next we name the second instance  as "test2" and run it when previously we have run another one.
```
docker compose -p test2 up -d

```

there are other command really useful to use:



* `docker compose --project-name test1 up -d` run a instance with name
* `docker compose -p test1 up -d` shortcut
* `docker compose ls` List running projects
* `docker compose cp [containerID]:[SRC_PATH] [DEST_PATH]` copy file from the container
* `docker compose [SRC_PATH] [containerID]:[DEST_PATH]` copy files to the container
 

# Docker compose file

The docker compose file is based in YAML file there we can specify multiple services and parameters thatn lets to configure it. In the compose file we can limit the service capacity with:

```yaml
services:
    redis:
        image: redis:alpine
        deploy:
            resources:
                limits:
                    cpus: '0.50'
                    memory: 150M
                reservations:
                    cpus: '0.25'
                    memory; 20M
```

in this compose file example the service redis is provisioned with 0.25 of the cpu capacity nad with 20 megabytes of ram memory and the limit are greater. so the service can not take more than  this in execution time.

## variables

The variables are can be set in the file too.

```yaml
services:
    web:
        image: nginx:alpine
        enviroments:
            - DEBUG=0
            - FOO=BAR
```

The values can be overwritten when the services are launched by:

```bash
docker compose  up -d -e DEBUG=1
```

The variables can be set in the nightly way settling in `.env` file docker compose will read it from there. This file must be in the same dir than the compose file to lauch.


```yaml
services:
    db:
        image: "postgres:${POSTGRES_VERSION}"
```
env file
```yaml
# set enviroment variable
export POSTGRES_VERSION=14.3

# powershell
$env:POSTGRES_VERSION= "14.3"

```

## Networking

When a service is launched exists in the default network and all services can call it be using its name service as host name. But we can define multiple networks inside of this default network to devide and make more secure our application. 

```yaml
services:
    web:
        image: nginx:alpine
        ports:
            - "8080:80"
    db:
        image: postgres
        ports:
            - "5432"

```

in the previous yaml we can see the the web service is exposed outside the default compose network but the database it is no.

### Multiple networks

In the next section we can see that we can have multiple networks. the `web` service on only is in the `frontend` network and the `db` is in `backend` network but the `app` is in both and can talk with the two apps the other no.

```yaml
services:
    web:
        image: nginx:alpine
        networks:
            - frontend
    db:
        image: postgres
        networks:
            - backend

    app:
        image: myapp
        networks:
            - frontend
            - backend

networks:
    frontend:
    backend:

```

## dependencies

Sometimes is necessary than a service is deploy it before another one with this in mind we need to use the next command in our docker compose file:

```yaml
services:
    app: 
        image: myapp
        depends_on:
            - db
    db:
        image: postgres
        networks:
            - back-tier
```

## Volumes named

You can declare volumenes in the docker compose file and use it in the services deployed. In the next compose file example we can see that `db-data:/etc/data` the volume is mapped and mounted at `/etc/data`.


```yaml
services:
    app:
        image: myapp
        depends_on:
            - db
    db:
        image: postgres
        volumes:
            - db-data:/etc/data
        networks:
            - back-tier

volumnes:
    db-data:
```

## restarting policy

Is a good practice to use the restarting policy

```yaml
services:
    app:
        image: myapp
        restart: always
    
    db:
        image: postgres
        restart: always
    
```