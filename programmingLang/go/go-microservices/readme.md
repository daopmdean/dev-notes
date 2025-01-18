
run project
```
go run ./cmd/web
```

## section 2

required go modules
```
go get github.com/go-chi/chi/v5
go get github.com/go-chi/cors  
```
run docker compose

```
docker-compose up -d
```

## Section 3 auth service
required go modules
```
go get github.com/go-chi/chi/v5
go get github.com/go-chi/cors  

go get github.com/jackc/pgconn
go get github.com/jackc/pgx/v4
```

## Section 4 logger service


required go modules
```
go get github.com/go-chi/chi/v5
go get github.com/go-chi/cors  

go get go.mongodb.org/mongo-driver/mongo
```
## section 5 mail service

```
go get github.com/vanng822/go-premailer/premailer
go get github.com/xhit/go-simple-mail/v2

```

## section 6 listener - rabbitmq


```
go get github.com/rabbitmq/amqp091-go
```


## section 7 - rpc

## section 8 - grpc

```
go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.27
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2

go get google.golang.org/grpc
go get google.golang.org/protobuf
```

https://grpc.io/docs/protoc-installation/

```
protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative logs.proto
```

## section 11 - testing

```
go test -v ./cmd/api
```