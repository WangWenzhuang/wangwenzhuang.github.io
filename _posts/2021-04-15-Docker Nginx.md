---
layout: post
title: "Docker Nginx"
description: ""
category: 技术
tags: ["Docker", "Nginx"]
published: true
---

## Dockerfile

```bash
FROM nginx:1.23.4
# 更改时区
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo Asia/Shanghai > /etc/timezone
# 解决中文乱码
ENV LANG C.UTF-8
COPY nginx.conf /etc/nginx/nginx.conf
COPY ssl/  /ssl/
EXPOSE 80
EXPOSE 443
```

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

    upstream lszy {
        server 192.168.0.165:8081   weight=1;
        server 192.168.0.165:8082   weight=1;
        server 192.168.0.165:8083   backup;
    }

    server {
        listen       80;
        server_name  wish-api.lingshilive.com;

        location / {
            proxy_pass http://lszy;
            proxy_redirect default;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }

    server {
        listen       443 ssl;
        server_name  wish-api.lingshilive.com;

        ssl_certificate      /ssl/cert.pem;
        ssl_certificate_key  /ssl/cert.key;

        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;

        location / {
            proxy_pass http://lszy;
            proxy_redirect default;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```

## 编译

```bash
docker build . -t="nginx_proxy"
```

## 运行

```bash
docker run --name=nginx_proxy --restart=always -d -p 80:80 -p 443:443 -v ./logs/nginx:/var/log/nginx nginx_proxy
```

## 使用 docker-compose 运行

### docker-compose.yml

```bash
version: '3'

services:
  nginx:
    container_name: nginx_proxy
    build: .
    image: nginx_proxy
    restart: always
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./log:/var/log/nginx
```

### 运行

```bash
docker-compose up --force-recreate --build -d
```