## Install java

```
$ apt install default-jdk -y
```

go to

```
$ sudo nano /etc/enviroment
```

add

```
JAVA_HOME="/usr/bin/java"
```

save & exit

```
$ source /etc/enviroment
```

run the file

```
$ echo $JAVA_HOME
```

test the variable
