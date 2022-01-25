# SSH note

Generate key: ssh-keygen -t rsa  
Add identity:

```
$ ssh-add ~/.ssh/id_rsa_do
```

add in the root (~) in .ssh folder the file id_rsa_do

Go to server with root:

```
$ ssh root@128.199.147.233
```

Go to server with user:

```
$ ssh dean@128.199.147.233
```

## Generate SSH key

```
$ ssh-keygen -t rsa
```

when it prompt "Enter file in which to save the key...", enter the directory

```
/Users/daopham/.ssh/id_rsa_do
```

Enter to skip the password
