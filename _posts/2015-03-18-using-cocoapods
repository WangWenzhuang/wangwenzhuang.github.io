---
layout: post
title: "使用 CocoaPods"
description: ""
category: 技术
tags: ["CocoaPods"]
published: true
---

#### CocoaPods 简介 ####

在做 iOS 开发时我们总会用到各种第三方开源库，使用的时候都是通过下载源码，引入到工程，向工程添加开源库使用到的 Framework，如果开源库有更新的时候，还需要删除引入的旧代码，在重新引入最新代码到工程。

CocoaPods 就是为了解决这些麻烦的事情的，使用 CocoaPods 只需简单的配置一下就 OK 了。

#### 准备工作 ####

祖国的大局域网是安装不成功的，需要替换 ruby 的源更新为淘宝源：

    $gem sources --remove https://rubygems.org/
    $gem sources -a http://ruby.taobao.org/
    $gem sources -l

输出：http://ruby.taobao.org/就代表替换成功

#### CocoaPods 安装 ####

    $ sudo gem install cocoapods
    $ pod setup

等待安装成功。

#### CocoaPods 使用 ####

进入工程目录，创建 Podfile 文件，下面是一个例子：

    source 'https://github.com/CocoaPods/Specs.git'
    source 'https://github.com/Artsy/Specs.git'
    inhibit_all_warnings!

    platform :ios, '7.0'
    pod 'SVProgressHUD'
    pod 'CocoaLumberjack'
    pod 'AFNetworking', '~> 2.0'
    pod 'SDWebImage'

Podfile 文件的具体用法点这里[CocoaPods Guides - The Podfile](http://guides.cocoapods.org/using/the-podfile.html)

Terminal 进入到工程目录，输入如下代码：

    $ pod install

等待完成。完成之后会生成.xcworkspace 文件，在此之后打开工程使用此文件打开，而不是.xcodeproj 以后每次更新 Podfile 文件只需执行

    $ pod update

#### 可能出现的问题 ####

`Undefined symbols for architecture x86_64:`

解决办法：

修改Other Linker Flags，增加$(inherited)

