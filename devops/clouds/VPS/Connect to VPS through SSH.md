
```
ssh root@103.232.120.25
```

root pass
```
4bzw0wJU
```

### if you can not ssh into your vps again
remove old key from known_hosts
```
ssh-keygen -R 103.232.120.25
```
then re-connect again
```
ssh root@103.232.120.25
```

