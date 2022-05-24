---
layout: post
title: "docker-compose 部署"
description: ""
category: 技术
tags: ["docker-compose"]
published: true
---

## Jenkins 命令

```bash
echo '*****   构建   *****'
mvn clean package -P test -Dmaven.test.skip=true

mkdir -p /root/logs/lszy1
mkdir -p /root/logs/lszy2
mkdir -p /root/logs/lszy3

echo '*****   部署   *****'
docker-compose up --force-recreate --build -d

echo '*****   热备   *****'
if docker ps -f NAME=lszyapibackup | grep -i lszyapibackup; then
    docker stop $(docker ps -f NAME=lszyapibackup -q)
fi
if docker ps -f NAME=lszyapibackup -a | grep -i lszyapibackup; then
    docker rm $(docker ps -f NAME=lszyapibackup -q -a)
fi
docker run --name=lszyapibackup --privileged=true --restart=always -m 512M -d -p 8083:8081 lszyapi


echo '*****   删除none镜像   *****'
docker rmi $(docker images | grep "none" | awk '{print $3}')

echo '*****   发布完成   *****'
```

## docker-compose.yml

```bash
version: '3'

services:
  nginx:
    container_name: lszyapi_nginx
    image: lszyapi_nginx
    build: ./nginx
    restart: always
    privileged: true
    links:
      - api1
      - api2
      - api3
    ports:
      - "8081:80"
    depends_on:
      - api1
      - api2
      - api3

  api1:
    container_name: lszyapi1
    build:
      context: .
      dockerfile: ./java/Dockerfile
    image: lszyapi
    restart: always
    privileged: true
    volumes:
      - /root/logs/lszy1:/root/logs

  api2:
    container_name: lszyapi2
    image: lszyapi
    restart: always
    privileged: true
    volumes:
      - /root/logs/lszy2:/root/logs

  api3:
    container_name: lszyapi3
    image: lszyapi
    restart: always
    privileged: true
    volumes:
      - /root/logs/lszy3:/root/logs
```

## Java 环境 Dockerfile

```bash
FROM daocloud.io/library/java:8

MAINTAINER Wangwenzhuang "1020304029@qq.com"

# 更改时区
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo Asia/Shanghai > /etc/timezone

# 解决中文乱码
ENV LANG C.UTF-8

ADD ./target/lszy-1.0.jar app.jar

CMD java -jar app.jar

EXPOSE 8081
```

## nginx Dockerfile

```bash
FROM daocloud.io/nginx

MAINTAINER Wangwenzhuang "1020304029@qq.com"

# 更改时区
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo Asia/Shanghai > /etc/timezone

# 解决中文乱码
ENV LANG C.UTF-8

# 拷贝 nginx 配置文件
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
```

## nginx.conf

```
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
        server api1:8081   weight=1;
        server api2:8081   weight=1;
        server api3:8081   weight=1;
    }

    server {
        listen       80;
        server_name  localhost;

        location / {
            proxy_pass http://lszy;
            proxy_redirect default;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```

