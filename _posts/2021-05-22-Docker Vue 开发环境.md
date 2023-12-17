---
layout: post
title: "Docker Vue 开发环境"
description: ""
category: 技术
tags: ["Docker", "Vue"]
published: true
---

## Dockerfile

```bash
FROM daocloud.io/node
# 更改时区
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo Asia/Shanghai > /etc/timezone
# 解决中文乱码
ENV LANG C.UTF-8
RUN mkdir /source
# 指定命令运行的目录
WORKDIR /source
# 给这个目录执行权限，x是执行权限
RUN chmod +x /source
VOLUME /source
EXPOSE 8080
```

## 编译容器

```bash
docker build . -t="vue_dev"
```

## 运行容器

```bash
docker run -i -t -d  -p 9527:8080 --restart=always -v /lszy_admin_web:/source --name=vue_dev --privileged=true vue_dev
```

## 编译&运行 Vue

```bash
docker exec -it lszydev /bin/bash

npm install

npm run serve
```

