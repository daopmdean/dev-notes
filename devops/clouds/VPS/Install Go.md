
Download go from curl
```
curl -OL https://golang.org/dl/go1.23.4.linux-amd64.tar.gz
```

Copy go to /usr/local/go
```
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.23.4.linux-amd64.tar.gz
```

Add /usr/local/go/bin to the `PATH` environment variable.
```
export PATH=$PATH:/usr/local/go/bin
```

check go version
```
go version
```