# Docker

List all images

```
$ docker ps -a
```

Run <name> image

```
$ docker start <name>
```

# install postgres

```
docker run --name sql-postgres -e POSTGRES_USER=appuser -e  POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres:latest
```

## postgres management

[pgadmin](pgadmin.org)
