---
layout: post
title: "XcodeColors、CocoaLumberjack，带颜色的 Log"
description: "XcodeColors、CocoaLumberjack，带颜色的 Log"
category: 技术
tags: ["XcodeColors","CocoaLumberjack"]
published: true
---

#### 安装 XcodeColors ####

*	[XcodeColors - GitHub](https://github.com/robbiehanson/XcodeColors)

*	打开项目运行一下即可成功安装插件

*	退出 Xcode，退出 Xcode，退出 Xcode。重要的事情说三遍。

*	在“- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions” 中添加
	
		setenv("XcodeColors", "YES", 0);

####  CocoaLumberjack ####

*	[CocoaLumberjack - GitHub](https://github.com/CocoaLumberjack/CocoaLumberjack)

*	将 CocoaLumberjack 引入项目

*	在 xxx.pch 文件中定义日志级别

		#ifdef DEBUG
		static const int ddLogLevel = DDLogLevelVerbose;
		#else
		static const int ddLogLevel = DDLogLevelError;
		#endif

*	在“- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions”中添加

		[DDLog addLogger:[DDTTYLogger sharedInstance]];
		// 允许颜色
	    [[DDTTYLogger sharedInstance] setColorsEnabled:YES];
	    // 自定义日志颜色，这里更改默认 Debug 颜色
	    [[DDTTYLogger sharedInstance] setForegroundColor:UIColorFromRGB(100, 56, 32) backgroundColor:[UIColor whiteColor] forFlag:DDLogFlagDebug];

*	使用方法
	
		DDLogDebug(@"Debug");
	    DDLogError(@"Error");
	    DDLogWarn(@"Warning");
	    DDLogInfo(@"Info");
	    DDLogVerbose(@"Verbose");