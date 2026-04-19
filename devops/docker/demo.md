nginx-play folder

```
docker build -t nginx:1.0 .
```

-> create image with name nginx:1.0

```
docker run -d -p 9090:80 --name webserver nginx:1.0
```

-> run the docker image, create a container

- -d run in detached mode
- -p port number, local-port:container-port
- --name name for the container