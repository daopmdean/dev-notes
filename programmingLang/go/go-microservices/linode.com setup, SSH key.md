
image

ubuntu LTS

## ssh

generate key
```
ssh-keygen -t ed25519 -C "daopmdean@gmail.com"
```

SSH keys are stored in the `~/.ssh/` directory
default file name will be stored in 
```
/Users/daopham/.ssh/id_ed25519
```

## setup linode

get into server with ssh

```
ssh root@139.162.60.93
```

```
# node-1
ssh daopham@139.162.60.93 

# node-2
```

setup user
```
adduser daopham
```

change user info/permission
```
usermod -aG sudo daopham
sudo usermod -aG docker daopham
```

setup firewall

UFW (Uncomplicated Firewall)

```
ufw allow ssh
ufw allow http
ufw allow https
```

firewall for ports

```
ufw allow 2377/tcp
ufw allow 7946/tcp
ufw allow 8025/tcp

ufw allow 7946/udp
ufw allow 4789/udp
```

```
ufw enable

ufw status
```

## docker setup

[docker link](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

setup
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

install docker
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

test
```
sudo docker run hello-world
```

## set hostname

```
sudo hostnamectl set-hostname node-1
```

open hosts file and update your linode ip address
```
sudo vi /etc/hosts
```

update host file 

```
# /etc/hosts
127.0.0.1 localhost
  
# The following lines are desirable for IPv6 capable hosts
::1 localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

# linode ips 
139.162.60.93 node-1
139.177.186.140 node-2
```

setup DNS

Go to your domain register site, setup DNS
```
Host or host name or name: node-1
Type: A
Ip address: 139.162.60.93
```

## Run swarm

node-1
```
sudo docker swarm init --advertise-addr 139.162.60.93
```

node-2
```
docker swarm join --token SWMTKN-1-4ga9a6nz3nj0y2gz90a99kupe02vh9jbnba7mkkt62d1sj3df6-95cfg3pka1ktuh9nzya3ytgm7 139.162.60.93:2377
```

build caddy image
```
docker build -f caddy.prod.dockerfile -t daopmdean/micro-caddy-prod:1.0.0 .
```


```
cd /
sudo mkdir swarm
sudo chown daopham:daopham swarm/
cd swarm
mkdir caddy_data
mkdir caddy_config

# create swarm.yml file with content of your deployment
vi swarm.yml
```

check container running status
```
docker node ls
docker node ps
docker node ps node-2

watch docker node ps
```

## connect linode postgres

host: 127.0.0.1
port: 5432
user: postgres
pass: password

connect over ssh

server: swarm.easypomo.com
port: 22
user: daopham
pass: yourpass

## mount data over servers

- https://www.gluster.org/
- https://phoenixnap.com/kb/sshfs