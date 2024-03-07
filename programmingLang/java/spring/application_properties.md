# application.properties file

[properties list](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties)

config spring port to run

```
server.port=1234
```

config context path

```
server.servlet.context-path=/api/v1
```

config database connection

```
spring.datasource.url=jdbc:mysql://localhost:3306/db_name?useSSL=false&serverTimezone=UTC
spring.datasource.username=username
spring.datasource.password=password
```

Auto migrations

```
spring.jpa.generate-ddl=true
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
```

config variables

```
abc.secretThing
```

use in java file

```java
@Value("${abc.secretThing}")
private String secretThing;
```
