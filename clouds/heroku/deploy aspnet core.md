# Deploy aspnet core on heroku

```
brew tap heroku/brew && brew install heroku
```

[dotnet build pack on heroku](https://elements.heroku.com/buildpacks/jincod/dotnetcore-buildpack)

set up heroku environment to production

```
heroku config:set ASPNETCORE_ENVIRONMENT=Production
```

## Heroku-18

```
heroku create --stack heroku-18
heroku stack:set heroku-18
```

## Heroku postgres

[Heroku postgres](https://devcenter.heroku.com/articles/heroku-postgresql)
