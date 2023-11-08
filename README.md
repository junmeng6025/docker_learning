# Docker Notebook

## Register your host machine to get sudo permission with docker:
```bash
sudo setfacl -m user:$USER:rw /var/run/docker.sock
```
## 1) Container vs. Image
- **Container**: a running environment for `Image`, 
  - provides all the environmental stuff:
    - file system
    - env configs
    - log files
    - **app image**
  - port binded
    - "talk" to the app running inside of it
  - **virtual** file system

- **Image**: application itself.
  - what we can find in `DockerHub`
  - tag/version

## 2) Container Port vs. Host Port
- Multiple `Containers` can run on our `Host` simutaneously
- Our PC has only certain ports available
- We need to create a "binding" between a port on our PC (the Host) and the Container
- Conflict happens when same port on Host machine binded to more than one Containers.
  - But multiple Containers with the same `Container Port` binded to different `Host Port`s would work without problems

## 3) Commands
### Pull & Run
```bash
docker pull ${ImageName:version}   
# -> download an IMAGE fron DockerHub

docker run ${ImageName:version}
# -> run an IMAGE (if not exist, pull and run right away)
# a randomely generated ContainerName

docker run --name ${ContainerName} ${ImageName:version}
# a given ContainerName

docker run -d ${ImageName:version}
# detached mode: leave the terminal usable

docker run -p ${HostPort}:${Containerport} ${ImageName:version}
# bind HOST port and CONTAINER port maneually
```
```bash
docker run -d -p ${HostPort}:${Containerport} --name ${ContainerName} ${ImageName:version}
```
```bash
docker start ${ContainerID/Name}

docker stop ${ContainerID/Name}
```
`docker run` vs. `docker start`:
- `docker run ${ImageName(:version)}` creates a new container from an image
- `docker start ${ContainerID/Name}` restart a stopped  container, which exists already
### List & Check
```bash
docker ps       # list the running CONTAINERs
docker ps -a    # list the running & history CONTAINERs
```
### Debug
```bash
docker logs ${ContainerID/Name}
```
get into Container's virtual file system:
```bash
docker exec -it ${ContainerID/Name} /bin/bash
#-it: Interactive Terminal
```
to exit container, get back to Host terminal:
```bash
exit
```
## 4) Workflow with Docker
- Development
- CI/CD
- Deployment
  
### create docker network

```bash
docker network create mongo-network
```

### start mongodb

```bash
docker run -d \
> -p 27017:27017 \
> -e MONGO_INITDB_ROOT_USERNAME=admin \
> -e MONGO_INITDB_ROOT_PASSWORD=password \
> --net mongo-network \
> --name mongodb \
> mongo
```

### start mongo-express

```bash
docker run -d \
> -p 8081:8081 \
> -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
> -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
> -e ME_CONFIG_MONGODB_SERVER=mongodb \
> --net mongo-network \
> --name mongodb-express \
> mongo-express
```