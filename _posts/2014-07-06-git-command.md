---
layout: post
title: "Git 常用命令"
description: ""
category: 技术
tags: ["Git"]
published: true
---

## 初次运行的配置

设置用户信息

```bash
git config --global user.name "WangWenzhuang"
git config --global user.email "1020304029@qq.com"
```

查看配置信息列表

```bash
git config --list
```

查看单个配置信息

```bash
git config user.name
```

生成 SSH 公钥

```bash
ssh-keygen
```

## 常用命令

从远程仓库克隆

```bash
clone git@github.com:WangWenzhuang/test.git
```

查看状态

```bash
git status
```

添加文件

```bash
git add filename
```

删除文件

```bash
git rm filename
```

查看修改的内容

```bash
git diff
```

提交更新

```bash
git commit -m "提交更新"
```

查看提交历史

```bash
git log
```

查看远程仓库

```bash
git remote
git remote -v```

拉取远程仓库数据[不会自动合并]

```bash
git fetch git@github.com:wangwenzhuang/test.git
```

拉取远程仓库数据[自动合并]

```bash
git pull
```

将更新推送到远程仓库

```bash
git push
```

## 获取帮助

```bash
git help <verb>
```

例如查看config使用

```bash
git help config
```