#  Docker 

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

## structure

- Stack: defines the interactions of all the service
- Services: defines how containers behave in production
- Container: 

## Container

`Dockerfile` define portable images or what goes on in the environment inside your container.

Access to resources like networking interfaces and disk drives is virtualized inside this environment, which is isolated from the rest of your system, so you need to map ports to the outside world, and be specific about what files you want to “copy in” to that environment.

### Example `Dockerfile`

```dockerfile
# Use an official Python runtime as a parent image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

### Building Image

```bash
# create a Docker image which stays in local Docker image registry
# --tag or -t option for naming the image
$ docker build --tag=friendlyhello .


$ docker image ls

REPOSITORY            TAG                 IMAGE ID
friendlyhello         latest              326387cea398
```

### Run the app 

To run the app, need to map the machine's port 400 to container's published port 80 using -p

```bash
$ docker run -p 4000:80 friendlyhello
or 
$ docker run -d -p 4000:80 friendlyhello
```

basically, we mapped `http://localhost:4000` to `http://0.0.0.0:80`

This port remapping of `4000:80` demonstrates the difference between `EXPOSE` within the `Dockerfile` and what the `publish`value is set to when running `docker run -p`.

### Stop the app

```bash
$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED
1fa4ab2cf395        friendlyhello       "python app.py"     28 seconds ago

$ docker container stop 1fa4ab2cf395
```

## Service

### what is service 

Services are really just “containers in production.” 

A service only runs one image, but it codifies the way that image runs—what ports it should use, how many replicas of the container should run so the service has the capacity it needs, and so on. Scaling a service changes the number of container instances running that piece of software, assigning more computing resources to the service in the process.

For docker platform, `docker-compose` define, run adn scale services

### Example `docker-compose.yml`

```yml
version: "3"
services:
  web:
    # replace username/repo:tag with your name and image details
    # Pull the image we uploaded in step 2 from the registry. 
    # you can use a local image, but you need to define the docker file location 
    image: username/repo:tag
    
    deploy:
    	# Run 5 instances of that image as a service called web, 
      replicas: 5
      # limiting each one to use, at most, 10% of a single core of CPU time (this 	could also be e.g. “1.5” to mean 1 and half core for each), and 50MB of RAM.
      resources:
        limits:
          cpus: "0.1"
          memory: 50M
      # Immediately restart containers if one fails.
      restart_policy:
        condition: on-failure
    # Map port 4000 on the host to web’s port 80.
    ports:
      - "4000:80"
    # Instruct web’s containers to share port 80 via a load-balanced network called webnet. (Internally, the containers themselves publish to web’s port 80 at an ephemeral port.)
    networks:
      - webnet
# Define the webnet network with the default settings (which is a load-balanced overlay network).
networks:
  webnet:
```

### status 

`docker-compose ps`: tells the status of containers

`docker-compose up -d`: hide the output due to deamon 

`docker-compose logs -f container_name` : -f to tail the log so you can see the output in real-time

### rebuild

when the dependencies had changed we need to rebuild the images 

`docker-compose down`

`docker-compose build`

`docker-compose up -d`

### running command

##### choose 1:

`docker-compose run`: launch a new container and runt he command 

##### choose 2:

`docker-compose exec`: try to run in an exiting container 

### Load-balanced app

```
$ docker sward init

# run it and give the app a name: hello
$ docker stack deploy -c docker-compose.yml hello 

# get the service name 
$ docker service ls

$ docker stack services hello_web
ID             NAME        MODE        REPLICAS   IMAGE               PORTS
bqpve1djnk0x   hello_web   replicated  5/5        username/repo:tag   *:4000->80/tcp
```



## Specifc to Django 

### exec command in Django container

`docker-compose exec Django_container ./manage.py` to exec the command for django container

### debugging into Django 

`docker ps`  to get the container ID and then run `docker attach <container ID>` to attach the debugger to container 

to exit the debugging mode, press 	`CTRL+P` or `CTRL+Q` but not `CTRL+C`, since it will terminate the contaienr 

### setting alias 

settting `alias dc='docker-compose' into the ~./.bash_profile 

## TroubleShooting

### proxy server settings

Proxy server can block connectiosnt o your web app once it is up and running. If you are behind a proxy server, add the following lines to your Dockerfile, using the `ENV` command to specify the host and port for your proxy servers:

```dockerfile
# Set proxy server, replace host:port with values for your servers
ENV http_proxy host:port
ENV https_proxy host:port
```

### DNS settings

DNS misconfigurations can generate problems with `pip`. You need to set your own DNS server address to make `pip` work properly. You might want to change the DNS settings of the Docker daemon. You can edit (or create) the configuration file at `/etc/docker/daemon.json` with the `dns` key, as following:

```json
{
  "dns": ["your_dns_address", "8.8.8.8"]
}
```

first element is < your dns address> and second element is an alternative DNS which is used when the first one is not available, in this case, `8.8.8.8` is the DNS of Google.

Once the `deamon.json` file is save, restart the docker service, and run and build the docker 

```
sudo service docker restart
docker build
docker run
```

### Permission

To avoid the permission errors or the use of `sudo`, add your user to the `docker` group 

https://docs.docker.com/install/linux/linux-postinstall/

## ShortCut

```bash
## List Docker CLI commands
docker
docker container --help

# shows more detail 
docker --version 															# Display Docker version and info
docker version 
docker info

## build and run
docker build -t hello . 				# Create image using this directory's Dockerfile
docker run hello																					# Execute Docker image
docker run -p 4000:80 hello				 # Run "friendlyhello" mapping port 4000 to 80
docker run -d -p 4000:80 hello        				# Same thing, but in detached mode

## container 
docker container ls                                # List all running containers
docker container ls -a             # List all containers, even those not running
docker container ls --all 								 
docker container ls -aq											 # List all containers in quiet mode
docker container stop <hash>           # Gracefully stop the specified container
docker container kill <hash>         # Force shutdown of the specified container
docker container rm <hash>        # Remove specified container from this machine
docker container rm $(docker container ls -a -q)         # Remove all containers

## image
docker image ls																							# List Docker images
docker image ls -a                             # List all images on this machine
docker image rm <image id>            # Remove specified image from this machine
docker image rm $(docker image ls -a -q)   # Remove all images from this machine

## publish
docker login             # Log in this CLI session using your Docker credentials
docker tag <image> username/repository:tag  # Tag <image> for upload to registry
docker push username/repository:tag            # Upload tagged image to registry
docker run username/repository:tag                   # Run image from a registry
```

## Reference 

https://docker-curriculum.com

https://docs.docker.com/get-started/

