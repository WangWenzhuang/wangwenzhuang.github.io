---
layout: post
title: "Centos 安装 Docker"
description: ""
category: 技术
tags: ["Centos", "Docker"]
published: true
---

## 安装 Docker

```bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2

sudo yum-config-manager --add-repo https://mirrors.ustc.edu.cn/docker-ce/linux/centos/docker-ce.repo

sudo yum install docker-ce -y
```

启动

```bash
sudo systemctl start docker
```

开机启动

```bash
sudo systemctl enable docker
```



## 安装 docker-compose

```bash
yum install -y epel-release

yum install -y docker-compose
```

