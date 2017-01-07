---
layout: post
title: "Swift 使用 AFNetworking"
description: "Swift 使用 AFNetworking"
category: 技术
tags: ["Swfit","AFNetworking"]
published: true
---

## 环境 ##

*	使用 Swift 2.3

*	AFNetworking 3.1.0，[AFNetworking - GitHub](https://github.com/AFNetworking/AFNetworking)

*	CocoaLumberjack，调试输出使用，[CocoaLumberjack - GitHub](https://github.com/CocoaLumberjack/CocoaLumberjack)

## 代码 ##

*Get 请求*

<pre><code class="language-swift">let manager = AFHTTPSessionManager()
manager.GET(url, parameters: parameters, progress: nil, success: { (task, responseObject) in
    if responseObject != nil {
        DDLogDebug(responseObject)
    }
}) { (task, error) in
    DDLogError((task!.currentRequest?.URL?.absoluteString)! + "  ******  error:\r" + error.description)
}
</code></pre>

*Post 请求*

<pre><code class="language-swift">let manager = AFHTTPSessionManager()
manager.POST(url, parameters: parameters, progress: nil, success: { (task, responseObject) in
    if responseObject != nil {
        DDLogDebug(responseObject)
    }
}, failure: { (task, error) in
    DDLogError((task!.currentRequest?.URL?.absoluteString)! + "  ******  error:\r" + error.description)
})
</code></pre>

*监听网络环境*

<pre><code class="language-swift">AFNetworkReachabilityManager.sharedManager().startMonitoring()
AFNetworkReachabilityManager.sharedManager().setReachabilityStatusChangeBlock { (status) in
    switch status {
    case .Unknown:
        DDLogDebug("当前网络状态：Unknown")
    case .NotReachable:
        DDLogDebug("当前网络状态：NotReachable")
    case .ReachableViaWWAN:
        DDLogDebug("当前网络状态：ReachableViaWWAN")
    case .ReachableViaWiFi:
        DDLogDebug("当前网络状态：ReachableViaWiFi")
    }
}
</code></pre>

*判断是否有网络连接*

<pre><code class="language-swift">AFNetworkReachabilityManager.sharedManager().reachable
</code></pre>