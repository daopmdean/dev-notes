# Commands

```
docker version
```

```
docker info
```

```
docker <command>
docker <command> <sub-command>
```

## CMD & ENTRYPOINT

```
FROM Ubuntu
CMD sleep 5
```

```
docker run ubuntu-sleeper sleep 10
```

```
FROM Ubuntu
ENTRYPOINT ["sleep"]
```

```
docker run ubuntu-sleeper 10
```

```
FROM Ubuntu
ENTRYPOINT ["sleep"]
CMD ["5"]
```

```
docker run ubuntu-sleeper
```


## run docker image on multiple ports
```
docker run -d -p 8080:80 -p 8443:443 my-web-app
```
start container from image name `my-web-app` , 
mapping port 8080 on local to port 80 in container (access on your host via localhost:8080)
mapping port 8443 on local to port 443 in container (access on your host via localhost:8443)
