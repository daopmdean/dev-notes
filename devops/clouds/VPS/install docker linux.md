update system
```
sudo apt update  
sudo apt upgrade
```

install necessary packages
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

Add the GPG key.
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Add the Docker repository to APT sources:
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

install docker engine
```
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```