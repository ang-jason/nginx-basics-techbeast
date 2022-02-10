# NGINX Basics

# Part 3
## Introduction of Part 3
![Introduction of Part 3](https://i.imgur.com/TH6simV.png)


## Go to config file
[conf.d folder](#confd-folder)

https://i.imgur.com/gwCxhIb.png




## Single Server - Reverse Proxy
![Reverse Proxy](https://i.imgur.com/zGtebjc.png)

1. Add the upstream to the top ```app_3888``` can be any name. ```:3888``` will the port you want to specific/connect
```
upstream app_3888 {

        server 127.0.0.1:3888;

}

```
2. Add location and tag tot he proxy for reverse proxy
```


location /proxy {

proxy_pass http://app_3888/;


}

```



## Mutiple Server - Load Balancer
![Load Balancer](https://i.imgur.com/zkxnVQw.png)
- Round Robin - 1,2,3,1,2,3
- Least Connection - Server with the least connection will connect first
- IP Hash - Server will remember host ip and always connect to the server, unless the server is down.

### RoundRobin
```
upstream roundrobin {

        server 127.0.0.1:3888;
        server 127.0.0.1:3889;
        server 127.0.0.1:3887;
}

```
```
location /roundrobin {

proxy_pass http://roundrobin/;


}

```

### Least Connection
```
upstream leastconn {
least_conn;
        server 127.0.0.1:3888;
        server 127.0.0.1:3889;
        server 127.0.0.1:3887;
}

```
```
location /leastconn {

proxy_pass http://leastconn/;


}

```

### IP Hash
```
upstream iphash {
ip_hash;
        server 127.0.0.1:3888;
        server 127.0.0.1:3889;
        server 127.0.0.1:3887;
}

```
```
location /iphash {

proxy_pass http://iphash/;


}

```
# END