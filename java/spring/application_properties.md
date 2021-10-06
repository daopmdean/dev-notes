# application.properties file

[properties list](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties)

config spring port to run

```
server.port=1234
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
