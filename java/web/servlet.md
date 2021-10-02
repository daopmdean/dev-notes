## Access web.xml

In servlet class

```java
ServletContext context = getServletContext(); // from HttpServlet

Somevalue value = context.getInitParameter("somename");
```

In web.xml

```xml
<context-param>
  <param-name>somename</param-name>
  <param-value>somevalue</param-value>
</context-param>
```
