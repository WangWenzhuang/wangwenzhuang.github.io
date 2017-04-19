---
layout: post
title: "使用 Homebrew 安装 MySQL"
description: ""
category: Full Stack
tags: ["MySql"]
published: true
---

## 使用 Homebrew 安装

```bash
brew install mysql
```

## MySql 常用命令

启动

```bash
mysql.server start
```

重启

```bash
mysql.server restart
```

登录

```bash
mysql -u [用户名] -p
```

关闭

```bash
mysql.server stop
```

## 使用 Navicat Premium 客户端连接

Connection -> MySql，默认地址：localhost（127.0.0.1）