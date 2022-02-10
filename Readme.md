# NGINX Basics
- adapted from https://www.youtube.com/watch?v=RzrIqzC9bQc (3 Parts Videos)
- https://github.com/techbeast-org/nginx-basics

# Part 1
## Install Nginx
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
5. Default config location
```
cd  /etc/nginx
```

![config location](https://i.imgur.com/kOjKVin.png)

```
cat /etc/nginx/nginx.conf
```
![nginx](https://i.imgur.com/pZk7KKn.png)

![nginx access logs](https://i.imgur.com/Xw5aPQ1.png)


## Sites-enabled
```
cd sites-enabled
```
![nginx sites-enabled](https://i.imgur.com/xMxcO8z.png)

``` 
cat default 
```
![nginx sites-enabled cat default 1](https://i.imgur.com/ahn31sU.png)
![nginx sites-enabled cat default 2](https://i.imgur.com/1GcvqBY.png)


## Sites-enable linked sites-available
```
ls -ltr
```
![nginx sites-enabled ls -ltr](https://i.imgur.com/iM8SlkO.png)

## Custom your own nginx pages and location

1. In ```sites-enable``` folder - to unlink the default config
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
2. create new conf file
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
3. Check config file
```
sudo nginx -t
```
![nginx -t](https://i.imgur.com/uPUugjK.png)



## root folder location - html
```
/var/www/html
```

## create a custom html location - huatcake.local
4. Make new folder for new custom location

```huatcake.local``` is created in ```/var/www/``` folder
then ``` cd huatcake.local ``` into the folder


```
sudo mkdir huatcake.local
```
![huatcake.local](https://i.imgur.com/frqQslw.png)



## To test the folder and location
5. Setup index.html page
``` 
sudo nano index.html
```
![default index.html](https://i.imgur.com/Gnx4NCV.png)


6. After which reload nginx 
```
sudo systemctl reload nginx
```
![reload nginx](https://i.imgur.com/bNTDhrn.png)



### Git clone repo
7. Go to the folder of ubuntu and git clone this repo

```
git clone 
``` 
![git clone](https://i.imgur.com/tj7YPjO.png)

### copy/mv the files over to ```huatcake.local```

```
sudo mv -v /home/ubuntu/nginx-basics-techbeast/* /var/www/huatcake.local/
```
![mv -v](https://i.imgur.com/zBDtibA.png)


### Access/Reload the website - updated
8. Refresh the website; update due to the git clone

![updated website](https://i.imgur.com/TluCKAn.png)


### Connect hyperlink to huat.html
9. Add hyperlink to nginx pages (click for huat toto)
```
cd  /etc/nginx/conf.d
```

![/etc/nginx/conf.d](https://i.imgur.com/SOmQ2vu.png)

Add location settings in the files
- / is index
- /huat is hyperlink huat.html

```

location / {

try_files $uri $uri/ $uri.html =400;

}

location /huat {

try_files $uri /huat.html;

}

```

![location huat.html](https://i.imgur.com/iVIoitI.png)

### Add error page /mypage or 400
10. Add error page /mypage or 400 to nginx pages
```

error_page 400 404 /400.html;
location = /400.html {

internal;
}

```
![400.html](https://i.imgur.com/mwApwRZ.png)



### Add server error page 500 / 50x
11. Add server error page 500 / 50x to nginx pages
```

error_page 500 502 503 504 /50x.html;
location = /50x.html {

internal;
}

```
![50x.html](https://i.imgur.com/ZLNv0Ko.png)



### To test or simulate server error 500

```

location /500error {
fastcgi_pass unix:/this/is/error;
}

```


![simulate server error 500](https://i.imgur.com/ulcMOaZ.png)

### Update Nginx config

```
sudo nginx -t

sudo systemctl reload nginx
```
![nginx reload -t](https://i.imgur.com/8iWyifv.png)

### Access the webpage again
Connected hyperlink

![update huat](https://i.imgur.com/5TZUh1Y.png)


Connected error pages such as 400 etc

![update 400 1](https://i.imgur.com/wK5fMK0.png)
![update 400 2](https://i.imgur.com/KNX6Tbc.png)

Simulate server error 500


![update 500](https://i.imgur.com/sr3XOOO.png)




# Part 2
https://i.imgur.com/rvfusCj.png


## Restrict access by IP address
1. Go to config location & edit the config file
```
cd  /etc/nginx/conf.d
```


2. ```sudo nano huatcake.conf``` add the below code into the config
- deny all - will deny all ip address
- allow - google your ip address and add in.

```

location /secure {

try_files $uri /secure.html;

allow X.X.X.X
deny all;

}


```

![secure.html](https://i.imgur.com/iwwDtUS.png)




3. nginx -t and systemctl reload nginx
[Reload nginx](#Config-validation---check-config-file)

4. To test address to the website. You can visit. To test secure, connect to another network.

## Protect sensitive pages using username & password (basic)
5. Install apache utils (not sure is the right way)

```
sudo apt-get install -y apache2-utils

if error;
sudo apt-get update 

```
6. run the command to add username and then enter password

```
sudo htpasswd -c /etc/nginx/huatpass huatuser

```
![add password and username](https://i.imgur.com/TXhjT0g.png)

7. Go to config file and edit for auth access
[conf.d folder](#conf.d-folder)

- Add the below commands for the page that require auth
- ```auth_basic_user_file``` will be the path folder added before (```/etc/nginx/huatpass```)

```

        auth_basic "Authentication is require!";
        auth_basic_user_file /etc/nginx/huatpass;

```

![add auth to page](https://i.imgur.com/LEyajqN.png)


8. nginx -t and systemctl reload nginx
[Reload nginx](#Config-validation---check-config-file)



### Password and user location
```
cat /etc/nginx/huatpass
```
![add auth to page](https://i.imgur.com/7kt70HM.png)

## SSL (skipped) - to use LetEncrypt instead
With the cert in the webserver, attached the settings via the config file 
[conf.d folder](#conf.d-folder)

![SSL Cert](https://i.imgur.com/60Pb5At.png)


# Part 3

# END