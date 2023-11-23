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
### Check system version in a running docker container
```bash
cat /etc/*release
```
### Pull & Run
```bash
docker pull ${ImageName:version}   
# -> download an IMAGE fron DockerHub

docker run ${ImageName:version}
# -> run an IMAGE (if not exist, pull and run right away)
# a randomely generated ContainerName

docker run --name ${ContainerName} ${ImageName:version}
# [Recommanded] a given ContainerName

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
- `docker rm ${ContainerID/Name}`: remove an existing container

  > This would be helpful to kill too much redundant containers with the same image

### Push a local image to docker hub
1. Log in your docker hub
```bash
docker login -u ${USER_NAME}
```
- my PASSWORD:
  ```txt
  dckr_pat_MgOA_Ex5EU6Xy_xYIMZ8Em8Nc1g
  ```

2. Tag the local image to your docker hub
```bash
docker tag LOCAL_IMAGE YOUR_DOCKERHUB_NAME/IMAGE_NAME
```
3. Push
```bash
docker push YOUR_DOCKERHUB_NAME/IMAGE_NAME
```
4. (Optional) Untag the redundant image tag:
```bash
docker rmi YOUR_DOCKERHUB_NAME/IMAGE_NAME
```

### Rename an existing image
```bash
docker tag ${IMAGE_ID} ${NEW_IMAGE_NAME}
docker rmi ${OLD_IMAGE_NAME}
```

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
# -it: Interactive Terminal
```
- to execute a Container, should start it first
  ```bash
  docker start ${ContainerID/Name}
  ```
to exit container's terminal, get back to Host terminal:
```bash
exit
```
  - cmd "`exit`" won't stop it, the container is still running

***

a quick `.sh` script:
```sh
DOCKER_NAME="IMAGE_NAME:TAG "
CONTAINER_NAME="CONTAINER_NAME"
printf "Using docker image %s\n" $DOCKER_NAME

# Port bindings: -p host_port:container_port
data="DATA/PATH/TO/LOAD"
workspace="WORKSPACE/PATH/TO/LOAD"

docker run -it --gpus all \
           --shm-size=4g \
           -v $data:/data \
           -v $workspace:/workspace \
           --name ${CONTAINER_NAME} \
           ${DOCKER_NAME}
```

## 4) Workflow with Docker
see [demo_app README](demo_app/README.md)

## 5) Commit Changes to Image
```bash
sudo docker commit ${CONTAINER_ID} ${new_image_name}
```