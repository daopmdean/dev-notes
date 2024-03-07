# SQL Syntax

```
SELECT setval('table_seq', (SELECT MAX(id) FROM table_name));
```
