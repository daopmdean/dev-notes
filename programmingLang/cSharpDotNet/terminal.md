```
dotnet --info
```

## Trust https certificate

```
dotnet dev-certs https --trust
```

## Create new project

See help

```
dotnet new -h
```

Create new solution

```
dotnet new sln
```

Create new web API with the name "API" or "DatingApp.API"

```
dotnet new webapi -o API
dotnet new webapi -n DatingApp.API
```

Add "API" to sln

```
dotnet sln add API
```

Create git ignore file

```
dotnet new gitignore
```

## Run

```
dotnet run
dotnet watch run
```

## Database Migration

### First install

```
dotnet tool install --global dotnet-ef
dotnet tool update --global dotnet-ef
```

### See help

```
dotnet ef -h
```

### Add migrations

create migration name InitialCreate

```
dotnet ef migrations add InitialCreate
dotnet ef migrations add InitialCreate -o Data/Migrations
```

### Update the migrations to database

```
dotnet ef database update
```

### Drop the database

```
dotnet ef database drop
```
