
---

Ref:
Channel: https://go101.org/article/channel.html
Use cases: https://go101.org/article/channel-use-cases.html

---
We can view channel as an internal FIFO (first in, first out) queue within a program

bidirectional channel type
```
chan T 
```

send-only channel type
```
chan<- T
```

receive-only channel type
```
<-chan T
```


