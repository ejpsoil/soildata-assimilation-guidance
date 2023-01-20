---
title: Overview Docker
summary: 
authors:
    - Paul van Genuchten
date: 2023-01-05
---

# Overview Docker

Docker is a virtualisation technology, slightly more efficient then running a virtual machine. With docker you run a full virtual environment (container) within your PC. Most containers run a flavour of Linux and you access them as if you access a remote server. Containers are based on a `docker-image`, a prepared set of operating system and software. Docker images are build locally from a `Dockerfile` (recipe) or downloaded from a repository such as [dockerhub](https://hub.docker.com/). Learn more about docker in the [Docker Overview](https://docs.docker.com/get-started/overview).

In this recipe we run most examples using Docker, because in this way there is no need to install any software on your computer, which may either not be allowed, give errors due to missing dependencies or in a worse case scenario can corrupt an existing configuration. 

On Windows and Apple we recommend to install [Docker Desktop](https://www.docker.com/products/docker-desktop/). Docker Desktop provides an additional panel to manage running containers. On Linux you can install [docker engine](https://docs.docker.com/engine/install/ubuntu/). Start docker engine from the start menu, if it is not already running. A general check can be triggered by typing `docker ps` in a console, this will provide a notification of docker availability and running containers.

In this recipe we will use the following Docker concepts:

- *Docker container*; an image deployed as a virtual environment. Most containers have an assigned port, so you can access the service of the container via the browser (for example, http://localhost:5000). You can also interact with containers from your commandline (docker ps, docker logs xxx, docker run geopython/pygeoapi)
- *Docker volume*; a folder on the host system which you mount as a folder into the container. Containers are destroyed when stopped, any file stored in the container file system is lost. By mounting a host folder into the container, you can persist items between runs of the container.
- *Docker compose*; with a compose file you orchestrate a cluster of containers into a functional system. One container runs a database, another container runs a webserver and the third container runs the web application. The compose file arranges that the containers can connect, on which port they run and which volumes they load.
- *Docker build* is the command to build a docker image from a `Dockerfile`
- With *Docker pull* you can pull an image from a repository 
- *Docker run* starts a container, press ctrl-c to stop is again (unless you run it with -d (detach) option then stop a container with `docker stop <id>`) 

Instead of running containers for permanent server applications, you can also start a container to run a short process, similar to running a command line utility. The container will stop when the process is finished. 

## Docker exercise

- Install Docker Desktop, verify it is running, else start it from the start menu.
- On commandline run this command
  
  ```
  docker run -p 80:80 --name test uzyexe/tetris:latest
  ```

- Open browser at http://localhost
- Open a shell within the container

```
docker exec -it test /bin/bash
```
- type `exit` to return to your pc
- ctrl-c to stop the container

(if other processes are running on port 80, Docker will throw an error, select another port, e.g. -p 81:80, and open http://localhost:81)

## Cleaning up

The virtual environments take quite some memory and CPU, you will notice this on older computers. Make sure to stop all containers after you finish using them. You can easily start them again later. `docker ps` (or the docker desktop window) indicate which containers are still running.

After your experiments you will notice the size of your harddisk has considerably been reduced. Images, containers, volumes all use quite some space. There is a single command to clean up everything

```
docker system prune -a
```

Only use it if you are sure you don't want to keep any docker resources.
