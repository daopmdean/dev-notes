## Update software

```
sudo apt update
```

## Upgrade software

```
sudo apt upgrade
```

## Add new user

```
$ adduser dean
```

After run the command, enter the new password

```
$ usermod -aG sudo dean
```

give user dean sudo permission

## Create ssh key for dean

```
$ cd /home/dean
$ mkdir .ssh
$ cd .ssh
$ touch authorized_keys
```

Now copy the public key, paste to authorized_keys

```
$ sudo nano authorized_keys
```

save the file.

## Turn off authorize for root

go to sshd_config

```
$ sudo nano /etc/ssh/sshd_config
```

change 'PermitRootLogin' to 'no'

reload the system

```
$ sudo systemctl reload sshd
```

## Give dean all permission

```
$ sudo chown -R dean:dean /home/dean
```

let's check

```
$ ls -la
```
