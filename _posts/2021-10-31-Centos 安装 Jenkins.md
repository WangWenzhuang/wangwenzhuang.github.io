---
layout: post
title: "Centos 安装 Jenkins"
description: ""
category: 技术
tags: ["Centos", "Jenkins"]
published: true
---

## 安装 java jdk

```bash
yum -y install java-1.8.0-openjdk*
```

## 安装 Jenkins

```bash
wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
yum install -y jenkins
```

修改默认端口：

```bash
vi /etc/sysconfig/jenkins
```

JENKINS_PORT="8080”，默认8080

启动：`service jenkins start/stop/restart`

下面两个插件可以和 gitlab 配合持续集成

- GitLab Plugin
- Gitlab Hook Plugin