# Docker 

## What is Docker?

Docker is a tool that allows developers, sys-admins etc. to easily deploy their applications in a sandbox (called *containers*) to run on the host operating system i.e. Linux. 

The key benefit of Docker is that it allows users to **package an application with all of its dependencies into a standardized unit** for software development.

## Why Docker?

The industry standard today is to use Virtual Machines (VMs) to run software applications. VMs run applications inside a guest Operating System, which runs on virtual hardware powered by the server’s host OS.

VMs are great at providing full process isolation for applications: there are very few ways a problem in the host operating system can affect the software running in the guest operating system, and vice-versa. But this isolation comes at great cost — the computational overhead spent virtualizing hardware for a guest OS to use is substantial.

Containers take a different approach: by leveraging the low-level mechanics of the host operating system, containers provide most of the isolation of virtual machines at a fraction of the computing power.

## Docker Concept

- Flexible: Even the most complex applications can be containerized.
- Lightweight: Containers leverage and share the host kernel.
- Interchangeable: You can deploy updates and upgrades on-the-fly.
- Portable: You can build locally, deploy to the cloud, and run anywhere.
- Scalable: You can increase and automatically distribute container replicas.
- Stackable: You can stack services vertically and on-the-fly.

### Image:

An **image** is an executable package that includes everything needed to run an application--the code, a runtime, libraries, environment variables, and configuration files.

### Container

A **container** is a runtime instance of an image--what the image becomes in memory when executed (that is, an image with state, or a user process).

A **container** runs *natively* on Linux and shares the kernel of the host machine with other containers. It runs a discrete process, taking no more memory than any other executable, making it lightweight.

By contrast, a **virtual machine** (VM) runs a full-blown “guest” operating system with *virtual* access to host resources through a hypervisor. In general, VMs provide an environment with more resources than most applications need

![Container vs. Virtual Machine](/Users/shuyi/Desktop/Notes/docker/container vs vm.png)

## Test Set Up 

To avoid the permission errors or the use of `sudo`, add your user to the `docker` group 

https://docs.docker.com/install/linux/linux-postinstall/

```
## List Docker CLI commands
docker
docker container --help

## Display Docker version and info
docker --version
# shows more detail 
docker version 
docker info

## Execute Docker image
docker run hello-world

## List Docker images
docker image ls

## List Docker containers (running, all, all in quiet mode)
docker container ls
docker container ls --all
docker container ls -aq
```



## status 

`docker-compose ps`: tells the status of containers

`docker-compose up -d`: hide the output due to deamon 

`docker-compose logs -f container_name` : -f to tail the log so you can see the output in real-time



## rebuild

when the dependencies had changed we need to rebuild the images 

`docker-compose down`

`docker-compose build`

`docker-compose up -d`



## running command

### choose 1:

`docker-compos run`: launch a new container and runt he command 

### choose 2:

`docker-compose exec`: try to run in an exiting container 



## Specifc to Django 

### exec command in Django container

`docker-compose exec Django_container ./manage.py` to exec the command for django container

### debugging into Django 

`docker ps`  to get the container ID and then run `docker attach <container ID>` to attach the debugger to container 

to exit the debugging mode, press 	`CTRL+P` or `CTRL+Q` but not `CTRL+C`, since it will terminate the contaienr 

### setting alias 

settting `alias dc='docker-compose' into the ~./.bash_profile 



## Reference 

https://docker-curriculum.com

