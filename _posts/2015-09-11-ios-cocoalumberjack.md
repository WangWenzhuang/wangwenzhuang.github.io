---
layout: post
title: "使用 CocoaLumberjack 日志框架"
description: ""
category: iOS
tags: ["CocoaLumberjack"]
published: true
---

##  CocoaLumberjack

*	[CocoaLumberjack - GitHub](https://github.com/CocoaLumberjack/CocoaLumberjack)

*	将 **CocoaLumberjack** 引入项目

*	在 **xxx.pch** 文件中定义日志级别

	<pre><code class="language-objectivec">#ifdef DEBUG
	static const int ddLogLevel = DDLogLevelVerbose;
	#else
	static const int ddLogLevel = DDLogLevelError;
	#endif</code></pre>

*	在 **- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions** 中添加

	<pre><code class="language-objectivec">[DDLog addLogger:[DDTTYLogger sharedInstance]];
	// 允许颜色
    [[DDTTYLogger sharedInstance] setColorsEnabled:YES];
    // 自定义日志颜色，这里更改默认 Debug 颜色
    [[DDTTYLogger sharedInstance] setForegroundColor:[UIColor redColor] backgroundColor: [UIColor whiteColor] forFlag:DDLogFlagDebug];</code></pre>

*	打印到控制台
	
	<pre><code class="language-objectivec">DDLogDebug(@"Debug");
    DDLogError(@"Error");
    DDLogWarn(@"Warning");
    DDLogInfo(@"Info");
    DDLogVerbose(@"Verbose");</code></pre>