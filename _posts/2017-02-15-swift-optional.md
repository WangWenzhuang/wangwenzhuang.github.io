---
layout: post
title: "[ Swift ] Optional（可选值）细节"
description: ""
category: Swift
tags: ["Optional"]
published: false
---

## ？和！号的区别

> 使用 ? 声明，在使用时需要使用 ! 来拆包。使用 ! 声明为已拆包，在使用时不需要 !

例子

```swift
// 使用?声明
var a: String? = "Hello, World"
var b: String = a! // 使用时需要用!

// 使用!声明
var c: String! = "Hello, World"
var d: String = c // 使用时不需要用!
```

## ?? 绑定默认值

> 有时可选值为**nil**时我们一般都希望可以指定一个默认值

例子

```swift
// 一般实现代码
var a: String? = nil
var b: String
if a == nil {
    b = "Hello, Worl"
} else {
    b = a!
}
// 或者使用三目简洁一点
var a: String? = nil
var b = a == nil ? a! : "Hello, World"

// 使用 ??
var a: String? = nil
var b = a ?? "Hello, World"
```