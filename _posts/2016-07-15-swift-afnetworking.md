---
layout: post
title: "使用 AFNetworking"
description: ""
category: Swfit
tags: ["AFNetworking"]
published: true
---

## 环境

* Swift 3.0.2

* Xcode 8.2.1

* [AFNetworking 3.1.0 - GitHub](https://github.com/AFNetworking/AFNetworking)

* 日志输出使用 [CocoaLumberjack 3.0.0 - GitHub](https://github.com/CocoaLumberjack/CocoaLumberjack)

## 快速使用

Get 请求

```swift
let manager = AFHTTPSessionManager()
manager.get("url", parameters: [ "key" : "value" ], progress: nil, success: { (task, responseObject) in
    if responseObject != nil {
        DDLogDebug(responseObject)
    }
}) { (task, error) in
    DDLogError((task!.currentRequest?.url?.absoluteString)! + "  ******  error:\r" + error.localizedDescription)
}
```

Post 请求

```swift
let manager = AFHTTPSessionManager()
manager.post("url", parameters: [ "key" : "value" , progress: nil, success: { (task, responseObject) in
    if responseObject != nil {
        DDLogDebug(responseObject)
    }
}, failure: { (task, error) in
    DDLogError((task!.currentRequest?.url?.absoluteString)! + "  ******  error:\r" + error.localizedDescription)
})
```

监听网络环境

```swift
AFNetworkReachabilityManager.shared().startMonitoring()
AFNetworkReachabilityManager.shared().setReachabilityStatusChange { (status) in
    switch status {
    case .unknown:
        DDLogVerbose("当前网络状态：Unknown")
    case .notReachable:
        DDLogVerbose("当前网络状态：NotReachable")
    case .reachableViaWWAN:
        DDLogVerbose("当前网络状态：ReachableViaWWAN")
    case .reachableViaWiFi:
        DDLogVerbose("当前网络状态：ReachableViaWiFi")
    }
}
```

判断是否有网络连接

```swift
AFNetworkReachabilityManager.shared().isReachable
```