## Container
see running containers 
```
docker ps
docker ps -a # list all, even container stopped
```

stop running container
```
docker stop [container_name] [container_name2] [container_name3]
docker stop [container_id] [container_id2]
```

remove container
```
docker rm [container_name]
docker rm -f [container_name] # force to stop even it still running
```

to inspect container info
```
docker inspect [container_name]
```

## Image
```
docker images
```

remove images
```
docker rmi [image_name]
docker images rm [image_name]
```

pull image
```
docker pull [image_name:tag_name]
```


## Running 

pull image & run
```
docker run [image_name]
```

Run in detached mode
```
docker run -d [image_name]
```

run with environment
```
docker run -e ENV_NAME=env_value container_name
```

map port 8080 from container to port 80 in local machine
```
docker run -p 80:8080 daopmdean/web-app
```


example dockerfile for python flask server

```
FROM Ubuntu

RUN apt-get update
RUN apt-get install python

RUN pip install flask
RUN pip install flask-mysql

COPY . /opt/source-code

ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
```

build the docker image

```
docker build Dockerfile -t daopmdean/web-app
```

push to docker hub

```
docker push daopmdean/web-app
```

## Network

```
docker network create \
    --driver bridge \
    --subnet 182.19.2.2/16
    custom-isolated-network
```

```
docker network ls
```

## Volumes

```
docker run -v data_volumn:/var/lib/mysql mysql

docker run -v data/mysql:/var/lib/mysql mysql
```

or another syntax
```
docker run \
    --mount type=bind,source=data/mysql,target=/var/lib/mysql mysql
```

## Docker compose

normal commands
```
docker run -d --name=redis redis

docker run -d --name=db postgres:9.4

docker run -d --name=vote -p 5000:80 --link redis:redis voting-app

docker run -d --name=result -p 5001:80 --link db:db result-app

docker run -d --name=worker --link db:db --link redis:redis worker
```

docker-compose.yml

```yml
redis:
    image: redis
db:
    image: postgres:9.4
vote:
    image: voting-app
    ports:
        - 5000:80
    links:
        - redis
result:
    image: result-app
    ports:
        - 5001:80
    links:
        - db
worker:
    image: worker
    links:
        - redis
        - db
```

## Registry

```
docker login docker.io
```

```
docker image tag my-image docker.io/my-image

docker push docker.io/my-image

docker pull docker.io/my-image
```

## Docker swarm

```
docker swarm init

docker swarm join --token <token>
```

## Docker kubernetes

```
kubectl run --replicas=100 my-web-server
kubectl scale --replicas=1000 my-web-server
```

