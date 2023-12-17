---
layout: post
title: "Docker Nginx 负载 Tomcat"
description: ""
category: 技术
tags: ["Docker", "Nginx", "Tomcat"]
published: true
---

## nginx.conf

```bash
#user  nobody;
worker_processes  1;

events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
    
    sendfile        on;
    #tcp_nopush     on;
    
    keepalive_timeout  65;
    
    #gzip  on;
    
    upstream database {
        server 172.17.1.64:8081   weight=1;
        server 172.17.1.64:8082   backup;#热备，nginx自带高可用，如果上面两台服务挂掉，则由此服务提供服务
    }
    
    server {
        listen       80;
        server_name  localhost;
    
        location / {
            proxy_pass http://database;
            proxy_redirect default;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
    
    # HTTPS server
    #
    server {
        listen       443 ssl;
        server_name  localhost;
    
        ssl_certificate      /root/ssl/cert.pem;
        ssl_certificate_key  /root/ssl/cert.key;
    
        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;
    
        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;
    
        location / {
            proxy_pass http://database;
            proxy_redirect default;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```

## Dockerfile

```bash
FROM java:8

# 更改时区
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo Asia/Shanghai > /etc/timezone

# 解决中文乱码
ENV LANG C.UTF-8

ADD target/database-1.0.jar app.jar

CMD java -jar app.jar

EXPOSE 8081
```

## Jenkins 命令

```bash
echo '*****   构建   *****'
mvn clean package -P dev -Dmaven.test.skip=true

echo '*****   编译镜像   *****'
docker build . -t="database"

echo '*****   停止服务1，使用热备服务2   *****'
#先停止databas1，然后启动database1，这样服务不会断，会使用热备database2
if docker ps -f NAME=database1 | grep -i database1; then
    docker stop database1
    docker rm database1
fi
docker run --name=database1 --restart=always -d -p 8081:8081 database
echo '*****   启动服务1   *****'

echo '*****   休眠10秒   *****'
sleep 10

echo '*****   停止服务2   *****'
if docker ps -f NAME=database2 | grep -i database2; then
    docker stop database2
    docker rm database2
fi
docker run --name=database2 --restart=always -d -p 8082:8081 database
echo '*****   启动服务2   *****'

echo '*****   删除none镜像   *****'
docker rmi $(docker images | grep "none" | awk '{print $3}')

echo '*****   发布完成   *****'
```