# New created linux server

## Connect to server

```
ssh root@172.105.xxx.xxx
```

<hr>

## Add new user

```bash
adduser dean
```

## Provide authorize

```
usermod -aG sudo dean
```

After new user added, you should connect to your server as new role next time

```
ssh dean@172.105.xxx.xxx
```

## Setup basic firewall

```
ufw allow sh
ufw allow http
ufw allow https
ufw allow 2377/tcp
ufw allow 7946/tcp
ufw allow 7946/udp
ufw allow 4789/udp
ufw allow 8025/tcp
ufw enable
```
```
ufw status
```

## Install Docker

Follow the [Intruction](https://docs.docker.com/engine/install/ubuntu/)

## Seting hostname

```
sudo hostnamectl set-hostname server-node-abc
```

Exit server

```
exit
```

Connect to server again for refresh.

To Change local config 

```
sudo vi /etc/hosts
```

Edit local env, such as

```
172.123.123.123 server-node-1
```

To exit vim, press `ESC`, then type
```
:wq
```

## Add docker manager & worker

```
sudo docker swarm init --advertise-addr 172.123.123.123
```

Notes: Replace 172.123.123.123 with your ip address

Copy the command generated & run in another server to add worker