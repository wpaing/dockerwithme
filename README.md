
## Installation

Add to config into Dockerfile

```bash
vim Dockerfile


```
```
FROM ubuntu:latest 
LABEL maintainer="winpaingsoe" 
RUN  apt-get -y update && apt-get -y install nginx
COPY default /etc/nginx/sites-available/default
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
```

## Add nginx config into default file

``` bash
vim default
```
``` bash
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    
    root /usr/share/nginx/html;
    index index.html index.htm;

    server_name _;
    location / {
        try_files $uri $uri/ =404;
    }
}
```

## Add html file
``` bash
vim index.html
```
``` bash
<html>
  <head>
    <title>Dockerfile</title>
  </head>
  <body>
    <div class="container">
      <h1>My App</h1>
      <h2>This is my first app</h2>
      <p>Hello everyone, This is running via Docker container</p>
    </div>
  </body>
</html>
```

## And then , you can build container image  with Dockerfile

``` bash
sudo docker build -t yourcontainername-ver .
```

``` bash
sudo docker images 
```
``` bash
sudo docker run -d --name myweb -p 8080:8080 yourcontainername-ver
```
