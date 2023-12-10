---
layout: post
title: "Vultr Debian 服务器搭建 Shadowsocks"
description: ""
category: 技术
tags: ["Shadowsocks"]
published: true
---

```bash
ufw disable
```

```bash
apt-get install firewalld
```

开启 TCP 端口65534

```bash
firewall-cmd --zone=public --add-port=65534/tcp --permanent
```

加载配置

```bash
firewall-cmd --reload
```

安装 shadowsocks-libev

```bash
apt install shadowsocks-libev
```

启动 shadowsocks

> 服务器端口：65534，本地端口：8388，密码：123456，加密方法：chacha20-ietf-poly1305

```bash
nohup ss-server -s 0.0.0.0 -p 65534 -l 8388 -k 123456 -m chacha20-ietf-poly1305 &
```

服务器需要在防火墙规则里添加 65534 端口