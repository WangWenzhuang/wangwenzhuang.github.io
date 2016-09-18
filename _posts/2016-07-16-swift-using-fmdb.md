---
layout: post
title: "Swift 使用 FMDB"
description: "Swift 使用 FMDB"
category: 技术
tags: ["Swfit","FMDB"]
published: true
---

#### 环境 ####

*   使用 Swift 2.3

*   FMDB 2.5，[FMDB - GitHub](https://github.com/ccgus/fmdb)

#### 代码 ####

##### 指定数据库 #####

<pre><code class="language-swift">let db = FMDatabase(path: "路径")
</code></pre>

*打开数据库*

<pre><code class="language-swift">db.open()
</code></pre>

*更新数据库*

>   insert、update、delete...等语句统一属于更新操作（executeUpdate）

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