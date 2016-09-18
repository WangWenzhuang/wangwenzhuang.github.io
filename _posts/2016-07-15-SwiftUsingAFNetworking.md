---
layout: post
title: "Swift 使用 AFNetworking"
description: "Swift 使用 AFNetworking"
category: 技术
tags: ["Swfit","AFNetworking"]
published: true
---

#### 环境 ####

使用 Swift 2.3，AFNetworking 3.1.0

[AFNetworking - GitHub](https://github.com/WangWenzhuang/ZKAlertView)

#### 特点 ####

*   显示一个按钮，没有 Block 回调，主要用于提示信息

*   显示一个按钮，包含 Block 回调

*   显示多个按钮，包含 Block 回调

#### 安装 ####

<pre><code class="language-bash">CocoaPods：pod 'ZKAlertView'</code></pre>

#### 使用 ####

*#import "ZKAlertView.h"*

<pre><code class="language-objectivec">    [ZKAlertView
      showAlertWithTitle:@"ZKAlertView"
                 message:@"封装 UIAlertView，简单易用"
            clickAtIndex:^(UIAlertView *alertView, NSInteger buttonIndex) {
              NSLog(@"索引：%ld", buttonIndex);
            }
       cancleButtonTitle:@"取消"
       otherButtonTitles:@"按钮1", @"按钮2", @"按钮3", nil];</code></pre>

#### 运行环境 ####

*	iOS 7+
*	支持 armv7/armv7s/arm64