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

[AFNetworking - GitHub](https://github.com/AFNetworking/AFNetworking)

#### 代码 ####

*Get 请求*

<pre><code class="language-swift">let manager = AFHTTPSessionManager()
manager.GET(url, parameters: parameters, progress: nil, success: { (task, responseObject) in
    if responseObject != nil {
        print(responseObject)
    }
}) { (task, error) in
    print((task!.currentRequest?.URL?.absoluteString)! + "  ******  error:\r" + error.description)
}
</code></pre>

*Post 请求*

<pre><code class="language-swift">let manager = AFHTTPSessionManager()
manager.POST(url, parameters: parameters, progress: nil, success: { (task, responseObject) in
    if responseObject != nil {
        print(responseObject)
    }
}, failure: { (task, error) in
    print((task!.currentRequest?.URL?.absoluteString)! + "  ******  error:\r" + error.description)
})
</code></pre>