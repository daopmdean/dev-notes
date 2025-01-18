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
