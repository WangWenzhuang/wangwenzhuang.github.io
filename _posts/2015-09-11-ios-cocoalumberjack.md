---
layout: post
title: "使用 CocoaLumberjack 日志框架"
description: ""
category: iOS
tags: ["CocoaLumberjack"]
published: true
---

## 环境

* Swift 3.0.2

* Xcode 8.2.1

* [CocoaLumberjack - GitHub](https://github.com/CocoaLumberjack/CocoaLumberjack)

## 快速使用

* **CocoaLumberjack** 引入项目

	```bash
	CocoaPods：pod 'CocoaLumberjack'
	```
* 在 **application(_:didFinishLaunchingWithOptions:)** 中添加

	```swift
	DDLog.add(DDTTYLogger.sharedInstance(), with: DDLogLevel.verbose)
	```

* 打印到控制台
	
	```swift
	DDLogDebug("Debug")
    DDLogError("Error")
    DDLogWarn("Warning")
    DDLogInfo("Info")
    DDLogVerbose("Verbose")
	```