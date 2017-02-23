---
layout: post
title: "[ Swift ] 高阶函数"
description: ""
category: Swift
tags: ["高阶函数"]
published: true
---

## 前言

> 高阶函数就是传递一个匿名闭包参数；使用高阶函数可以节省很多代码，也使代码更易读，总之很酷。看下面例子。

## 例子

### 求出数组中大于5的数

```swift
// 取出 arrya 大于5的元素添加到新数组
let array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

// 一般实现方式
var newArray1: [Int] = []
for item in array {
    if item > 5 {
        newArray1.append(item)
    }
}
// 使用 filter 函数
let newArray2 = array.filter({ $0 > 5 })
```

使用 **filter** 是不是很简洁？

## map 和 flatMap 对元素进行变换

> map 和 flatMap 可以将一个数组转化为另外一个数组

### map

```swift
let array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let newArray = array.map({ String($0) })
// newArray = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10"]
```

### flatMap

可以自动过滤 nil

```swift
let array = [1, 2, 3, 4, 5, 6, 7, 8, 9, nil, 10]
let newArray = array.flatMap({ return $0 == nil ? nil : String($0!) })
// ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10"]
```

将二维数组转化为一维数组

```swift
let array = [[1, 2, 3], [4, 5, 6, 7, 8, 9, 10]]
let newArray = array.flatMap({ $0 })
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

## filter 过滤元素是否应该包含在结果中

```swift
let array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let newArray = array.filter({ $0 > 5 })
// [6, 7, 8, 9, 10]
```

## reduce 将元素累加合并

```swift
let array = ["S", "w", "i", "f", "t"]
let result = array.reduce("", { $0 + $1}) // 简写形式 array.reduce("", { + })
// Swift
```

## 其他非常酷的函数

### sorted 排序

```swift
let array = [8, 3, 1, 2, 4, 9, 5, 6, 7]
let result = array.sorted(by: { $0 < $1 })
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### index 符合条件的元素索引

```swift
let array = [8, 3, 1, 2, 4, 9, 5, 6, 7]
let result = array.index(where: { $0 == 5 })
// Optional(6)
```

### first 符合条件的第一个元素

```swift
let array = [8, 3, 1, 2, 4, 9, 5, 6, 7]
let result = array.first(where: { $0 < 5 })
// Optional(3)
```

### contains 集合是否包含符合条件的元素

```swift
let array = [8, 3, 1, 2, 4, 9, 5, 6, 7]
let result = array.contains(where: { $0 > 10 })
// false
```

### max 符合条件的最大元素

```swift
let array = [8, 3, 1, 2, 4, 9, 5, 6, 7]
let result = array.max(by: { $0 < $1 }) // 也可以直接使用 array.max()
// Optional(9)
```

### min 符合条件的最小元素

```swift
let array = [8, 3, 1, 2, 4, 9, 5, 6, 7]
let result = array.min(by: { $0 < $1 }) // 也可以直接使用 array.min()
// Optional(1)
```

### prefix 取数组前 N 个元素

```swift
let array = [8, 3, 1, 2, 4, 9, 5, 6, 7]
let result = array.prefix(2)
// [8, 3]
```

### suffix 取数组后 N 个元素

```swift
let array = [8, 3, 1, 2, 4, 9, 5, 6, 7]
let result = array.suffix(2)
// [6, 7]
```
