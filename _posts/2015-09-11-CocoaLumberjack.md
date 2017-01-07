---
layout: post
title: "XcodeColors、CocoaLumberjack，带颜色的 Log"
description: "XcodeColors、CocoaLumberjack，带颜色的 Log"
category: 技术
tags: ["XcodeColors","CocoaLumberjack"]
published: true
---

## 安装 XcodeColors ##

*	[XcodeColors - GitHub](https://github.com/robbiehanson/XcodeColors)

*	打开项目运行一下即可成功安装插件

*	退出 Xcode，退出 Xcode，退出 Xcode。重要的事情说三遍。

*	在“- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions” 中添加

	<pre><code class="language-objectivec">setenv("XcodeColors", "YES", 0);</code></pre>

##  CocoaLumberjack ##

*	[CocoaLumberjack - GitHub](https://github.com/CocoaLumberjack/CocoaLumberjack)

*	将 CocoaLumberjack 引入项目

*	在 xxx.pch 文件中定义日志级别

	<pre><code class="language-objectivec">#ifdef DEBUG
	static const int ddLogLevel = DDLogLevelVerbose;
	#else
	static const int ddLogLevel = DDLogLevelError;
	#endif</code></pre>

*	在“- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions”中添加

	<pre><code class="language-objectivec">[DDLog addLogger:[DDTTYLogger sharedInstance]];
	// 允许颜色
    [[DDTTYLogger sharedInstance] setColorsEnabled:YES];
    // 自定义日志颜色，这里更改默认 Debug 颜色
    [[DDTTYLogger sharedInstance]
     setForegroundColor:[UIColor redColor]
     backgroundColor:[UIColor whiteColor]
     forFlag:DDLogFlagDebug];</code></pre>

*	使用方法
	
	<pre><code class="language-objectivec">DDLogDebug(@"Debug");
    DDLogError(@"Error");
    DDLogWarn(@"Warning");
    DDLogInfo(@"Info");
    DDLogVerbose(@"Verbose");</code></pre>