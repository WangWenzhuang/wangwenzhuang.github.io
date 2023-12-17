---
layout: post
title: "Docker Nginx Vue 部署"
description: ""
category: 技术
tags: ["Docker", "Nginx", "Vue"]
published: true
---

## Dockerfile

```bash
FROM nginx:1.23.4
# 更改时区
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo Asia/Shanghai > /etc/timezone
# 解决中文乱码
ENV LANG C.UTF-8
# 拷贝 nginx 配置文件
COPY nginx.conf /etc/nginx/nginx.conf
COPY dist/  /usr/share/nginx/html/
```

## nginx.conf

```bash
user  nginx;
worker_processes  1;
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;
events {
    worker_connections  1024;
}
http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
    access_log  /var/log/nginx/access.log  main;
    sendfile        on;
    keepalive_timeout  65;
    gzip  on;
    server {
        listen       80;
        server_name  localhost;
        location / {
            try_files $uri $uri/ @router;
            root   /usr/share/nginx/html;
            index  index.html index.htm;
        }
        location @router {
            rewrite ^.*$ /index.html last;
        }
    }
}
```

## 编译容器

```bash
docker build . -t=“mynginx”
```

## 运行容器

```bash
docker run --name=website --restart=always -d -p 8081:80 mynginx
```