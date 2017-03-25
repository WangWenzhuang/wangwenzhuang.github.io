---
layout: post
title: "[ 敏捷 ] 移动端持续集成：Jenkins、fir.im"
description: ""
category: 敏捷
tags: ["敏捷", "持续集成", "Jenkins", "fir.im"]
published: true
---

# 持续集成

敏捷中重要的一项就是持续集成，简称 CI。

![ci](/images/post/2017-03-25-agile-continuous-integration-fir/ci.svg)

> 持续集成是一种软件开发实践，即团队开发成员经常集成他们的工作，通过每个成员每天至少集成一次，也就意味着每天可能会发生多次集成。每次集成都通过自动化的构建（包括编译，发布，自动化测试）来验证，从而尽早地发现集成错误。与持续集成相关的，还有两个概念，分别是持续交付和持续部署。

## 移动端持续集成

![ci1](/images/post/2017-03-25-agile-continuous-integration-fir/ci1.svg)

* 每天19:00自动获取源码

* 检查源码是否有变更，如果有变更，（执行单元测试，项目没写单元测试😓）执行编译打包，生成安装包文件

* 将安装包上传 fir.im(App 托管分发服务的平台)

* Email 发送构建报告

## 安装持续集成工具 Jenkins

[Jenkins](https://jenkins.io/index.html) 官网，下载安装包安装。

我是使用 *Homebrew* 进行安装的，安装 *Homebrew*。

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

安装 Jenkins

```bash
brew install jenkins    
```

启动 Jenkins

```bash
jenkins    
```

请在浏览器输入地址：http://localhost:8080/

初始化过程...省略一百字。

## 配置 Jenkins 构建项目

新建一个项目

![ci2](/images/post/2017-03-25-agile-continuous-integration-fir/ci2.png)

选择“构建一个自由风格的软件项目”

![ci3](/images/post/2017-03-25-agile-continuous-integration-fir/ci3.png)

简单配置就不做介绍了，将比较重要的记录下来。

### 构建触发器

我配置的是工作日19：00进行构建，前置条件是如果有源码变更。

![ci4](/images/post/2017-03-25-agile-continuous-integration-fir/ci4.png)

### 构建（适用于 iOS、Android）

增加构建步骤 -> 选择“Execute shell”，输入命令

![ci5](/images/post/2017-03-25-agile-continuous-integration-fir/ci5.png)

我这里偷懒了，直接使用 *fir.im-cli* 命令行工具进行构建，使用 *fir.im-cli* [请点这里](https://github.com/FIRHQ/fir-cli/blob/master/README.md)

### 构建后操作

增加构建后操作步骤 -> 选择“E-mail Notification”

![ci6](/images/post/2017-03-25-agile-continuous-integration-fir/ci6.png)

保存，现在构建并不会发送邮件，需要配置邮件通知的邮箱

### 配置邮件通知

系统管理 -> 系统设置

![ci7](/images/post/2017-03-25-agile-continuous-integration-fir/ci7.png)

设置“	系统管理员邮件地址”

设置“邮件通知”，根据你的邮箱进行设置即可。

![ci8](/images/post/2017-03-25-agile-continuous-integration-fir/ci8.png)

保存，执行构建，完！！！