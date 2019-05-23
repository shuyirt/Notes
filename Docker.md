# Docker 

# status 

`docker-compose ps`: tells the status of containers

`docker-compose up -d`: hide the output due to deamon 

`docker-compose logs -f container_name` : -f to tail the log so you can see the output in real-time

# rebuild

when the dependencies had changed we need to rebuild the images 

`docker-compose down`

`docker-compose build`

`docker-compose up -d`

# running command

### choose 1:

`docker-compos run`: launch a new container and runt he command 

### choose 2:

`docker-compose exec`: try to run in an exiting container 



## Specifc to Django 

### exec command in Django container

`docker-compose exec Django_container ./manage.py` to exec the command for django container

### debugging into Django 

