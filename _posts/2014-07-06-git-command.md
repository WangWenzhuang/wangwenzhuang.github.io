---
layout: post
title: "Git 常用命令"
description: "git 简单配置和 git 的常用命令。用于随时查阅。。。"
category: 技术
tags: ["Git"]
published: true
---

#### 初次运行的配置 ####

设置用户信息

`$ git config --global user.name "WangWenzhuang"`

`$ git config --global user.email "1020304029@qq.com"`

查看配置信息列表

`$ git config --list`

查看单个配置信息

`$ git config user.name`

生成 SSH 公钥

`$ ssh-keygen`

#### 常用命令 ####

从远程仓库克隆

`$ git clone git@github.com:WangWenzhuang/test.git`

查看状态

`$ git status`

添加文件

`$ git add filename`

删除文件

`$ git rm filename`

查看修改的内容

`$ git diff`

提交更新

`$ git commit -m "提交更新"`

查看提交历史

`$ git log`

查看远程仓库

`$ git remote`

`$ git remote -v`

拉取远程仓库数据[不会自动合并]

`$ git fetch git@github.com:wangwenzhuang/test.git`

拉取远程仓库数据[自动合并]

`$ git pull`

将更新推送到远程仓库

`git push`

#### 获取帮助 ####

`$ git help <verb>`

例如查看config使用

`$ git help config`