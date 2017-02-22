---
layout: post
title: "[ Swift ] if let 和 guard else"
description: ""
category: Swift
tags: ["if let", "guard else"]
published: true
---

## if let

> 使用 if let 可以对可选值（Optional）进行绑定，条件判断

例子

```swift
let array = [1, 2, 3, 4, 5, 6]

// 查找是否包含元素 9，如果包含输出索引
// 一般实现代码
let index1 = array.index(where: { $0 == 9 })
if index1 != nil {
    print(index1!)
}

// 使用 if let
if let index2 = array.index(where: { $0 == 9 }) {
    print(index2)
}
```

对于可选值判断的操作是不是简单了许多，代码也更易读

## guard else

> guard else 对可选值绑定为 nil 时提前退出，是代码逻辑更清晰易读

例子

```swift
let array = [1, 2, 3, 4, 5, 6]

// 查找数组是否包含条件元素，如果包含，返回条件元素的2倍值
// 一般实现代码
func findNumber1(array: [Int], number: Int) -> Int? {
    let number = array.first(where: { $0 == number })
    if number == nil {
        return nil
    }
    return number! * 2
}

func findNumber2(array: [Int], number: Int) -> Int? {
    guard let number = array.first(where: { $0 == number }) else { return nil }
    return number * 2
}
```