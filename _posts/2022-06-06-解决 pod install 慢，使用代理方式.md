---
layout: post
title: "解决 pod install 慢，使用代理方式"
description: ""
category: 技术
tags: ["CocoaPods"]
published: true
---

> 慢的原因在于 GitHub 上的代码库访问速度慢，那么解决方案就是要加快 git 命令的速度

## 设置 Git 代理

```bash
git config --global http.https://github.com.proxy socks5://127.0.0.1:7890
```

socks5://127.0.0.1:7890 是代理

## 恢复设置

```bash
git config --global --unset http.https://github.com.proxy
```