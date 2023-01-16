# Container Registers

The containers are saved in register the docker hub is the official site and the default one but exists other alternatives as azure registers, aws and google as services.

The process to publish a image to the repository is like:
```bash

# login to docker hub
docker login -u <username> -p <password>

#tag the image previously build
docker tag my_image <repository>/my_image:latest

# push the image
docker push <repository>/my_image:latest

# pull the image
docker pull <repository>/my_image:latest 
```

follow along
```bash
docker build -t <YourRegisterName>/express:v1 .
docker push <YourRegisterName>/express:v1

# remove the image
docker rmi <YourRegisterName>/express:v1

# create a version v2

docker build <YourRegisterName>/express:v2 .
docker push <YourRegisterName>/express:v2

```