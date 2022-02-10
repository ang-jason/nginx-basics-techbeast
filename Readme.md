# NGINX Basics
- adapted from https://www.youtube.com/watch?v=RzrIqzC9bQc (3 Parts Videos)
- https://github.com/techbeast-org/nginx-basics

# Part 1
1. using ubuntu - install nginx
```
sudo apt-get install nginx
```

2. Check Nginx status
```
sudo systemctl status nginx
```
![NGINX active status](https://i.imgur.com/dpNimUX.png)



3. curl localhost
```
curl localhost
```
![curl localhost](https://i.imgur.com/emfgpAW.png)

4. Access Public Webpage
![Welcome NGINX](https://i.imgur.com/DFzDHzL.png)


## Config location
Default config location
```
/etc/nginx/nginx.conf

ls 
```
![config location](https://i.imgur.com/kOjKVin.png)

```
cat /etc/nginx/nginx.conf
```
![nginx](https://i.imgur.com/pZk7KKn.png)
Access logs and etc
![nginx access logs](https://i.imgur.com/Xw5aPQ1.png)


## sites-enabled
```
cd sites-enabled

```
![nginx sites-enabled](https://i.imgur.com/xMxcO8z.png)

``` cat default ```
![nginx sites-enabled cat default 1](https://i.imgur.com/ahn31sU.png)
![nginx sites-enabled cat default 2](https://i.imgur.com/1GcvqBY.png)


## sites-enable linked sites-available
```ls -ltr```
![nginx sites-enabled ls -ltr](https://i.imgur.com/iM8SlkO.png)

In ```sites-enable``` folder - to unlink the default config
```
unlinked default
```
![nginx sites-enabled unlinked default](https://i.imgur.com/hXeRk2g.png)
check if the link still present ```ls -ltr```
![nginx sites-enabled check link](https://i.imgur.com/CnxDbl9.png)


## conf.d folder
https://i.imgur.com/IDGeUzB.png

## Setup your own conf file 
```
nano huatcake.conf
```

specific the port number
specific basic index page formats
identify location of the server via server_name

always end with semicolons

## END