# Go commands

```
go list -m -versions github.com/golang-jwt/jwt
```

## Set remote module path to local

run this command to replace `example.com/greetings` with local greetings

```
go mod edit -replace example.com/greetings=../greetings
```

run this command to clean go.mod and make use of local module

```
go mod tidy
```
