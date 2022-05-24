---
layout: post
title: "Centos 安装 Maven"
description: ""
category: 技术
tags: ["Centos", "Maven"]
published: true
---

## 配置源 

```bash
wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
```

## 安装

```bash
yum -y install apache-maven
```

### 配置文件路径

```bash
/etc/maven/settings.xml
```
## 配置

### 配置阿里云镜像

在 *settings.xml* 文件中的 *mirrors* 下添加 *mirror* 标签

`vi /etc/maven/settings.xml`

```bash
<mirror>
	<id>alimaven</id>
	<name>aliyun maven</name>
	<url>http://maven.aliyun.com/nexus/content/groups/public/</url>
	<mirrorOf>central</mirrorOf>
</mirror>
```