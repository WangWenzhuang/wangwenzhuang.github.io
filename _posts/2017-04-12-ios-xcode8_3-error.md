---
layout: post
title: "[ iOS ] Xcode 8.3 命令打包出错"
description: ""
category: iOS
tags: ["Xcode"]
published: true
---

# 问题

`xcrun: error: unable to find utility "PackageApplication", not a developer tool or in PATH`

# 原因

*PackageApplication* 在前几个版本已被标识为废弃，在8.3版本彻底移除了

# 解决方法

* [PackageApplication 下载](https://pan.baidu.com/s/1jHJF2Lo)

* 复制到 */Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin/* 目录下

* 执行命令 

    1. `sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer/`

    2. `chmod +x /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin/PackageApplication`