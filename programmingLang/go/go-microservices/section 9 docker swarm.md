
```
docker login -u "daopmdean" -p "password" docker.io
```

build docker 
on logger-service
```
docker build -f logger-service.dockerfile -t logger-service:1.0.0 .

docker tag logger-service:1.0.0 daopmdean/logger-service:1.0.0

docker push daopmdean/logger-service:1.0.0
```

```
docker build -f broker-service.dockerfile -t daopmdean/broker-service:1.0.0 .

docker push daopmdean/broker-service:1.0.0
```

```
docker build -f listener-service.dockerfile -t daopmdean/listener-service:1.0.0 .

docker push daopmdean/listener-service:1.0.0
```

---

```
docker swarm init
```

add worker to swarm detail

```
docker swarm join --token SWMTKN-1-02wjiw5xv2vktb8ipqhgr8bnikucqoyq52d5wlrda1u6hwd3u8-7t4rkhtxjne7de3j8jvceimxa 192.168.65.3:2377
```

for instruction help
```
docker swarm join-token worker
docker swarm join-token manager
```

deploy docker swarm
```
docker stack deploy -c swarm.yml go-micro
```

listing services
```
docker service ls
```

for scaling service

```
docker service scale go-micro_logger-service=3
```

update service
```
docker service update --image daopmdean/logger-service:1.0.1 go-micro_logger-service
```

stop docker swarm

```
docker stack rm go-micro
```

```
docker swarm leave --force
```

monitor docker container resources usage
```
docker stats
```
## Caddy

```
sudo vi /etc/hosts
```