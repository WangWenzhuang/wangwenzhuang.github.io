---
layout: post
title: "Centos 安装 Nginx"
description: ""
category: 技术
tags: ["Centos", "Nginx"]
published: true
---

```bash
sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

sudo yum install -y nginx
```

启动：`sudo systemctl start nginx.service`

开机启动：`sudo systemctl enable nginx.service`

目录：/etc/nginx/nginx.conf

