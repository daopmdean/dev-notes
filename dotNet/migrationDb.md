## Work with code first approach

Import nuGet dependencies as mention in extensionVSCode.md  
Run commands mention in terminal.md

## appsettings.json

Add Connection, create db name datingapp.db

```json
"ConnectionString": {
  "DefaultConnection": "Data Source=datingapp.db"
},

```

```C#
public void ConfigureServices(IServiceCollection services)
{
  ...
  services.AddDbContext<DataContext>(
    x => x.UseSqlite(
      Configuration.GetConnectionString("DefaultConnection")
    )
  );
  ...
}
```
