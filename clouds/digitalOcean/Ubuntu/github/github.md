## Generate new key

```
$ ssh_keygen -t rsa
Enter...: /home/dean/.ssh/id_rsa_github
```

copy public key in id_rsa_github.pub, enter this command to see

```
$ cat .ssh/id_rsa_github.pub
```

paste the key to ssh key in github.

### Add ssh key to access github

```
$ ssh-add /home/dean/.ssh/id_rsa_github
```

### If could not open a connection, activate ssh agent:

```
$ eval `ssh-agent -s`
```
