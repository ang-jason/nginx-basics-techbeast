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
cd  /etc/nginx
```

![config location](https://i.imgur.com/kOjKVin.png)

```
cat /etc/nginx/nginx.conf
```
![nginx](https://i.imgur.com/pZk7KKn.png)
```Access logs and etc```
![nginx access logs](https://i.imgur.com/Xw5aPQ1.png)


## sites-enabled
```
cd sites-enabled

```
![nginx sites-enabled](https://i.imgur.com/xMxcO8z.png)

``` 
cat default 
```
![nginx sites-enabled cat default 1](https://i.imgur.com/ahn31sU.png)
![nginx sites-enabled cat default 2](https://i.imgur.com/1GcvqBY.png)


## sites-enable linked sites-available
```
ls -ltr
```
![nginx sites-enabled ls -ltr](https://i.imgur.com/iM8SlkO.png)

In ```sites-enable``` folder - to unlink the default config
```
sudo unlinked default
```
![nginx sites-enabled unlinked default](https://i.imgur.com/hXeRk2g.png)

Check if the link still present 
```
ls -ltr
```
![nginx sites-enabled check link](https://i.imgur.com/CnxDbl9.png)


## conf.d folder
Location conf.d folder - to be customised
```
/etc/nginx/conf.d
```
![nginx sites-enabled conf.d](https://i.imgur.com/IDGeUzB.png)
## Setup your own conf file 
```
sudo nano huatcake.conf
```

- specific the port number
- specific basic index page formats
- identify custom name of the server via server_name
- root directory of folders - where all the html locate
- always end with semicolons

## Starter config
```
server {

        listen 80 default_server;
        index index.html index.htm index.php;
        server_name huatcake.local;
        root /var/www/huatcake.local;

}

```

## Config validation - check config file

```
sudo nginx -t
```
![nginx -t](https://i.imgur.com/uPUugjK.png)



## root folder location - html
```
/var/www/html
```

## create a custom html location - huatcake.local
```huatcake.local``` is created in ```/var/www/``` folder
then ``` cd huatcake.local ``` into the folder


```
sudo mkdir huatcake.local
```
![huatcake.local](https://i.imgur.com/frqQslw.png)



## To test the folder and location
``` 
sudo nano index.html
```

index.html page is


![default index.html](https://i.imgur.com/Gnx4NCV.png)


After which reload nginx 
```
sudo systemctl reload nginx
```
https://i.imgur.com/bNTDhrn.png
![reload nginx](https://i.imgur.com/bNTDhrn.png)



## Git clone repo

Go to the folder of ubuntu and git clone this repo

```
git clone 
``` 
![git clone](https://i.imgur.com/tj7YPjO.png)


https://i.imgur.com/tj7YPjO.png

## copy/mv the files over to ```huatcake.local```

```
sudo mv -v /home/ubuntu/nginx-basics-techbeast/* /var/www/huatcake.local/
```
https://i.imgur.com/zBDtibA.png
![mv -v](https://i.imgur.com/zBDtibA.png)


## Access/Reload the website - updated

https://i.imgur.com/TluCKAn.png

![updated website](https://i.imgur.com/TluCKAn.png)


## Connect hyperlink to huat.html

```
cd  /etc/nginx/conf.d
```
https://i.imgur.com/SOmQ2vu.png
![/etc/nginx/conf.d](https://i.imgur.com/SOmQ2vu.png)


Add location settings in the files
```

location / {

try_files $uri $uri/ $uri.html =400;

}


location /huat {

try_files $uri /huat.html;

}



```
https://i.imgur.com/iVIoitI.png

![location huat.html](https://i.imgur.com/iVIoitI.png)


## Add error page /mypage or 400
```

error_page 400 404 /400.html;
location = /400.html {

internal;
}

```
https://i.imgur.com/mwApwRZ.png


![400.html](https://i.imgur.com/mwApwRZ.png)



## Add server error page 500 / 50x
```
error_page 500 502 503 504 /50x.html;
location = /50x.html {

internal;
}

```
https://i.imgur.com/ZLNv0Ko.png
![50x.html](https://i.imgur.com/ZLNv0Ko.png)



## To test or simulate server error 500

```

location /500error {
fastcgi_pass unix:/this/is/error;
}

```


https://i.imgur.com/ulcMOaZ.png
![simulate server error 500](https://i.imgur.com/ulcMOaZ.png)

## Update Nginx config

```
sudo nginx -t

sudo systemctl reload nginx
```
https://i.imgur.com/8iWyifv.png
![nginx reload -t](https://i.imgur.com/8iWyifv.png)

## Access the webpage again
Connected hyperlink
https://i.imgur.com/5TZUh1Y.png
![update huat](https://i.imgur.com/5TZUh1Y.png)


Connected error pages such as 400 etc
https://i.imgur.com/wK5fMK0.png
https://i.imgur.com/KNX6Tbc.png
![update 400 1](https://i.imgur.com/wK5fMK0.png)
![update 400 2](https://i.imgur.com/KNX6Tbc.png)

Simulate server error 500

https://i.imgur.com/sr3XOOO.png
![update 500](https://i.imgur.com/sr3XOOO.png)
## END